---
name: nn-diagram-style
version: 1.0.0
description: 神经网络/机器学习教材风格图的补充样式规范，与 drawio-skill 配合使用。Use when the user asks for neural-network or ML model-structure diagrams in textbook style (感知机、多层前馈网络、CNN/RNN/Transformer 结构图、前向/反向传播流程图等), or names the preset "nn-textbook". 触发词：神经网络图、模型结构图、神经元结构图、nn-textbook、教材风格、画一个神经网络. 生成神经网络类示意图时也优先适用。
---

# nn-diagram-style — 神经网络教材风格样式包

这是 **drawio-skill 的补充样式 skill**：drawio-skill 负责生成机制（XML、CLI 导出、校验、自检），
本 skill 强制套用一套「教科书神经网络图」的视觉与构图规范。

## Step 0 — 判断是否激活

满足任一条件即激活本样式包：

- 用户要求画神经网络/ML 模型结构类示意图（感知机、多层前馈网络、层结构、前向/反向传播、RNN/CNN/Transformer 结构图等）
- 用户点名 "nn-textbook" 样式
- 用户要求「教材风格」「课件风格」的 drawio 图

若用户明确要求其他风格（如原 drawio-skill 内置的 corporate、handdrawn 等），**不激活**，直接走 drawio-skill 默认流程。

## Step 1 — 必读文件（生成任何 XML 之前）

两份文件都读完才能开始画：

1. `references/nn-textbook-conventions.md` — schema 之外的构图惯例（**核心：神经元白底圆、颜色只用三处、层名在矩形上方等**，含反例清单）
2. `presets/nn-textbook.json` — 配色/形状/字体预设 JSON（路径相对于本 skill 目录解析）

## Step 2 — 与 drawio-skill 协作

按 drawio-skill 的完整工作流生成（依赖检查 → 生成 → 导出 → 自检），并满足以下优先级：

**conventions.md > preset JSON > drawio-skill 内置惯例**

即：预设 JSON 覆盖内置配色/字体，conventions.md 在两者之上再覆盖构图决策。
冲突时以 conventions.md 的反例清单为准。

风格包的选择与「风格未指明时反问」逻辑由上层容器 `../SKILL.md`（drawio-styles）统一管理。
加载后按 drawio-skill 惯例在回复首行注明：*"Using preset `nn-textbook`."*
