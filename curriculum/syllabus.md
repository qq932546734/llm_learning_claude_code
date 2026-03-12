# LLM 学习课程大纲（Syllabus Track）

> 版本: 1.0 | 更新日期: 2026-03-06
> 本大纲遵循「先广度后深度」原则，先建立完整知识地图，再按需深入

---

> 说明：本文件是“学习路径叙事线”，编号统一使用 `S01` ~ `S16`，避免与 canonical 课程模块 `M01` ~ `M16` 冲突（见 `docs/taxonomy.md`）。

## 第一阶段：基础重塑 (Foundation)

### S01: 神经网络回顾与重塑
**目标**: 确保基础扎实，统一术语体系
- 前馈网络、反向传播的完整推导
- 激活函数的本质与选择逻辑
- 梯度消失/爆炸的现代解决方案
- **诊断点**: BatchNorm vs LayerNorm 的数学差异与使用场景

### S02: 表示学习与嵌入空间
**目标**: 理解"嵌入"的数学本质
- One-hot 到 Dense Vector 的演进逻辑
- 词嵌入 (Word2Vec, GloVe) 的统计学习本质
- 嵌入空间的代数性质与语义映射
- **诊断点**: 为什么 Word2Vec 的类比性质成立？cosine相似度的理论依据？

### S03: 序列模型演进史
**目标**: 理解RNN到Transformer的必然性
- RNN/LSTM/GRU 的局限与门控机制设计思想
- Attention 机制的直觉与数学形式
- Seq2Seq + Attention 作为 Transformer 的前夜
- **诊断点**: LSTM的门控为什么那样设计？Attention权重的归一化目的是什么？

---

## 第二阶段：Transformer 核心 (Core)

### S04: Transformer 架构全解
**目标**: 完整掌握Transformer的每个组件
- Self-Attention: 从Q,K,V定义到矩阵并行计算
- Multi-Head Attention: 子空间分割的本质
- Position Encoding: 绝对vs相对位置，RoPE深度解析
- FFN: 隐层维度的设计逻辑
- LayerNorm + Residual: 训练稳定性的基石
- **诊断点**: 为什么需要√d_k缩放？Multi-Head的concat和线性变换顺序重要吗？

### S05: 训练策略与优化
**目标**: 理解大模型训练的技术细节
- Warmup + Cosine Decay 的数学原理
- 梯度裁剪、混合精度训练
- 分布式训练基础: DP, DDP, ZeRO
- **诊断点**: 为什么Transformer需要warmup？Adam的β参数如何影响训练？

---

## 第三阶段：预训练与规模化 (Pre-training)

### S06: 预训练任务设计
**目标**: 理解为什么这些任务有效
- 语言建模: Autoregressive vs Masked
- GPT系列: 从左到右的因果建模
- BERT系列: MLM + NSP 的设计与废弃
- T5: Span Corruption 的通用性
- **诊断点**: 为什么GPT不能双向？MLM的缺点是啥？

### S07: 数据工程与Tokenization
**目标**: 数据决定上限，掌握数据流水线
- Tokenization演进: BPE, WordPiece, SentencePiece, Unigram
- 数据清洗与去重策略
- 数据配比与课程学习
- **诊断点**: BPE贪心算法的次优性？多语言tokenizer的挑战？

### S08: 模型缩放定律 (Scaling Laws)
**目标**: 理解"大力出奇迹"的科学基础
- Kaplan vs Chinchilla  scaling laws
- 计算最优训练的权衡
- 涌现能力的争议与解释
- **诊断点**: Chinchilla-optimal的计算公式？涌现是真实的还是度量的产物？

---

## 第四阶段：对齐与微调 (Alignment)

### S09: 指令微调 (Instruction Tuning)
**目标**: 从预训练模型到可用助手
- 指令数据的构建与多样性
- 多轮对话的格式化与处理
- 灾难性遗忘与缓解策略
- **诊断点**: 指令微调改变的是什么？为什么少量数据就能有效？

### S10: RLHF 与偏好优化
**目标**: 深度理解人类反馈强化学习
- 奖励模型: 从偏好到标量
- PPO: 策略梯度在LLM中的应用
- DPO: 直接偏好优化的 elegance
- RLHF的局限与替代方案 (KTO, IPO)
- **诊断点**: RM的 Bradley-Terry 假设？DPO vs PPO的优劣？

### S11: 对齐的科学 (The Science of Alignment)
**目标**: 理解对齐的本质问题
- 有用性vs无害性权衡
- 奖励黑客与Gaming
- Superalignment 与可扩展监督
- **诊断点**: RLHF真的对齐了吗？Sycophancy问题根源？

---

## 第五阶段：推理与部署 (Inference & Deployment)

### S12: 高效推理技术
**目标**: 掌握生产环境优化
- KV Cache: 原理与内存优化
- 量化: PTQ vs QAT, INT8/INT4/FP8
- 投机解码 (Speculative Decoding)
- 连续批处理与分页注意力 (vLLM)
- **诊断点**: KV Cache的内存复杂度？Group Query Attention的动机？

### S13: 长上下文处理
**目标**: 突破上下文长度限制
- 位置编码外推: ALiBi, RoPE scaling
- 上下文压缩与摘要
- RAG vs 长上下文: 何时用什么
- **诊断点**: RoPE位置编码的外推困境？RAG和长上下文的成本对比？

---

## 第六阶段：前沿与探索 (Frontiers)

### S14: 多模态大模型
**目标**: 理解视觉-语言模型
- CLIP: 对比学习的跨模态对齐
- Flamingo/GPT-4V: 视觉指令微调
- Diffusion与LLM的结合
- **诊断点**: 视觉tokenization的方法？多模态对齐的挑战？

### S15: Agent 与工具使用
**目标**: 从模型到行动体
- Function Calling 的机制
- ReAct, Reflection 等推理架构
- 多Agent协作与规划
- **诊断点**: Tool use的tokenization问题？Agent的边界在哪里？

### S16: 架构新探索
**目标**: 超越Transformer
- Mamba/State Space Models
- Mixture of Experts (MoE)
- RetNet, RWKV 等线性注意力
- **诊断点**: SSM的线性复杂度优势？MoE的负载均衡问题？

---

## 学习路径建议

### 路径A: 应用开发者
Modules: 04 → 06 → 09 → 12 → 13 → 15

### 路径B: 算法研究员
Modules: 01 → 02 → 03 → 04 → 05 → 06 → 08 → 10 → 11

### 路径C: 全栈工程师
Modules: 04 → 05 → 06 → 07 → 09 → 10 → 12 → 13 → 14 → 15

---

## 进度追踪

每完成一个模块，在 [../docs/progress.md](../docs/progress.md) 中更新状态：
- `🔄 Not Started`
- `📖 Reading`
- `💡 Understanding`
- `🔨 Practicing`
- `✅ Mastered`

每个Module的预估学习时间: 4-8小时 (包含诊断、学习、练习、测评)
