# Quill — 产品定义

## 一句话

AI 驱动的产品决策工具。帮你在写代码之前想清楚做什么。

## 定位

编码 AI 工具的上游。Cursor/Claude Code 帮你写代码，Quill 帮你决定写什么代码。

## 目标用户

**SaaS 崩盘后独立创业的技术人**
- 会写代码（或会用 AI 写代码），但不擅长产品决策
- 一个人或小团队，没有 PM
- 用 vibe coding 快速出原型，但经常"做了才发现方向不对"
- 需要的不是更好的编码工具，而是"写代码之前帮我想清楚"

## 核心功能（3 个）

### 1. Spec 生成（/spec）
输入：一个模糊的想法（"我想做一个 XX"）
输出：结构化的产品规格文件
- 用户是谁、痛点是什么
- 核心功能（不超过 3 个）
- 不做什么（明确排除）
- 成功标准

### 2. 可行性分析（/feasibility）
输入：一份 Spec
输出：可行性评估
- 技术方案选择（2-3 个方案对比）
- 工作量估算（天/周）
- 关键风险和依赖
- 建议的技术栈

### 3. 执行计划（/plan）
输入：确认后的 Spec + 可行性分析
输出：可执行的任务列表
- 按优先级排序的任务
- 每个任务的验收标准
- MVP 范围划定
- 可以直接交给 Cursor/Claude Code 的任务描述

## 不做什么

- 不写代码（那是 Cursor/Claude Code 的事）
- 不做项目管理（那是 Linear/Notion 的事）
- 不做设计（那是 Figma 的事）
- 不做市场调研（那是 Bill_v1/Alan 的事）

## 产品形态

**Phase 1（MVP）：Claude Code 原生技能**
- 以 `.claude/skills/` 的形式存在
- 用户在任何项目目录下用 `/spec`、`/feasibility`、`/plan` 调用
- 输出 Markdown 文件到项目目录

**Phase 2（考虑中）：独立 CLI 工具**
- 可能打包为 npm 包或 OpenClaw Skill
- 自带模板和 Agent 配置

## 灵感来源

- **Bill_v1** — CLAUDE.md + Agent 架构 + 文件记忆 = Quill 的原型
- **obsidian-claude-pkm** — Skills/Agents/Hooks 的标准化格式
- **aios-core** — "Agentic Agile" PRD→执行自动化
