# 学习日志（History）

> 本文件存放历史学习记录；当前状态面板统一查看 `docs/progress.md`。

## 2026-03-17
- 模块：`M10` 解码策略
- 学习内容：失败模式与调参顺序第二轮、重复/过长/发散/模板化的排查框架、stop sequence vs max tokens、temperature 与 top-p 的分工、聊天/代码/摘要/事实问答四类任务的默认解码风格
- 诊断表现：已能稳定说出“temperature 控制探索强度，top-p 控制探索边界”；能区分 stop sequence 的边界触发与 max tokens 的长度硬上限；能按任务目标解释四类任务的默认解码风格。当前仍需继续压稳“重复 + 过长但不跑题”时先动 repetition penalty 而不是先动温度
- 提问：无新增提问（本次以诊断题口述与纠偏为主）
- 模块：`M03` 分词与表示
- 学习内容：WordPiece“似然导向训练准则”与 Unigram“显式概率模型”短复习、tokenizer 对 prefill / decode 成本影响的标准口径
- 诊断表现：已能说清 prefill 看序列长度、decode 看输出层 / 词表大小 / 带宽；WordPiece 与 Unigram 的主干差异已通，但标准表述自然度仍需再压 1 次
- 提问：无新增提问（本次以短复习口述为主）
- 模块：`M05` 长文本建模
- 学习内容：系统层 / 表示层 / 方案层三层框架，`RAG` vs 原生长上下文的本质区别，原生扩窗 / 稀疏注意力 / 压缩记忆 / `RAG` 四条路线的失败模式，企业知识库问答与超长合同审阅两个场景的选型训练，120 字费曼收束
- 诊断表现：已能说清长文本问题不只是位置编码问题，而是系统成本、表示外推和方案权衡的叠加；能区分 `RAG` 的“先筛再读”与长上下文的“少筛直接读”；当前仍需继续压稳两点：一是回答中少用绝对化表述，二是“如果只能给一个统一方案，会牺牲什么”的面试口径
- 提问：无新增提问（本次以临时插学、口述训练与纠偏为主）

## 2026-03-16
- 模块：`M10` 解码策略
- 学习内容：greedy / temperature / top-k / top-p、beam search 与 length penalty、repetition penalty / stop sequence / max tokens、beam 与 sampling 的任务边界、失败模式与调参、按任务反推默认参数
- 诊断表现：已能解释“模型给分布，解码把分布变成输出”；能区分采样控制项和工程约束项；能说明 beam search 不只是更贵，也更偏保守与模板化；已建立重复/发散/过短/过保守的第一轮调参映射；当前仍需继续压稳“多现象并存时的排查顺序”与聊天/代码/摘要的参数选型直觉
- 提问：Q045-Q062
- 模块：`M10` 解码策略
- 学习内容：beam search 为什么不适合开放式生成、重复/模板化/过长场景下的排查顺序、temperature 调高后与 top-p 的联动
- 诊断表现：已能口述“更贵 + 更保守 + 更模板化”的 beam 边界，也能在“先保留多样性，再收尾部风险”的框架下解释 temperature 与 top-p 的联动；下一步需要继续训练多参数同时变化时的排查顺序
- 提问：Q063-Q066
- 模块：`M03` 分词与表示
- 学习内容：BPE / WordPiece / Unigram 对比复习、WordPiece 中“似然收益”与概率口径、Unigram 的显式概率模型直觉、SentencePiece 的层次边界
- 诊断表现：三者主干差异已能口述；WordPiece vs Unigram 的区别明显更清楚；当前仍需继续压稳“概率、条件概率、似然”三者的层次，以及为什么 WordPiece 不应被想成每步都训练完整语言模型
- 提问：Q067-Q073
- 模块：`M07` 指令微调
- 学习内容：SFT 副作用根源短复习
- 诊断表现：仍需继续压稳“窄分布 + 强监督约束”，避免简化成“继续训练导致遗忘”
- 提问：无新增提问

## 2026-03-15
- 模块：`M07` 指令微调
- 学习内容：少量高质量 SFT 数据为什么有效、SFT 副作用与根源、LoRA 的显存收益与低秩边界
- 诊断表现：已能说明 SFT 不是从零训练、主要改变行为分布；LoRA 省显存的主因较稳；SFT 副作用的根源仍容易简化成“继续训练导致遗忘”，还需压稳“窄分布 + 强监督约束”
- 提问：无新增提问（本次以口述复测为主）
- 模块：`M03` 分词与表示
- 学习内容：大 vocab 与短序列的权衡、tokenizer 为什么同时影响 prefill 与 decode、BPE/WordPiece/Unigram 的训练目标差异
- 诊断表现：已能把“prefill 看序列长度、decode 看词表大小”讲清；BPE 与 Unigram 基本稳定；WordPiece 的“似然收益驱动”表述还需继续压稳
- 提问：无新增提问（本次以口述复测为主）
- 补充：完成了 1 次“3 分钟快复盘”，将昨日主线收束为 4 句记忆钩子

## 2026-03-12
- 模块：`M07` 指令微调
- 学习内容：SFT 改变行为分布、少量高质量数据为何有效、SFT 副作用、LoRA 低秩增量、客服助手 SFT 数据样例设计
- 诊断表现：已能区分“行为变化”与“知识增加”；能设计客服场景下的澄清、拒答、负面情绪样本；SFT 副作用的口述还可再压稳
- 提问：Q033-Q035
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
