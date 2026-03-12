# M02: 预训练理论与方法

> Canonical 模块编号口径见 `docs/taxonomy.md`。本模块对应 README 的 `M02`。

## 为什么学
- 预训练决定模型的基础能力边界，是 tokenizer、优化、分布式训练的上游。
- 面试中常考目标函数差异、decoder-only 主流原因、AdamW 和训练稳定性。

## 前置依赖
- M01 Transformer 基础
- 损失函数、梯度下降、基本优化器概念

## 诊断题
1. CLM / MLM / Span Corruption 分别在优化什么？各自优劣是什么？
2. 为什么 decoder-only 适合统一“生成式”任务？
3. AdamW 相比 Adam 的关键差异是什么？
4. 训练中出现 loss spike / NaN，你会先排查哪些变量？

## 核心知识点
- `核心必会`：GPT / BERT / T5 三类训练目标与架构的关系。
- `核心必会`：decoder-only 成为主流，与任务统一性、效率和扩展规律有关。
- `工程重点`：warmup、梯度裁剪、loss scaling、混合精度、检查点策略。
- `工程重点`：AdamW 的 decoupled weight decay 与训练稳定性。
- `扩展阅读`：Kaplan / Chinchilla scaling laws 与算力最优训练。

## 易错点 / 边界条件
- 容易把“预训练学知识”和“微调改行为”混成同一层。
- 容易把 L2 正则和 AdamW 的 weight decay 说成完全等价。
- 容易知道 Chinchilla 结论，却说不清“算力预算固定”的前提。

## 练习
- [ ] 给定 batch / seq / hidden / 层数，估算 activation 与 optimizer state 的主导项。
- [ ] 用一句话解释 Chinchilla 的核心结论，并举例其工程意义。
- [ ] 解释为什么当前主流 LLM 多为 decoder-only。

## 费曼输出
- 用自己的话解释：为什么“数据决定上限，训练决定下限”在预训练阶段经常成立？

## 完成标准
- 诊断题正确率达到 80%。
- 完成 1 次费曼输出。
- 完成 1 个估算或解释型练习。
- 能清楚区分 CLM / MLM / Span Corruption 与 AdamW / L2 正则。

## 后续关联
- 与 `M03` 相连：tokenizer 与数据流水线共同决定预训练输入分布。
- 与 `M06` 相连：预训练成本最终落到并行与资源切分上。
