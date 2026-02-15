---
name: review
description: 回顾已完成的项目，提炼经验和教训
allowed-tools: Read, Write, Edit, Glob, Grep, TaskCreate, TaskUpdate, TaskList, AskUserQuestion
user-invocable: true
---

# /review — 项目回顾

## 使用方式

```
/review specs/my-project/
```

## 这个技能做什么

项目完成后（或中途暂停时），回顾整个过程，提炼经验。

## 流程

1. 读取项目的所有文件（spec.md, feasibility.md, plan.md）
2. 和用户对话：实际做了什么？和计划差距多大？什么做对了？什么踩坑了？
3. 生成 `specs/{project}/review.md`，包含：
   - 计划 vs 实际对比
   - 关键教训（下次要记住的事）
   - 可复用的模式（什么方法好用）
4. 如果项目完成，移动到 `archive/`

## 输出

- 文件：`specs/{project-name}/review.md`
- 归档到 `archive/{project-name}/`（用户确认后）
