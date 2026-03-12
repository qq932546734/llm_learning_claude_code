# 学习日志（History）

> 本文件存放历史学习记录；当前状态面板统一查看 `docs/progress.md`。

## 2026-03-12
- 模块：`M03` 分词与表示
- 学习内容：subword trade-off、BPE/WordPiece/Unigram、embedding 参数量、tied embeddings、tokenizer 对 serving 成本的影响、中英混合代码 tokenizer 设计维度
- 诊断表现：能把 vocab size、序列长度、prefill/decode、KV cache 串起来；WordPiece 的目标表述仍需再压稳
- 提问：Q030-Q032
- 模块：`M12-01` 推理优化（Prefill vs Decode）
- 学习内容：prefill/decode 复杂度、KV cache、continuous batching、Paged KV、chunked prefill、speculative decoding、KV 量化
- 诊断表现：能解释 prefill/decode 不同瓶颈；能估算 batching 利用率；能区分 PyTorch batch 与 kernel 调度 batch
- 提问：Q018-Q029

## 2026-03-11
- 模块：`M08-01` DPO 稳定性与偏差分析
- 学习内容：beta 取值、长度偏置、数据构造优先级、偏短/啰嗦问题
- 诊断表现：能提出长度匹配和信息密度对比两条数据构造规则
- 提问：Q017

## 2026-03-10
- 模块：`M08-01` RLHF 基础
- 学习内容：SFT → RM → PPO/DPO、Bradley-Terry、Advantage、PPO 训练循环、DPO 原理与练习
- 诊断表现：PPO 四模型、DPO 隐式奖励、margin 边界理解稳定
- 提问：Q011-Q016

## 2026-03-07
- 模块：`M01-03`、`M02-01`、`M06-01`
- 学习内容：位置编码、预训练基础、分布式训练与 ZeRO
- 诊断表现：RoPE/ALiBi、AdamW、ZeRO 三阶段关系掌握良好
- 提问：Q006-Q010

## 2026-03-06
- 模块：`M01-01`、`M01-05`、`M04`、`M01-06`
- 学习内容：Attention 回顾、Pre-LN/Post-LN、MQA/GQA、FlashAttention、Mini-GPT 实战引入
- 诊断表现：Attention 公式与多头计算量有过易错点；位置编码与复杂度分析表现较好
- 提问：Q001-Q005
