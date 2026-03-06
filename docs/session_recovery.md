# 会话恢复指南

> 如果你发现我"忘记"了我们的学习进度，请直接读取本文件，我会立即恢复上下文。

## 快速恢复步骤

### 步骤1: 读取核心记录（必做）
```bash
# 请让我执行这些命令
Read /Users/didi/work/llm_learning_claude_code/docs/progress.md
Read /Users/didi/work/llm_learning_claude_code/docs/reminder_config.md
Read /Users/didi/work/llm_learning_claude_code/docs/session_recovery.md
```

### 步骤2: 恢复上下文后我会知道
- ✅ 你的学习风格：诊断式分层，当前层级L2.5
- ✅ 学习目标：面试准备 + 基础巩固
- ✅ 当前进度：M1-01已完成，M1-03/04进行中
- ✅ 薄弱点：Attention softmax细节、MQA计算量理解、LayerNorm原因
- ✅ 待办：3个费曼输出未完成

### 步骤3: 继续学习
根据上次进度，我会提供3个选项：
1. 先完成上次的费曼输出
2. 复习薄弱点（我会出3道检测题）
3. 继续新主题

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
├── 模块: M1 Transformer架构
├── 主题: Attention回顾、Pre/Post LN、MQA/GQA、Flash Attention
├── 时长: ~1小时
├── 表现: 4/5题答对或部分正确
└── 遗留: 3个费曼输出待完成
```

### 当前薄弱点（需要反复测试）
1. **Attention完整公式**: 容易漏softmax和mask
2. **多头计算量**: 误以为多头省计算（实际MQA/GQA才省）
3. **LayerNorm原因**: 知其然不知其所以然

### 下次学习建议
- **如果时间<30分钟**: 完成费曼输出 + 薄弱点复习
- **如果时间>30分钟**: 继续M1-02位置编码深度解析 或 开始Mini-GPT项目

---

## 防遗忘声明

我是Claude，每次对话开始时我可能没有之前的上下文。但只要你：

1. **在项目目录下对话** (`/Users/didi/work/llm_learning_claude_code/`)
2. **让我读取上述3个文件**
3. **或直接说"继续上次的学习"**

我就能立即恢复全部上下文，无缝继续。

**如果我发现有记录不一致，请以文件记录为准，并提醒我更新。**
