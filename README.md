# PM-Quill — AI 驱动的产品决策工具

> 在写代码之前，先想清楚做什么。

编码 AI 工具的**上游**。Cursor / Claude Code 帮你写代码，PM-Quill 帮你决定**写什么代码**。

## 为什么需要 PM-Quill

AI 把编码的门槛拉到了地板。但"做什么"和"为什么做"这个决策，还是靠拍脑袋。

独立开发者的常见循环：

```
有个想法 → 直接写代码 → 做到一半方向不对 → 推倒重来
```

PM-Quill 帮你打破这个循环：

```
有个想法 → /spec 想清楚 → /feasibility 评估 → /plan 拆任务 → 交给 AI 写代码
```

## 核心命令

| 命令 | 做什么 | 输出 |
|------|--------|------|
| `/spec` | 把模糊想法变成结构化产品规格 | `specs/{project}/spec.md` |
| `/feasibility` | 评估技术方案、工作量、风险 | `specs/{project}/feasibility.md` |
| `/plan` | 拆解成可执行的任务列表 | `specs/{project}/plan.md` |
| `/review` | 项目回顾，提炼经验教训 | `specs/{project}/review.md` |

## 快速开始

### 前提

- 安装 [Claude Code](https://code.claude.com/)
- 安装 [OpenCode](https://opencode.ai/)

### 使用

1. 克隆仓库：

```bash
git clone <repo-url> PM-Quill
```

2. 在 PM-Quill 目录下启动 Claude Code / OpenCode：

```bash
cd PM-Quill
claude
```

3. 开始用：

```
/spec 我想做一个帮独立开发者追踪 AI API 成本的仪表盘
```

PM-Quill 会问你几个关键问题，然后生成一份完整的产品规格。接着运行 `/feasibility` 评估方案，`/plan` 拆成任务，就可以把任务交给 OpenCode 或 Claude Code 去写代码了。

## 工作流示例

```
你：/spec 我想做一个 Chrome 插件，帮人快速保存和整理书签

PM-Quill：[问 1-2 个关键问题]
PM-Quill：[生成 specs/bookmark-manager/spec.md]

你：/feasibility

PM-Quill：[评估 2-3 个技术方案，估算工作量]
PM-Quill：[生成 specs/bookmark-manager/feasibility.md]

你：/plan

PM-Quill：[拆解成按天排列的任务，每个任务附带可以直接给 AI 用的提示词]
PM-Quill：[生成 specs/bookmark-manager/plan.md]

你：把 Task 1.1 的提示词复制到 Cursor，开始写代码
```

## 项目结构

```
PM-Quill/
├── CLAUDE.md              # 产品灵魂文件
├── context/               # 产品和用户上下文
│   ├── product.md         # PM-Quill 的产品定义
│   └── user.md            # 目标用户画像
├── specs/                 # 所有项目的 Spec 输出
│   └── {project-name}/    # 每个项目一个子目录
├── templates/             # Spec 模板
├── archive/               # 已完成项目的归档
└── .claude/
    ├── agents/            # 专业 Agent 定义
    ├── skills/            # 斜杠命令定义
    └── rules/             # 撰写规范
```

## 设计原则

1. **Spec 驱动一切** — 不写 Spec 就不动手
2. **文件即数据库** — 所有产出都是 Markdown，可读、可搜、可版本控制
3. **渐进式披露** — 先出 80% 的方案，不确定的地方标注让你决策
4. **简单优先** — 三行重复代码好过一个过早的抽象

## 不做什么

- 不写代码（交给 Cursor / Claude Code）
- 不做项目管理（交给 Linear / Notion）
- 不做设计（交给 Figma）
- 不做市场调研（交给专门的调研工具）

## 作者

- [刘仙升](https://x.com/lukeliu95)

## License

MIT
