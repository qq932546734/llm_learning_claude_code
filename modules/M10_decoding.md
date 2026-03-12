# M10: 解码策略

## 为什么学
- 解码不是“最后一层小技巧”，而是直接影响回答质量、稳定性和吞吐的策略层。

## 前置依赖
- M01 Attention 与概率输出直觉
- M12 推理效率基础

## 诊断题
1. top-p 与 top-k 的核心差异是什么？为什么 top-p 常更稳？
2. beam search 为什么可能更“重复/啰嗦”？
3. speculative decoding 在什么条件下收益最大？

## 核心知识点
- `核心必会`：贪心 / beam / sampling 的适用场景与失败模式。
- `核心必会`：temperature / top-k / top-p 如何改变分布形状和截断方式。
- `工程重点`：speculative decoding 依赖 acceptance rate 与 draft 成本。

## 易错点 / 边界条件
- 容易把 beam search 误解为“更高级，所以总更好”。
- 容易把 speculative decoding 当成纯算法技巧，忽略 acceptance rate 前提。

## 练习
- [ ] 设计题：给一个客服场景和一个创意写作场景，分别选解码参数并说明原因。

## 费曼输出
- 用 90 秒解释：top-k 和 top-p 本质上在控制什么？

## 完成标准
- 诊断题正确率达到 80%。
- 完成 1 次费曼输出。
- 完成 1 个参数设计题。

## 后续关联
- 与 `M12` 相连：speculative decoding 会在部署时体现为延迟与吞吐权衡。
