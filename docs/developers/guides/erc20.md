---
sidebar_position: 1
---

# 发行 ERC-20/ERC-721/ERC-1155 代币

## 代币

Token 几乎可以代表现实世界中的任何东西

- 在线平台的积分数字
- 游戏中的角色技能
- 六合彩
- 金融资产、像是股权、期权、债券
- 类似美元的法定货币
- 一盎司黄金
- 一份精美的画作
- 一个个性的签名
- 和更多...

## 什么是 ERC-20?

ERC-20 通证是区块链上的“某种东西”的代表。它们是可替换的，也就是说它们是可以互换的。你不用关心你有某种通证的哪一个，因为它们都是一样的，只需要关心你有多少个这种通证。这与不可替代的通证（NFTs）形成对比，后者是独特的，因此不能互换：你关心的是你拥有哪个通证，而不一定是多少个。

## 什么是 ERC-721?

ERC-721 token 标准开启了 NFT 热潮。它是同类产品中的第一个，因此也是创建这些独特 token 的最受欢迎的标准。NFT 历史悠久，但与 ERC-721 token 标准一起，它们只有在 CryptoKitties 项目中才真正走到了最前沿。

CryptoKitties 背后的公司 Dapper Labs 在 2017 年通过以太坊改进提案 (EIP) 推出了 ERC-721。CryptoKitties 是一组可收集的、随机生成的小猫，可以单独交易，类似于电子宠物或口袋妖怪。 每只 CryptoKitty 都是 100% 独一无二的——它们不能被复制，并且它们有交易历史，让公众确切地知道谁在它的整个生命周期内拥有这只小猫。

除了完全独特之外，以下是 ERC-721 的一些附加功能规范：

- 它允许您在账户之间转移 NFT，允许将 NFT 交易为其他货币。
- 它允许您识别网络上一组 NFT 的总供应量。
- 它允许您查询特定资产的所有者。

仅仅四年后，基于 ERC-721 的 NFT 就接管了加密生态系统。 项目范围从数以千万计的数字艺术品原始副本的区块链所有权，到已成为专属俱乐部的公共会员的独特头像，再到私人土地的部分所有权。

## 什么是 ERC-1155?

ERC-1155 token 标准由 Enjin 项目背后的团队开发，该项目专注于基于区块链的游戏解决方案。 Enjin 于 2019 年推出了 token 标准，它介于 ERC-20 标准和 ERC-721 标准之间。

Enjin 发现了一些与相对有限的 ERC-721 标准相关的挑战——特别是无法进行批量传输。

与 ERC-721 不同，如果要转移多个 NFT，每个 NFT 都需要单笔交易——因为每个 NFT 都由一个智能合约表示。这导致在铸造或交易单个 NFT 时交易成本过高。 ERC-1155 允许批量转移——单个智能合约上的多个资产——导致所有 token 一次转移，从而减少网络拥塞，从而降低 gas 成本。例如，当用户想将游戏中的一千件物品出售给另一个用户时，他或她可以使用 ERC-1155 的批量代币转移将它们一次全部发送 💸。

这个多 token 标准的另一个主要特点是它支持可替代和不可替代的 token——因为它能够支持多个状态——在同一个地址和合约上。实际上，这意味着您可以使用该地址上的可替代 token 进行游戏内支付，同时也可以转移独特的 NFT 资产。

ERC-1155 的另一个特点是它支持创建半同质 token。 SFT 作为可替代 token 进行交易，但一旦被赎回，它们就会转换为 NFT。例如，活动前的音乐会门票可能被视为可替代资产 - 任何门票都会为您提供相同的 GA 入场券。然而，演唱会结束后，门票就失去了可交易的价值，成为了一件独一无二的纪念品。 SFT 将这种类型的功能直接添加到票证本身的代码中。

最后，如果出现错误，可以恢复此标准上的 token 转移。在 ERC-721 标准中，如果资产被发送到错误的地址，您将无法收回资产。但是，ERC-1155 包含解决此问题的函数。安全传输功能和许多其他规则已到位以防止利用。

## ERC-721 和 ERC-1155

由于其附加功能，ERC-1155 token 标准在不久的将来可能会比 ERC-721 token 标准更加突出。 两者都允许你铸造新的 NFT，但有一些关键区别：

- ERC-1155 允许创建半同质 token 和非同质 token，而 ERC-721 只允许后者。
- 在 ERC-1155 中，智能合约链接到多个 URI，并且不存储额外的元数据（例如文件名）。 相比之下，ERC-721 仅支持直接存储在智能合约上的每个 token ID 的静态元数据，增加了部署成本并限制了灵活性。
- ERC-1155 的智能合约支持无限数量的 token，而 ERC-721 需要为每种类型的 token 创建一个新的智能合约。
- ERC-1155 还允许批量转移 token，可以减少交易成本和时间。 使用 ERC-721，如果你想发送多个令牌，它们会单独发生。

## 快速开始

#### ERC-20

您可以通过 openzeppelin 的合约 github 仓库作为基础，快速创建您的 ERC-20token.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.2;
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
contract testCoin is ERC20 {
    constructor() ERC20("testCoin", "tCoin") {
        _mint(msg.sender, 1000 * 10 ** decimals());
    }
}
```

#### ERC-721

您可以通过 openzeppelin 的合约 github 仓库作为基础，快速创建您的 ERC-721 token.

您可以参考 openzeppelin 提供的官方文档来完成这一步骤：[https://docs.openzeppelin.com/contracts/3.x/erc721](https://docs.openzeppelin.com/contracts/3.x/erc721).

#### ERC-1155

您可以通过 openzeppelin 的合约 github 仓库作为基础，快速创建您的 ERC-1155 token.

您可以参考 openzeppelin 提供的官方文档来完成这一步骤：[https://docs.openzeppelin.com/contracts/3.x/erc1155](https://docs.openzeppelin.com/contracts/3.x/erc1155).

## 需要帮助推广？

我们欢迎您随时联系我们 Discord，来向我们讲述您的 Token，我们会将我们认可的 token 发布在文档中。合作共赢。
