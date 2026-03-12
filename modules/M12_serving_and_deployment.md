# M12: 生产部署与推理优化

> Canonical 模块编号口径见 `docs/taxonomy.md`。本模块对应 README 的 `M12`。

## 为什么学
- 这是把“模型能跑”变成“服务可用、成本可控、指标稳定”的关键模块。
- 你已经学过 `M12-01`，这个模块很适合做“复习闭环 + 面试输出”的样板。

## 前置依赖
- M01 Transformer
- M04 高效注意力
- M06 资源与并行直觉

## 诊断题
1. prefill 和 decode 的瓶颈为什么通常不同？
2. KV cache 为什么缓存 K/V 而不缓存历史 Q？
3. continuous batching 和 Paged KV 分别解决什么问题？

## 核心知识点
- `核心必会`：prefill vs decode 的复杂度和资源瓶颈。
- `核心必会`：KV cache 的形状、读写路径、显存主导项。
- `工程重点`：continuous batching、Paged KV、chunked prefill 的调度与内存作用。
- `工程重点`：speculative decoding、KV 量化、TTFT / TPOT / token/s 指标。

## 易错点 / 边界条件
- 容易把 prefill 和 decode 当成同类计算负载。
- 容易知道缓存 K/V，却说不清 decode 每步为什么还会被读 KV 带宽卡住。
- 容易把 Paged KV 当成“纯加速技巧”，忽略它首先解决的是内存管理与碎片问题。

## 练习
- [ ] 从 `config.json` 读懂一个模型，并估算 `seq_len=4096, dtype=FP16` 时 KV cache 量级。
- [ ] 设计题：为一个高并发聊天服务解释为什么需要 continuous batching + Paged KV。
- [ ] 指标题：分别说明 TTFT、TPOT、token/s 更接近用户体验还是系统吞吐。

### 学习产物
- 1 页总结：prefill / decode、KV cache、batching、量化、指标。
- 1 组错题：至少记录 3 个容易混淆的系统瓶颈或指标口径。
- 1 个练习产物：KV cache 估算表、服务调度设计说明或指标解释卡片。

## 费曼输出
- 用 2 分钟解释：为什么 decode 常常比 prefill 更容易被带宽卡住？

## 面试高频问法
### 问法 1
问题：KV cache 为什么能加速推理？为什么不缓存历史 Q？
- 一句话答案：因为 decode 每步只需要当前 query，但要反复与历史 K/V 交互，所以复用 K/V 才有收益。
- 展开框架：训练 vs decode -> 当前步需要什么 -> 历史 K/V 如何复用 -> 读写路径。
- 常见追问点：KV cache 的显存复杂度是什么？什么时候 cache 会成为瓶颈？

### 问法 2
问题：continuous batching 和 Paged KV 的关系是什么？
- 一句话答案：continuous batching 提高槽位利用率，Paged KV 提供能支撑它的内存管理机制。
- 展开框架：固定 batch 的空槽问题 -> 请求动态进出 -> block table / 块池 -> 避免扩容 memcpy。
- 常见追问点：chunked prefill 为什么也重要？block size 过小有什么代价？

## 完成标准
- 诊断题正确率达到 80%。
- 完成 1 次费曼输出。
- 完成 1 道 KV cache 估算题或推理调度设计题。
- 能独立解释 TTFT / TPOT / token/s 与 KV cache / Paged KV 的关系。

## 后续关联
- 与 `M10` 相连：解码策略会转化为部署层的延迟与吞吐取舍。
- 与 `M05` 相连：长上下文的系统成本最终落在部署与资源管理上。
