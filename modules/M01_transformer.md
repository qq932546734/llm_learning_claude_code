# M01: Transformer 架构深度解析

> Canonical 模块编号口径见 `docs/taxonomy.md`。本模块对应 README 的 `M01`。

## 为什么学
- 这是后续预训练、推理优化、对齐和部署的共同前置。
- 面试中高频考点集中在公式完整性、结构顺序、复杂度来源和设计动机。

## 前置依赖
- 线性代数基础：矩阵乘法、向量内积、维度检查
- 神经网络基础：MLP、残差连接、归一化

## 诊断题
1. Transformer 相比 LSTM 的核心优势有哪些？至少说 3 点。
2. Self-Attention 的 Q/K/V 分别代表什么？完整公式是什么？
3. 为什么需要位置编码？绝对 vs 相对位置编码差异是什么？
4. 一个标准 decoder-only Transformer block 按顺序有哪些子层？
5. Attention 的时间/空间复杂度为什么是 `O(n^2)`？瓶颈在哪里？

## 核心知识点
- `核心必会`：Scaled Dot-Product Attention 的数学形式、维度检查、mask 与 softmax 的作用。
- `核心必会`：Multi-Head Attention 的作用是多子空间表征，不是节省计算。
- `核心必会`：位置编码解决置换不变性，RoPE / ALiBi 在外推与工程表现上不同。
- `工程重点`：Pre-LN / Post-LN 影响梯度流动、训练稳定性与深层可训练性。
- `工程重点`：FFN 是 token-wise 非线性变换，宽度与激活函数会影响容量和效率。
- `扩展阅读`：Mini-GPT 可作为 M01-06 的实现出口，与 M12 的 KV cache 估算练习形成连接。

## 易错点 / 边界条件
- 容易漏写 Attention 完整公式中的 softmax 和 mask。
- 容易把 MHA 的表征收益与 MQA/GQA 的推理收益混为一谈。
- 容易知道 Pre-LN 更稳，但说不清它如何改善梯度流动。

## 练习
- [ ] 用 NumPy 实现一个简化版 Self-Attention，包含 causal mask。
- [ ] 写出 decoder-only block 的完整顺序，并解释 residual / LN 的位置。
- [ ] 估算序列长度从 2k 增加到 8k 时 self-attention 主要复杂度如何变化。

### 学习产物
- 1 页总结：Attention 公式、位置编码、Pre-LN / Post-LN。
- 1 组错题：至少记录 3 个最容易漏掉的公式或结构细节。
- 1 个练习产物：实现题、估算题、口述题三选一。

## 费曼输出
- 用不超过 200 字，向一个懂编程但不了解 NLP 的朋友解释 Transformer 的核心思想。
- 用 90 秒口述：为什么 Pre-LN 通常比 Post-LN 更稳定？

## 面试高频问法
### 问法 1
问题：为什么 Attention 要除以 `sqrt(d_k)`？
- 一句话答案：避免点积方差随维度增大而变大，导致 softmax 饱和和梯度变差。
- 展开框架：点积统计量 -> softmax 饱和 -> 梯度问题 -> 缩放作用。
- 常见追问点：如果不除会怎样？为什么不是除以 `d_k`？

### 问法 2
问题：Pre-LN 和 Post-LN 的核心差异是什么？
- 一句话答案：区别在于 LN 相对 residual / sub-layer 的位置，直接影响梯度流动和训练稳定性。
- 展开框架：结构位置 -> 梯度路径 -> 深层训练稳定性 -> 当前主流选择。
- 常见追问点：原始 Transformer 为什么用 Post-LN？Pre-LN 有什么代价？

## 完成标准
- 诊断或复习题正确率达到 80%。
- 完成 1 次费曼输出。
- 完成 1 个练习。
- 能独立复述 Attention 完整公式和 LayerNorm 动机。

## 后续关联
- 与 `M04` 相连：高效注意力变体建立在 M01 的公式和数据流理解之上。
- 与 `M12` 相连：KV cache、prefill/decode、推理指标都要求先理解 block 内部结构。
