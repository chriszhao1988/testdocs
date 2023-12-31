---
sidebar_position: 1
---

# 交易

交易是指由账户发起的改变区块链状态的行为。为了有效地执行状态更改，每笔交易都会广播到整个网络。任何节点都可以广播请求在区块链状态机上执行的交易；发生这种情况后，验证器将验证、执行交易并将产生的状态更改传播到网络的其余部分。

为了处理每笔交易，网络上的计算资源都会被消耗。因此，“gas”的概念是作为验证者处理交易所需的计算的参考而出现的。用户必须为此计算付费，所有交易都需要相关费用。该费用是根据执行交易所需的燃料费和燃料费价格计算的。

此外，交易需要使用发送方的私钥进行签名。这证明交易只能来自发件人，而不是欺诈性发送。

简而言之，将签名交易提交到网络后的交易生命周期如下：

- 交易哈希是加密生成的。
- 该交易被广播到网络并添加到由所有其他未决网络交易组成的交易池中。
- 验证者必须选择你的交易并将其包含在一个块中，以验证交易并认为它“成功”。

交易哈希是一个唯一标识符，可用于检查交易信息，例如，发出的事件是否成功。

交易可能因各种原因而失败。例如，提供的 gas 或费用可能不足。此外，交易验证可能会失败。每笔交易都有特定的条件，必须满足这些条件才能被视为有效。一个广泛的验证是发送者是交易签名者。在这种情况下，如果您在发件人地址与签名者地址不同的地方发送交易，即使费用足够，交易也会失败。

## Cosmos 交易

在 Cosmos 链上，交易由存储在上下文和 sdk.Msg 中的元数据组成，这些元数据通过模块的 Protobuf Msg 服务触发模块内的状态更改。

当用户想要与应用程序交互并进行状态更改（例如发送代币）时，他们创建交易。Cosmos 交易可以包含多个 sdk.Msgs。在交易广播到网络之前，每个 sdk.Msg 都必须使用与相应账户关联的私钥进行签名。

Cosmos 交易包括以下信息：

- Msgs：消息数组（sdk.Msg）
- GasLimit：用户选择的选项，用于计算他们需要支付多少燃料费
- FeeAmount：用户愿意支付的最大费用
- TimeoutHeight：交易有效的区块高度
- Signatures: 来自交易所有签名者的签名数组
- Memo: 随交易发送的注释或评论

要提交 Cosmos 交易，用户必须使用提供的客户端之一。

## 以太坊交易

以太坊交易是指由人类管理的 EOA（外部拥有账户）发起的操作，而不是内部智能合约调用。以太坊交易会改变 EVM 的状态，因此必须广播到整个网络。

以太坊交易还需要支付一定的费用，称为燃料费（gas）。EIP-1559 引入了基础费用的概念，以及优先费用作为矿工将特定交易包含在区块中的激励。

以太坊交易可以分为以下几类：

- 常规交易：从一个账户向另一个账户的交易。
- 合约部署交易：没有 to 地址的交易，合约代码被发送到数据字段中。
- 执行合约交易：与已部署的智能合约进行交互的交易，to 地址为智能合约地址。

一个以太坊交易包括以下信息：

- recipient: 接收者地址
- signature: 发送者签名
- nonce: 交易编号计数器
- value: 要转账的代币数量
- data: 包括任意数据。 在部署智能合约或进行智能合约方法调用时使用
- gasLimit: 要消耗的最大燃气费用
- maxPriorityFeePerGas: 包括在向验证器支付小费的最高每单位燃气费用
- maxFeePerGas: 为 tx 支付的最大 gas 量

Treasurenet 支持以下以太坊交易。
