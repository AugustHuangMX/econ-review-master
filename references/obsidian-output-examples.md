# Obsidian Output Examples

Read this file only when examples are needed for formatting review notes. Keep the final user artifact concise and source-grounded.

## Fully Annotated Definition

```markdown
> [!definition] 边缘概率质量函数 (Marginal pmf)
> $p_X(j) = \sum_k p_{X,Y}(j,k)$。
> 表格题通常是“沿列求 $p_X$，沿行求 $p_Y$”。`Lec 3 课件页 20-25｜推荐练习：PS3 Q2`

> [!intuition] 经济学直觉
> 边缘分布是在忽略另一个变量后的分布。对所有可能的 $k$ 求和，就是把 $Y$ 的信息积掉，只保留 $X$ 本身的不确定性。
```

## Formula With Technique

```markdown
> [!formula] 矩形区域概率公式
> $$P(x_1 < X \le x_2,\; y_1 < Y \le y_2) = F(x_2,y_2) - F(x_2,y_1) - F(x_1,y_2) + F(x_1,y_1)$$
> 条件：$F$ 是联合 CDF，且矩形边界按 inclusion-exclusion 处理。`Lec 4 课件页 39-42｜推荐练习：PS3 Q4, Exam 2023 Q3a`

> [!intuition] 经济学直觉
> 先取右上角累积概率，再扣掉左边和下边多算的区域；左下角被扣了两次，所以要加回来。

> [!technique] 解题技巧
> 连续题先画支撑区域 (support region)，再写积分上下限；不要一上来就列积分。`Lec 4 课件页 51-56`
```

## Model Block

```markdown
### 拍卖中的激励相容 (Incentive Compatibility in Auctions)

> [!definition] 激励相容 (Incentive Compatibility, IC)
> 一个机制满足 IC，当且仅当对每个参与者 $i$ 和每个类型 $t_i$，真实报告 $t_i$ 至少和任何虚假报告 $t_i'$ 一样好。`Lec 6 课件页 34-38｜推荐练习：PS2 Q3, Exam 2023 Q1b`

> [!intuition] 经济学直觉
> 如果说谎能系统性带来更高效用，理性参与者就会说谎。IC 的作用是把“诚实”设计成最优策略，而不是依赖道德或外部强制。

> [!technique] 解题技巧
> 验证 IC 时，先写出不同类型下的期望效用，再比较真实报告和偏离报告；机制设计题通常还要同时检查 IR。`Lec 6 课件页 40-42｜推荐练习：PS2 Q3`
```

## Roadmap Session

```markdown
### Day 2 — Incentive Compatibility and IR

- `Goal`: 能在 25 分钟内判断机制是否满足 IC/IR，并写出标准证明结构。
- `Start from questions`: 先做 PS2 Q3 和 Exam 2023 Q1b，不看课件。
- `Return to notes`: 回到 `Lec 6 课件页 34-42` 修补 IC/IR 定义、效用比较和偏离条件。
- `Fix the gap`: 如果卡在 IC 约束，重写 truth-telling vs deviation 的效用差；如果卡在 IR，标出 outside option。
- `Output`: 一页 answer skeleton，加一条 error log，记录最容易漏写的约束。
```

## Outline Refinement Pattern

```markdown
## Topic: Auctions and Mechanism Design

### Start from questions
- PS2 Q3: verify IC and IR for a direct mechanism.
- Exam 2023 Q1b: derive payment rule from allocation monotonicity.

### Return to lecture concepts
- 激励相容 (Incentive Compatibility, IC): truthful reporting must weakly dominate every deviation. `Lec 6 课件页 34-38｜推荐练习：PS2 Q3, Exam 2023 Q1b`
- 个体理性 (Individual Rationality, IR): participation value must exceed outside option. `Lec 6 课件页 39-42｜推荐练习：PS2 Q3`
```
