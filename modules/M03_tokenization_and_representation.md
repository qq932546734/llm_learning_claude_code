# M03: 分词与表示（Tokenization & Representation）

> Canonical 模块编号口径见 `docs/taxonomy.md`。本模块对应 README 的 `M03`。

## 为什么学
- tokenizer 决定模型“看见世界”的粒度，直接影响参数量、压缩效率、多语言表现和推理带宽。
- 这是面试里特别能拉开理解层次的主题之一。

## 前置依赖
- M01 中的 embedding / softmax 基本概念
- M02 中的预训练目标直觉

## 诊断题
1. subword 相比“纯词/纯字”的核心收益与代价分别是什么？
2. BPE 每一步 merge 的贪心选择在优化什么？典型副作用是什么？
3. `vocab_size=50k, d_model=4096` 时 embedding 参数量级是多少？tied embeddings 会怎样影响参数量？

## 核心知识点
- `核心必会`：subword 是“压缩 + 归纳偏置”的组合，不只是预处理。
- `核心必会`：BPE / WordPiece / SentencePiece(Unigram) 的训练目标、切分行为和适用场景。
- `工程重点`：多语言、代码、长数字串、emoji、罕见词会怎样影响 tokenizer 设计。
- `工程重点`：embedding 矩阵、输出 softmax、tied embeddings、vocab size 对参数量和带宽的影响。
- `面试高频`：为什么同一模型架构只换 tokenizer，也会影响效果和成本。

## 易错点 / 边界条件
- 容易把 BPE 说成“全局最优压缩”，但它其实是贪心合并。
- 容易把 tokenizer 当成纯数据清洗步骤，忽略它对参数量和推理速度的影响。
- 容易说“vocab 越大越好”，却忽略 embedding 参数和长尾 token 利用率。

## 练习
- [ ] 给一段中英混合+代码文本，比较不同 tokenizer 的切分差异并解释原因
- [ ] 估算：不同 vocab size 下 embedding 参数占比与推理带宽影响
- [ ] 设计题：如果要训练一个中英混合代码模型，你会优先调 tokenizer 的哪三个维度？

### 学习产物
- 1 页总结：subword 价值、三类 tokenizer 差异、embedding 参数量公式。
- 1 组错题：至少记录 3 个易混点，如 BPE 贪心性、tied embeddings、vocab trade-off。
- 1 个练习产物：参数量估算表或 tokenizer 对比分析表。

#### 本次学习总结（2026-03-12）

**1 页总结**

- tokenizer 不是“预处理细节”，而是模型设计的一部分；它同时影响表示粒度、平均序列长度、embedding/output 参数量，以及训练和推理成本。
- subword 的核心价值是在“纯词”和“纯字”之间做折中：相比纯词，显著缓解 OOV 和长尾稀疏；相比纯字，通常能显著缩短序列长度。
- BPE / WordPiece / Unigram 都做 subword 切分，但训练思路不同：
  - BPE：从字符出发，贪心合并高频 pair，更像压缩。
  - WordPiece：更偏向选择能提升语料似然的子词。
  - Unigram：先给一个较大的候选词表，再删掉贡献小的 token，更像概率建模加剪枝。
- embedding 参数量公式：`vocab_size x d_model`。例如 `50k x 4096 ≈ 2.05e8`，约 2.05 亿参数。
- tied embeddings 表示输入 embedding 和输出投影共享同一份大矩阵；若不共享，vocab 相关参数通常近似翻倍。
- tokenizer 会影响 serving 成本：更短序列通常更利于 prefill；更大 vocab 会增加 embedding/output 层参数量，并抬高 decode 时的输出层带宽开销。

**错题 / 易混点**

- 不要把 BPE 说成“全局最优压缩”；它只是局部贪心 merge。
- 不要把“大 vocab 的主要问题”简单说成“长尾更严重”；更准确的说法是 token 利用率可能下降，且 embedding/output 层更大。
- 不要说“vocab size 直接决定序列长度”；更准确地说，是它显著影响平均切分粒度与平均序列长度。

**练习产物：参数量与 serving 取舍**

| 方案 | vocab size | avg seq len | embedding 参数量（`V x d`，`d=4096`） | prefill 直觉 | decode / 带宽直觉 |
|------|------------|-------------|----------------------------------------|--------------|-------------------|
| A | 50k | 1200 | ≈ 2.05 亿 | 序列更长，prefill 更贵 | 输出层更小，decode 更轻 |
| B | 100k | 900 | ≈ 4.10 亿 | 序列更短，prefill 更省 | 输出层更大，decode 更重 |

结论：不能简单说“大 vocab 一定更快”或“短序列一定更好”；本质是在 `参数量 / 输出层带宽` 与 `序列长度 / KV cache / prefill 开销` 之间做权衡。

## 费曼输出
用你自己的话解释：为什么 tokenization 不是“预处理细节”，而是模型能力/成本的一部分？

### 本次费曼输出（2026-03-12）
tokenizer 不是简单的预处理细节，而是模型设计的一部分。它首先决定词表大小和切分粒度，这会直接影响 embedding 和输出层的参数规模。它还会影响模型对文本的表示方式，比如长尾词、罕见词、多语言和代码片段是被整体记住，还是被拆成多个子词来组合表示。同时，tokenizer 会影响平均序列长度，而序列长度又直接影响训练成本以及推理时 prefill 阶段的开销。更进一步，词表大小也会影响 decode 时的输出层开销，所以 tokenizer 实际上是在 `参数量、序列长度、泛化能力、训练成本、推理成本` 之间做权衡。

## 面试高频问法
### 问法 1
问题：BPE、WordPiece、SentencePiece 的核心区别是什么？
- 一句话答案：三者都做 subword 切分，但优化目标、训练过程和边界处理方式不同。
- 展开框架：目标函数 -> 切分粒度 -> 空格/原始文本处理 -> 多语言适应性。
- 常见追问点：为什么 SentencePiece 常用于多语言？Unigram 和 BPE 的直觉区别是什么？

### 问法 2
问题：为什么 tokenizer 会影响模型参数量和推理成本？
- 一句话答案：vocab size 直接决定 embedding / softmax 矩阵规模，也影响平均序列长度和带宽。
- 展开框架：vocab size -> embedding 参数 -> 输出层 -> token 数量 -> 推理吞吐。
- 常见追问点：tied embeddings 为什么常见？大 vocab 的利弊是什么？

## 完成标准
- 诊断题正确率达到 80%。
- 完成 1 次费曼输出。
- 完成 1 道参数量估算题和 1 道 tokenizer 对比题。
- 能独立解释 subword 收益/代价、BPE 贪心性和 tied embeddings。

## 参考
- SentencePiece / BPE 相关论文与实现链接可补充到扩展阅读区。

## 后续关联
- 与 `M02` 相连：tokenization 影响预训练输入分布与数据利用率。
- 与 `M12` 相连：vocab size 和平均序列长度会影响推理带宽与吞吐。
