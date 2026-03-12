# M04: 高效注意力变体

> 本模块聚焦 Attention 的计算/内存/带宽瓶颈与主流变体设计。

## 为什么学
- 这是从“会 Attention”走向“会解释系统性能”的关键模块。
- 面试和工程讨论里，高效注意力常用于区分是否真正理解瓶颈来源。

## 前置依赖
- M01 Attention / Multi-Head Attention
- 基本显存、带宽、复杂度直觉

## 诊断题
1. 标准 Attention 的瓶颈主要是什么？在训练 vs 推理分别如何体现？
2. MQA/GQA 相比 MHA 省的是什么（计算/显存/带宽）？
3. FlashAttention 为什么能更快？它避免了哪类内存读写？

## 核心知识点
- 稀疏注意力 / 线性注意力：以近似换复杂度
- MQA/GQA：减少 KV heads，降低 KV cache 与带宽
- FlashAttention：分块 + 在线 softmax + 只保留需要的统计量

## 易错点 / 边界条件
- 容易把 MHA 的表征收益和 MQA/GQA 的推理收益混在一起。
- 容易只说 FlashAttention “更省显存”，却说不清它省的是哪类中间矩阵读写。
- 容易把所有高效注意力都归类成“降复杂度”，但 FlashAttention 更像 IO 优化。

## 练习
- [ ] 给定 `n_heads` 与 `n_kv_heads`，估算 KV cache 节省比例
- [ ] 设计题：训练和推理各选一种高效注意力方案，并说明你的瓶颈依据。

### 学习产物
- 1 页总结：Sparse / Linear / MQA-GQA / FlashAttention 的优化对象。
- 1 组错题：至少记录 3 个“不是在优化同一瓶颈”的对比点。
- 1 个练习产物：KV cache 节省估算或方案选型说明。

## 费曼输出
用 150 字解释：FlashAttention 和 Sparse Attention 解决的是同一个问题吗？

## 面试高频问法
### 问法 1
问题：MQA/GQA 为什么能提升推理性能？
- 一句话答案：它们通过减少 KV heads 降低 KV cache 和历史 KV 读取带宽，而不是降低多头计算本身。
- 展开框架：MHA 的 KV 形状 -> MQA/GQA 的共享方式 -> decode 阶段的读写瓶颈。
- 常见追问点：为什么训练阶段收益不如推理阶段明显？会损失什么能力？

### 问法 2
问题：FlashAttention 快在哪？
- 一句话答案：快在减少 HBM 读写，而不是改变 Attention 数学结果。
- 展开框架：标准实现的中间矩阵 -> 分块与在线 softmax -> IO-aware 优化。
- 常见追问点：为什么反向传播仍然正确？它和 Sparse Attention 的目标一样吗？

## 完成标准
- 诊断题正确率达到 80%。
- 完成 1 次费曼输出。
- 完成 1 道估算题或设计题。
- 能独立解释 MQA/GQA 与 FlashAttention 分别优化的瓶颈。

## 后续关联
- 与 `M05` 相连：长文本建模常借助高效注意力或上下文压缩。
- 与 `M12` 相连：推理优化直接建立在 MQA/GQA、FlashAttention、KV 形态理解上。
