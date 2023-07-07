---
sidebar_position: 1
---

# Run a Validator

## Create Your Validator

Your node public key can be used to create a node by pledging a Unit Token. You can find your Validator public key with the following command.

```shell
    treasurenetd tendermint show-validator

    {"@type":"/cosmos.crypto.ed25519.PubKey","key":"ZZ35B4oaIo2Az2+Pt8QW/3xIaRPRRXFKb14mmzvdjFw="}
```

:::caution
❗️ Note: Never use the test mode keyring backend to create your primary network validator key. Doing so may cause your funds to be accessed remotely through the eth_sendTransaction JSON-RPC node, resulting in a loss of funds

Reference：[Security Advisory: Insecurely configured geth can make funds remotely accessible](https://blog.ethereum.org/2015/08/29/security-alert-insecurely-configured-geth-can-make-funds-remotely-accessible)
:::

To start your Validator node on the test network, use the following command:

```shell

treasurenetd tx staking create-validator \
  --amount=158000000000000000000aUnit \
  --pubkey=$(treasurenetd tendermint show-validator) \
  --moniker="choose a moniker" \
  --chain-id=<chain_id> \
  --commission-rate="0.05" \
  --commission-max-rate="0.10" \
  --commission-max-change-rate="0.01" \
  --min-self-delegation="1000000" \
  --gas="auto" \
  --gas-prices="0.025aUnit" \
  --from=<key_name>


```

## Edit Validator Description

You can modify the public representation of your validator, which is used to identify your validator. Stakers use this information to determine which validator to stake their tokens to.

Please make sure to provide all the required parameters. If any of these parameters are not provided, the corresponding content will be empty. (If `moniker` is not provided, it defaults to the device name.)

The --identity flag can be utilized for authentication purposes with systems like Keybase or UPort. In case of Keybase, you should populate your account with a 16-bit string that is generated by [keybase.io](https://keybase.io/) --identity. This method ensures a cryptographically secure authentication of your identity across various online networks. By retrieving your Keybase avatar via the Keybase API, you can add your logo to the authenticator profile. If you do not provide this flag, your node’s public key will be used as the node identity.

<key_name> is used to specify the validator you are editing. If you choose not to include certain flags, remember that the --from flag must be included to identify the validator to be updated

```shell

treasurenetd tx staking edit-validator
  --moniker="choose a moniker" \                #The validator's name
  --website="https://www.treasurenet.io" \      #The validator's (optional) website
  --identity=6A0D65E29A4CBC8E \                 #The (optional) identity signature (ex. UPort or Keybase)
  --details="To infinity and beyond!" \         #The validator's (optional) details
  --chain-id=<chain_id> \                       #The network chain ID
  --from=<key_name> \                           #Name or address of private key with which to sign
  --commission-rate="0.10"                      #The new commission rate percentage


```

## View Validator Description

```shell
    treasurenetd query staking validator <account>
```

## Track Validator Signing Information

```shell
    treasurenetd query slashing signing-info <validator-pubkey> --chain-id=<chain_id>
```

## Unjail Validator

When the validator is "Jail" due to downtime, double-signing, etc., you must submit unjail transactions from your validator operator account to receive block rewards again.

```shell
    treasurenetd tx slashing unjail --from=<key_name> --chain-id=<chain_id>
```

## Confirm Your Validator is Running

```shell
    treasurenetd query tendermint-validator-set | grep "$(treasurenetd tendermint show-address)"
```

## Common Problems

### My validator voting power is 0.

Maybe, Your validator is in Jail status. This is usually because validators have not participated in 500 votes of the last 10,000 blocks or the validators have double-signed.

If it is confirmed that your validator has a jail status due to one of the above actions, you can try to recover it in one of these ways.
First, if the validator is not running, try to start it using the following command.

```shell
    treasurenetd start
```

Wait for the node to update to the latest block (the time depends on the gap between your node and the latest block), then try to unjail your validator.

You can refer to the section on[unjail your validator 章节](#unjail-validator)

Finally, check that your validator's voting power is back to normal

```shell
    treasurenetd status
```

### My node crashes because of `too many open files`.

The default number of files that Linux can open (per process) is 1024. treasurenetd may cause a process to crash if more than 1024 files are opened.

A quick fix is to run `ulimit -n 4096` command (i.e. increase the number of files allowed to be opened) and then restart the process using `treasurenetd start` command.

If you are using systemd or another process manager to start treasurenetd, you may need to do some configuration at that level. An example systemd file to solve this problem is as follows:

```shell
# /etc/systemd/system/treasurenetd.service
[Unit]
Description=TreasurenNet Node
After=network.target

[Service]
Type=simple
User=ubuntu
WorkingDirectory=/home/ubuntu
ExecStart=/home/ubuntu/go/bin/treasurenetd start
Restart=on-failure
RestartSec=3
LimitNOFILE=4096

[Install]
WantedBy=multi-user.target
```