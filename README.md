# GPT Image 2 Prompt Couture

**GPT Image 2 安全提示词技能包 | Safety-Aligned Prompting Skill Pack**

适用于 Hermes Agent / OpenClaw Codex / Claude Code 等 AI 智能体一键学习。
A skill pack designed for AI agents to master GPT Image 2 prompt engineering.

---

## 项目介绍 | Introduction

一套从互联网社区最佳实践中收集融合的 GPT Image 2 提示词工程技能包。

**核心功能 | Core Functions:**
- **敏感→安全转换**：将直白/敏感提示词转为专业视觉语言，安全可出图
  Sensitive→Safe conversion: transform raw prompts into safety-aligned professional prompts
- **模块化提示词**：低交集分行格式，适合复杂场景（古装、互动、角色扮演）
  Modular prompting: low-intersection block format for complex scenes
- **提示词扩写**：短想法 → 完整可出图提示词
  Prompt expansion: short ideas → complete generation-ready prompts
- **提示词修复**：冲突审计 + 压缩冗余 + 重写
  Prompt repair: conflict audit + compression + rewrite
- **图片反推**：从参考图提取视觉系统 → 可复用提示词
  Image distillation: extract visual systems from reference images
- **表情控制**：情绪词/emoji → 面部肌肉描述
  Expression control: emotion → facial muscle descriptions
- **参数导演**：部分参数 → 自动补全完整提示词
  Parameter director: partial params → auto-completed prompts
- **完整工作流**：从想法到测试迭代的8步系统
  Full workflow: 8-step system from idea to tested template

---

## 仓库结构 | Repository Structure

```
.
├── SKILL.md                             # 主技能文件（中英双语）
├── assets/
│   └── skill-map.svg
└── references/
    ├── core-methods.md                  # 9大核心方法
    ├── prompt-patterns.md               # 风格模式库（人像/古风/3D/品牌/城市）
    ├── prompt-recipes.md                # 配方模板（参数锁定/4K/修复/变体）
    └── sensitive-to-safe-dictionary.md  # 敏感→安全完整转换词典
```

---

## 快速使用 | Quick Start

### 场景 1：敏感提示词转换 | Sensitive Prompt Conversion

```
用户输入: "性感美女，穿着暴露的黑色蕾丝睡衣，撩人的姿势"

→ Agent 执行安全转换流程：
1. 识别风险点 Identify risk points
2. 提取核心审美意图 Extract core aesthetic intent
3. 专业视觉语言重写 Rewrite professionally
4. 输出可出图的安全提示词 Output generation-safe prompt
```

### 场景 2：短需求扩写 | Short Idea Expansion

```
用户输入: "古风美女，白衣，竹林"
→ 判断类型 → 补全模块 → 输出完整提示词
```

### 场景 3：提示词修复 | Prompt Repair

```
用户输入: "帮我把这个长提示词改得更好用"
→ 冲突审计 → 压缩冗余 → 重写
```

### 场景 4：图片反推 | Image-to-Prompt

```
用户上传图片: "帮根据这张图写一个同款 prompt"
→ 分析构图/光线/姿态/材质 → 输出视觉分析+可复用方法+生成提示词
```

---

## 如何教 AI 智能体学习 | How to Teach an AI Agent

```
请学习这个仓库作为 GPT Image 2 生图提示词技能。

先读 SKILL.md，理解路由、转换、锁参和输出规则。

需要方法、改写、图片反推或模块提示词时 → 读 references/core-methods.md
需要敏感词安全转换时 → 读 references/sensitive-to-safe-dictionary.md
用户给出具体图像类型/风格时 → 读 references/prompt-patterns.md
需要模板、参数锁定、4K、修复时 → 读 references/prompt-recipes.md

输出规则 Output rules:
- 用户明确写出的参数必须保留 Preserve user-asserted parameters
- 简单人像 → 高信号短提示词 Simple portraits → compact prompt
- 复杂互动图 → 低交集模块格式 Complex scenes → modular format
- 敏感词必须转译 Sensitive words → professional translation
- 失败时只改一个主要问题 Change only one issue per round
- 输出干净专业的提示词 Output clean, professional prompts
```

---

## 设计理念 | Design Philosophy

从社区最佳实践中提炼的三个核心原则：

1. **信 Fidelity** — 保留用户核心审美意图
2. **雅 Elegance** — 用专业视觉语言替换直白描述
3. **达 Deliverability** — 输出安全通过审核并可出图的提示词

---

## 参考文件读取指南 | Reference Guide

| 文件 File | 何时读取 When to Read |
|-----------|---------------------|
| `references/core-methods.md` | 需要核心方法、改写、图片反推、工作流时 |
| `references/prompt-patterns.md` | 用户给出具体图像类型或风格时 |
| `references/prompt-recipes.md` | 需要模板、参数锁定、4K、修复、变体时 |
| `references/sensitive-to-safe-dictionary.md` | 需要敏感→安全转换时 |

---

## License

MIT
