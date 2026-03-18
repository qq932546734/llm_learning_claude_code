# 会话恢复指南

> 如果你发现我"忘记"了我们的学习进度，请直接读取本文件，我会立即恢复上下文。

## 快速恢复步骤

### 步骤1: 读取核心记录（必做）
```bash
# 请让我执行这些命令
Read /Users/didi/work/llm_learning_claude_code/docs/progress.md
Read /Users/didi/work/llm_learning_claude_code/docs/reminder_config.md
Read /Users/didi/work/llm_learning_claude_code/docs/question_bank.md
Read /Users/didi/work/llm_learning_claude_code/docs/question_analysis.md
Read /Users/didi/work/llm_learning_claude_code/docs/session_recovery.md
```

### 步骤2: 恢复上下文后我会知道
- ✅ 你的学习风格：诊断式分层，当前层级L2.5
- ✅ 学习目标：面试准备 + 基础巩固
- ✅ 当前进度：以 `docs/progress.md` 为准（模块编号口径见 `docs/taxonomy.md`）
- ✅ 最近沉淀的问题：以 `docs/question_bank.md` 为准
- ✅ 薄弱点：Attention softmax细节、MQA计算量理解、LayerNorm原因
- ✅ 待办：以 `docs/progress.md` / `docs/reminder_config.md` 为准

### 步骤3: 继续学习
根据上次进度，我会提供3个选项：
1. 学习模式：继续主线 / 复习薄弱点 / 新主题
2. 提问模式：先回答当前问题并沉淀到知识库
3. 混合模式：先处理 1 个问题，再回到学习主线

---

## 完整学习档案

### 学习者画像
| 属性 | 值 |
|------|-----|
| 当前水平 | 有LLM基础，非初学者 |
| 诊断层级 | L2.5（理解层偏应用） |
| 优势领域 | 位置编码(RoPE)、复杂度分析 |
| 待强化 | 注意力细节、归一化原理 |
| 学习节奏 | 灵活安排 |

### 学习历史
```
2026-03-06: 第1次学习
├── 模块: M01 Transformer架构
├── 主题: Attention回顾、Pre/Post LN、MQA/GQA、Flash Attention
├── 时长: ~1小时
├── 表现: 4/5题答对或部分正确
└── 遗留: 当时有3个费曼输出（现已完成）
```

### 当前薄弱点（需要反复测试）
1. **Attention完整公式**: 容易漏softmax和mask
2. **多头计算量**: 误以为多头省计算（实际MQA/GQA才省）
3. **LayerNorm原因**: 知其然不知其所以然

### 下次学习建议
- **如果时间<30分钟**: 完成费曼输出 + 薄弱点复习
- **如果时间>30分钟**: 继续 M03 分词与表示 或推进 M12 推理优化补完

---

## 防遗忘声明

我是Claude，每次对话开始时我可能没有之前的上下文。但只要你：

1. **在项目目录下对话** (`/Users/didi/work/llm_learning_claude_code/`)
2. **让我读取上述核心文件**
3. **或让我读取 `docs/question_bank.md` / `docs/question_analysis.md` 恢复问题上下文**
4. **或直接说"继续上次的学习"**

我就能立即恢复全部上下文，无缝继续。

**如果我发现有记录不一致，请以文件记录为准，并提醒我更新。**
