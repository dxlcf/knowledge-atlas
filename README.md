# Knowledge Atlas

**A personal knowledge atlas, continuously refined with AI agents.**

一套由 AI Agent 辅助维护个人知识库的轻量级方法与仓库模板，用于知识记录、结构化整理、学习资源分析与知识体系的持续演进。

## 开始使用（绑定后删除本节）

本项目提供通用方法与模板，个人知识保存在自己的仓库中。先克隆：

```shell
git clone https://github.com/dxlcf/knowledge-atlas.git my-knowledge-atlas
```

在 Agent 中打开 `my-knowledge-atlas` 并授权，准备好自己的空远程仓库（建议私有），然后发送：

> 请将当前仓库的 origin 改为 `<我的远程仓库地址>`。绑定成功后，删除 README 中“开始使用（绑定后删除本节）”整个章节，提交该修改并将当前分支推送到我的仓库。如果目标仓库已有内容，先检查并告知我，不覆盖或强制推送。

替换地址即可，无须更改其他文件或配置。

## 项目简介

Knowledge Atlas 以 **Markdown + Git** 为基础，以**知识大纲（Knowledge Maps）**为核心，通过 AI Agent 协助完成知识的提取、去重、归纳和更新。

它希望解决知识零散、重复学习、缺乏体系和整理成本高的问题，建立一套结构清晰、内容精炼、易于检索、持续完善的个人知识体系，而不是收集尽可能多的资料。

## 核心模块

| 模块 | 入口 | 职责 |
| --- | --- | --- |
| Inbox | [临时笔记](inbox/README.md) | 随手记录，暂存未经整理的知识 |
| Maps | [知识大纲](maps/README.md) | 维护知识层级、掌握程度和笔记索引 |
| Notes | [精炼知识](notes/README.md) | 保存具有长期复用价值的知识 |
| Sources | [外部资料](sources/README.md) | 保存来源分析、知识增量和阅读建议 |

**Inbox** 是知识的快速入口，无须在记录时分类。可以记录想法、问题、学习发现，再按需交给 Agent 整理。

**Maps** 是仓库的核心。通过简洁的分层大纲定位知识、回顾主题全貌、发现缺口，并链接到笔记。掌握程度由用户判断，不能根据笔记是否存在推断。

**Notes** 围绕明确的知识点记录核心概念、关键机制、实践要点和必要限制。一个知识点尽量对应一份规范化笔记，新增知识优先融入已有内容，避免复制长篇教程或 Agent 回答。

**Sources** 记录开源项目、官方文档、技术文章等来源的分析。对照已有知识，区分已覆盖、值得新增和需要深化的内容，提供可追溯的引用与重点阅读建议。

## Agent 工作流

在 Inbox 随手记录，需要时让 Agent 整理，再从 Maps 浏览和回顾知识。无需提前设计分类；首次整理时，Agent 会提出大纲建议，确认后建立索引。

| 工作流 | 示例指令 | 预期结果 | Skill |
| --- | --- | --- | --- |
| 整理笔记 | 整理最近的 Inbox | 提取、归类、去重、合并知识 | [organize-inbox](.agents/skills/organize-inbox/SKILL.md) |
| 分析资料 | 分析这个 GitHub 项目：URL | 知识增量、阅读建议、来源引用 | [analyze-source](.agents/skills/analyze-source/SKILL.md) |
| 沉淀知识 | 将刚才的回答整理到知识库 | 提炼核心结论，新增或更新 Notes | [distill-knowledge](.agents/skills/distill-knowledge/SKILL.md) |
| 优化大纲 | 检查当前知识大纲 | 识别重复、缺口和结构问题 | [refine-map](.agents/skills/refine-map/SKILL.md) |

普通问答默认不修改仓库。“分析资料”默认只返回分析；需要保存时可说“分析并保存到 Sources”。Agent 更新知识前先检索相关 Maps 和 Notes，不把未确认的建议当作知识事实。

## 仓库结构

```text
knowledge-atlas/
├── README.md
├── AGENTS.md
├── inbox/
│   └── README.md
├── maps/
│   └── README.md
├── notes/
│   └── README.md
├── sources/
│   └── README.md
└── .agents/
    └── skills/
        ├── organize-inbox/SKILL.md
        ├── analyze-source/SKILL.md
        ├── distill-knowledge/SKILL.md
        └── refine-map/SKILL.md
```

目录说明内提供可复制的最小格式。主题、子目录、独立模板和辅助工具都按实际需要增加。

## 工作原则

- **大纲优先**：优先读取相关大纲，通过大纲组织与定位知识。
- **增量更新**：创建前检索已有内容，优先补充和合并。
- **内容精炼**：保留核心概念、机制与适用边界，减少重复描述。
- **来源可追溯**：尽量引用原始来源，重要代码引用优先使用固定版本链接。
- **按需沉淀**：仅在明确要求时更新长期知识，不自动保存所有对话。
- **人工主导**：Agent 提供分析与修改建议，用户保留对知识体系的最终控制权。
- **轻量开放**：采用 Markdown 和 Git，不依赖特定 Agent 框架、数据库或知识管理平台。

## 技术方案

| 组件 | 方案 |
| --- | --- |
| 知识存储 | Markdown |
| 版本管理 | Git |
| 知识组织 | 分层大纲 + 相对文件链接 |
| Agent 规则 | AGENTS.md |
| Agent 能力 | 项目级 Skills |
| 外部资料 | URL + 精炼分析 + 来源引用 |
| 检索方式 | 大纲导航 + 文件检索，按需扩展 |

Agent 优先读取相关大纲，再按需加载笔记与资料，减少不必要的上下文消耗。仓库无需安装依赖、启动服务或构建应用。

## 项目目标

**记录知识 → 整理归纳 → 更新大纲 → 发现缺口 → 深入学习 → 持续完善**

让知识库既能记录已经学过的内容，也能帮助判断下一步学习什么、哪些资源具有增量价值，最终成为一份不断演进、能够快速检索与复用的个人知识地图。

## GitHub 仓库信息

**Repository:** `knowledge-atlas`

**Description:** A lightweight, agent-assisted knowledge repository for structured learning, knowledge distillation, and continuous evolution.

**Topics:** `knowledge-management` · `knowledge-base` · `ai-agent` · `markdown` · `personal-knowledge`
