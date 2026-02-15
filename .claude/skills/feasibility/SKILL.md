---
name: feasibility
description: 评估 Spec 的可行性、技术方案、工作量和风险
allowed-tools: Read, Write, Edit, Glob, Grep, WebSearch, WebFetch, TaskCreate, TaskUpdate, TaskList, AskUserQuestion
user-invocable: true
---

# /feasibility — 可行性分析

## 使用方式

```
/feasibility specs/my-project/spec.md
```

或者不带参数，自动读取最近创建的 Spec。

## 这个技能做什么

基于一份 Spec，评估技术可行性，给出 2-3 个技术方案对比，估算工作量和风险。

## 流程

### Step 1: 读取 Spec

读取指定的 spec.md（或最近的 Spec）。如果没有 Spec，提示先运行 `/spec`。

### Step 2: 技术方案研究（5 分钟）

针对 Spec 中的核心功能，用 WebSearch 研究：
- 有哪些技术方案可以实现？
- 各方案的优缺点？
- 有没有现成的库/框架可以用？
- 有没有开源项目可以参考？

### Step 3: 生成可行性报告

在 `specs/{project-name}/` 目录下创建 `feasibility.md`：

```markdown
# {项目名} — 可行性分析

> 基于：spec.md
> 分析时间：{日期}
> 结论：{可行 / 有风险 / 不建议}

## 技术方案对比

### 方案 A: {名称}（推荐）
- 技术栈：{具体技术}
- 优点：{为什么推荐}
- 缺点：{已知风险}
- 工作量：{X 天/周}
- 参考项目：{GitHub 链接}

### 方案 B: {名称}
...

## 工作量估算

| 功能 | 估算 | 难度 | 备注 |
|------|------|------|------|
| 功能 1 | X 天 | 低/中/高 | |
| 功能 2 | X 天 | 低/中/高 | |
| 总计 | X 天 | | |

## 关键风险

1. **{风险名}** — {描述} → 缓解方案：{怎么降低风险}
2. ...

## 关键依赖

- {需要的 API / 服务 / 数据源}

## 建议

{基于以上分析，给出明确建议：做还是不做、先做哪个、技术栈选哪个}
```

### Step 4: 决策确认

问用户：
- 选哪个技术方案？
- 工作量能接受吗？
- 要不要调整 Spec 的范围？

## 输出

- 文件：`specs/{project-name}/feasibility.md`
- 终端：方案对比摘要 + 下一步建议（运行 `/plan`）
