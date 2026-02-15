---
name: plan
description: 把 Spec + 可行性分析拆解成可执行的任务列表
allowed-tools: Read, Write, Edit, Glob, Grep, TaskCreate, TaskUpdate, TaskList, AskUserQuestion
user-invocable: true
---

# /plan — 执行计划生成

## 使用方式

```
/plan specs/my-project/
```

或者不带参数，自动读取最近的项目。

## 这个技能做什么

基于 Spec + 可行性分析，生成可执行的任务列表。每个任务都写得足够清晰，可以直接复制粘贴给 Cursor / Claude Code 去执行。

## 前提

需要先有：
- `specs/{project}/spec.md`（运行 `/spec`）
- `specs/{project}/feasibility.md`（运行 `/feasibility`）

如果缺少，提示用户先运行对应命令。

## 流程

### Step 1: 读取上游文件

读取 spec.md 和 feasibility.md，理解：
- 核心功能和优先级
- 选定的技术方案
- 工作量估算

### Step 2: MVP 划定

和用户确认 MVP 范围：
- 哪些功能进 MVP？（通常是核心功能的最小版本）
- MVP 的目标是什么？（验证需求？获取用户？赚钱？）
- 时间约束？（1 周？2 周？）

### Step 3: 生成执行计划

在 `specs/{project-name}/` 目录下创建 `plan.md`：

```markdown
# {项目名} — 执行计划

> 基于：spec.md + feasibility.md
> 技术方案：{选定的方案}
> MVP 范围：{一句话描述}
> 预计工期：{X 天}

## 任务列表

### Phase 1: 基础搭建（Day 1）

#### Task 1.1: {任务名}
- 目标：{做完后的状态}
- 步骤：
  1. {具体步骤}
  2. {具体步骤}
- 验收标准：{怎么判断做完了}
- 给 AI 的提示词：
  > {可以直接复制给 Cursor/Claude Code 的任务描述}

#### Task 1.2: {任务名}
...

### Phase 2: 核心功能（Day 2-3）
...

### Phase 3: 打磨发布（Day 4-5）
...

## 风险缓解

| 风险 | 触发条件 | 应对方案 |
|------|---------|---------|
| {风险} | {什么时候会出问题} | {怎么处理} |

## 发布清单

- [ ] 核心功能可用
- [ ] 基本错误处理
- [ ] README / 使用说明
- [ ] 首批用户渠道确认
```

### Step 4: 确认开工

问用户：
- 计划可以吗？
- 从哪个 Task 开始？
- 要不要我帮你把第一个 Task 的 AI 提示词准备好？

## 核心原则

- **每个任务 < 2 小时** — 超过的要拆分
- **给 AI 的提示词** — 每个任务都要附带，让用户可以直接复制给 Cursor 用
- **验收标准必须可验证** — 不写"做得好看"，写"首页加载 < 2 秒"

## 输出

- 文件：`specs/{project-name}/plan.md`
- 终端：计划摘要 + 第一个任务的 AI 提示词
