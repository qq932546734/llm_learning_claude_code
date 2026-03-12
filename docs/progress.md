# 学习进度追踪

> 更新日期: 2026-03-12
> 当前状态面板；历史记录见 `docs/learning_journal.md`。

## 当前模块
- 当前学习：[`M03 分词与表示`](../modules/M03_tokenization_and_representation.md)
- 当前层级：L2.5（理解层偏应用）
- 当前目标：把 tokenization 与 embedding 从“知道术语”推进到“能做取舍与估算”
- 推荐产物：1 页总结 + 1 组错题/易错点 + 1 个参数量/切分对比练习
- 本次进展：已完成诊断题、1 次参数量估算、1 次 tokenizer 对 serving 成本的串联复习、1 次费曼输出草稿

## 已完成模块
| 模块 | 状态 | 完成日期 | 备注 |
|------|------|----------|------|
| [M01-01 Attention机制回顾](../modules/M01_transformer.md) | ✅ | 2026-03-06 | softmax 与 mask 需回访 |
| [M01-03 位置编码](../modules/M01_transformer.md) | ✅ | 2026-03-07 | 已掌握，可抽查 |
| [M01-05 LayerNorm与架构演进](../modules/M01_transformer.md) | ✅ | 2026-03-06 | 原理已通，需口述回访 |
| [M04 高效Attention变体](../modules/M04_efficient_attention.md) | ✅ | 2026-03-06 | 工程理解较强 |
| [M01-06 Mini-GPT](../modules/M01_transformer.md) | ✅ | 2026-03-06 | 偏概念引入，后续可补代码 |
| [M02-01 预训练基础](../modules/M02_pretraining.md) | ✅ | 2026-03-07 | 与 M03/M06 关联紧密 |
| [M06-01 分布式训练](../modules/M06_parallelism_and_efficiency.md) | ✅ | 2026-03-07 | ZeRO/FSDP 可继续强化 |
| [M08-01 RLHF基础](../modules/M08_rlhf.md) | ✅ | 2026-03-10 | DPO 边界问题理解较好 |
| [M12-01 推理优化](../modules/M12_serving_and_deployment.md) | ✅ | 2026-03-12 | 推理调度/带宽理解较好 |

## 本周薄弱点
| 知识点 | 所属模块 | 状态 | 触发原因 |
|--------|----------|------|----------|
| Attention 完整公式（softmax/mask） | M01 | 会但不稳 | 早期遗漏，需隔周抽查 |
| 多头注意力 vs MQA/GQA 的“省什么” | M04 | 会但不稳 | 易把表征收益和推理收益混淆 |
| Transformer 为什么用 LayerNorm | M01 | 待回访 | 已学过，但适合口述重建 |
| ZeRO/FSDP 选型直觉 | M06 | 待回访 | 面试/工程都常追问 |
| tokenizer 对参数量/带宽影响 | M03 | 新学 | 当前主线内容 |
| BPE / WordPiece / Unigram 目标差异 | M03 | 会但不稳 | WordPiece 口径仍需再压稳 |

## 待复习项
| 优先级 | 模块 | 状态 | 建议动作 |
|--------|------|------|----------|
| P1 | M03 | 新学 | 24 小时内做 3 题诊断 + 1 次费曼输出 |
| P1 | M03 | 会但不稳 | 48 小时内补 1 次 tokenizer 对比表口述，压稳 WordPiece / Unigram |
| P1 | M12 | 会但不稳 | 3 天内抽查 TTFT/TPOT/KV cache/Paged KV |
| P2 | M08 | 已掌握 | 7 天内抽查 DPO margin、beta、长度偏置 |
| P2 | M06 | 待回访 | 7 天内复述 ZeRO Stage 1/2/3 与 FSDP |
| P3 | M01 | 待回访 | 用 2 分钟口述 Attention 公式与 Pre-LN 动机 |

## 下一步建议
1. 完成 `M03` 的 tokenizer 对比表复述，重点压稳 WordPiece 与 Unigram 的目标差异。
2. 做一次 `M12` 短复习，继续抽查 TTFT/TPOT/KV cache/Paged KV。
3. 补一题“中英混合代码模型 tokenizer 设计题”，把工程判断标准再说熟。

## 学习统计
- 已完成重点模块：9 个
- 当前进行中模块：1 个
- 最后学习日期：2026-03-12
- 学习日志入口：`docs/learning_journal.md`
