![PM-Quill Logo](images/pm-quill-logo.png)

# PM-Quill — AI-Powered Product Decision Tool

[中文](README.zh.md) | [日本語](README.ja.md)

> Think before you code.

The **upstream** of coding AI tools. Cursor / Claude Code writes your code. PM-Quill helps you decide **what code to write**.

## Why PM-Quill

AI has lowered the barrier to coding to the floor. But the decision of "what to build" and "why to build it" still relies on gut feeling.

The common cycle for indie developers:

```
Have an idea → Start coding → Realize halfway the direction is wrong → Start over
```

PM-Quill breaks this cycle:

```
Have an idea → /spec think it through → /feasibility evaluate → /plan break into tasks → Hand off to AI to code
```

## Core Commands

| Command | What it does | Output |
|---------|-------------|--------|
| `/spec` | Turn a vague idea into a structured product spec | `specs/{project}/spec.md` |
| `/feasibility` | Evaluate technical approaches, effort, and risks | `specs/{project}/feasibility.md` |
| `/plan` | Break down into an executable task list | `specs/{project}/plan.md` |
| `/review` | Project retrospective, extract lessons learned | `specs/{project}/review.md` |

## Quick Start

### Prerequisites

- Install [Claude Code](https://code.claude.com/)
- Install [OpenCode](https://opencode.ai/)

### Usage

1. Clone the repo:

```bash
git clone https://github.com/lukeliu95/PM-Quill.git
```

2. Launch Claude Code / OpenCode in the PM-Quill directory:

```bash
cd PM-Quill
claude
```

3. Start using:

```
/spec I want to build a dashboard that helps indie devs track AI API costs
```

PM-Quill will ask a few key questions, then generate a complete product spec. Next, run `/feasibility` to evaluate approaches, `/plan` to break into tasks, and hand the tasks off to OpenCode or Claude Code to write the code.

## Workflow Example

```
You: /spec I want to build a Chrome extension to quickly save and organize bookmarks

PM-Quill: [Asks 1-2 key questions]
PM-Quill: [Generates specs/bookmark-manager/spec.md]

You: /feasibility

PM-Quill: [Evaluates 2-3 technical approaches, estimates effort]
PM-Quill: [Generates specs/bookmark-manager/feasibility.md]

You: /plan

PM-Quill: [Breaks into daily tasks, each with prompts ready for AI]
PM-Quill: [Generates specs/bookmark-manager/plan.md]

You: Copy Task 1.1's prompt into Cursor, start coding
```

## Project Structure

```
PM-Quill/
├── CLAUDE.md              # Product soul file
├── context/               # Product and user context
│   ├── product.md         # PM-Quill's product definition
│   └── user.md            # Target user personas
├── specs/                 # All project spec outputs
│   └── {project-name}/    # One subdirectory per project
├── templates/             # Spec templates
├── archive/               # Archived completed projects
└── .claude/
    ├── agents/            # Specialized agent definitions
    ├── skills/            # Slash command definitions
    └── rules/             # Writing standards
```

## Design Principles

1. **Spec drives everything** — No spec, no action
2. **Files as database** — All outputs are Markdown: readable, searchable, version-controlled
3. **Progressive disclosure** — Deliver an 80% solution first, flag uncertainties for your decision
4. **Simplicity first** — Three lines of repeated code beats a premature abstraction

## What We Don't Do

- Don't write code (leave that to Cursor / Claude Code)
- Don't do project management (leave that to Linear / Notion)
- Don't do design (leave that to Figma / Gemini)
- Don't do market research (leave that to dedicated research tools)

## Author

- [Luke Liu](https://x.com/lukeliu95)

## License

MIT
