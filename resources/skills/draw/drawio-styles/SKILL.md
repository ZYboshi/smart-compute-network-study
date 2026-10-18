---
name: drawio-styles
version: 1.0.0
description: drawio-skill 的风格包集合与选择路由。Use when the user asks for any draw.io diagram (流程图、架构图、神经网络图、ER 图、UML、时序图等) — 提供可选的自定义视觉风格。触发词：画图、风格、style、drawio、流程图、架构图、示意图。生成 drawio 图之前先决定是否套用风格包。
---

# drawio-styles — drawio 风格包容器

本目录是 **drawio-skill 的补充风格包集合**。drawio-skill 负责生成机制
（XML、CLI 导出、校验、自检）；本 skill 决定**套用哪个视觉风格**。

## 可用风格包

每个子文件夹是一个独立风格包（各自带 SKILL.md，触发词见其 description）：

| 风格 | 目录 | 适用场景 |
|---|---|---|
| `nn-diagram-style` | [nn-diagram-style/](nn-diagram-style/SKILL.md) | 神经网络/ML 教材风格结构图 |

## 核心规则：风格未指明时必须反问

当用户要求用 drawio-skill 画图，且 prompt 中**没有明确指出**使用哪种风格时，
**不要直接开始生成、也不要静默套用任何风格或默认配色**——先反问用户：

> 想用哪种风格？可选：<列出上表中的风格名>，或者不使用风格（drawio-skill 内置默认配色）。

用户回答"不使用 / 用默认 / 不需要 styles"时，激活状态 = 无风格包，走 drawio-skill 内置惯例。

用户点名某个风格后，加载对应子文件夹的 SKILL.md 并遵循其工作流。

若用户在 prompt 中已明确风格指向（直接命中某个子风格包的触发词），**无需反问**，直接加载。

## 优先级链条

子风格包里的 conventions > 子风格包的 preset.json > drawio-skill 内置惯例。

## 新增风格包

在本目录下新建子文件夹：`SKILL.md`（触发词 + 工作流）、可选 `presets/` 与 `references/`，
然后更新上表。pi 会递归发现子文件夹中的 SKILL.md，无需其他配置。
