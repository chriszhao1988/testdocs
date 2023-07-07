# 通用供应框架

### 步骤 1：多少 `$UNIT` 代币？

首先，Treasurenet 会将实际的 RWA 产量率与由 DAO 治理模块设定的目标率进行比较。

实际的实物资产产量率与目标率相比如何呢？
根据实际率和目标率的差异，减少区块奖励。

随后，会有 3 种常见的情况：

无法达到目标率 - 区块奖励减少 10%到 50%，具体取决于差异的大小
达到目标率 - 区块奖励减少 10%
超过目标率 - 区块奖励减少 1%到 10%，具体取决于差异的大小
总供应量：

UNIT 代币的供应量可能在 7 亿到 8 亿之间。

这个估计是基于以下几个突出的假设。然而，理解未来实物资产产量的实际数量将决定结果是至关重要的。具体来说，更多的 RWA 产量将导致 UNIT 供应量的增加，反之亦然。

| 主要假设                | 值                       | 描述                                                                 |
| ----------------------- | ------------------------ | -------------------------------------------------------------------- |
| 周期                    | `30,000,000`区块         | 每个周期大约是 1 年                                                  |
| 初始区块奖励            | `10 UNIT/区块`           | 对于初始的 2 个周期，区块奖励保持恒定，为 RWA 生态系统的建设提供时间 |
| 目标率 (对于 RWA 产量)  | `10%`                    | 周期性 RWA 产量增长率的默认目标率                                    |
| 最大区块奖励减少        | `50%`                    | 较低的边缘情况；如果没有 RWA 产出，区块奖励将大幅度减少 50%          |
| 最小区块奖励减少        | `1%`                     | 较高的边缘情况；如果 RWA 增长率超过 1,000%，区块奖励仅减少 1%        |
| 默认区块奖励减少        | `10%`                    | 默认减少；如果 RWA 增长率等于目标率，区块奖励减少 10%                |
| 未来 RWA 产量增长率分布 | PERT [`-50%, 15%, 500%`] | 预测 RWA 产量增长率是困难的，                                        |

我们假设前 3 个周期的增长率为`500%`，因为我们发展了更多的 RWA 连接。

然后，稳定状态的增长率被建模为 PERT 分布，
定义为`50%`是最低预期率，`15%`是预期率，`500%`是最高预期率。

在模拟 500 个周期后，UNIT 供应量可能会呈现出以下的分布。要获取完整的细节，请密切关注后续的发布。

![Expected_supply](/img/docs/expected_supply.png)

### 步骤 2：谁能赚取 `$UNIT`？

在确定了总的区块奖励后，每个区块奖励将被颁发给活跃的验证节点和活跃的超级验证节点。

|        | 活跃验证节点 | 活跃超级验证节点                         |
| ------ | ------------ | ---------------------------------------- |
| Apple  | 红色         | 美国                                     |
| Action | 抵押 `$UNIT` | -抵押 `$UNIT` -出价 `$TAT` (销毁 `$TAT`) |
| Reward | 基础奖励     | 基础奖励；超级验证者奖励                 |

`$UNIT`持有者可以将`$UNIT`抵押到任何节点中，以按比例分享基础奖励。$`$TAT`持有者也可以出价$`$TAT`，以按比例分享超级验证者奖励，这就是在核心概念中描述的奖金抵押。

从长远来看，我们估计超级验证者奖励将占区块奖励的大约 30%。
超级验证者奖励的幅度取决于各个节点之间的$`$TAT`竞标有多激烈，以及有多少超级验证者。详情将在未来的发布中进一步描述。