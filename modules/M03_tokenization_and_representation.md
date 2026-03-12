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

## 费曼输出
用你自己的话解释：为什么 tokenization 不是“预处理细节”，而是模型能力/成本的一部分？

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
