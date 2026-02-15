# Skill 自动提取系统 — 可行性分析

> 基于：spec.md
> 分析时间：2026-02-15
> 结论：可行

## 技术方案对比

### 方案 A: Tauri + React（推荐）

- 技术栈：Tauri + React + Rust 文件系统 + MiniMax API
- 优点：原生文件访问、性能好、打包体积小、可做桌面客户端
- 缺点：需要学习 Rust
- 工作量：7 天
- 参考：本地文件处理用 Rust 直接读取，AI 用 MiniMax API

### 方案 B: Electron + React

- 技术栈：Electron + React + Node.js 文件系统 + MiniMax API
- 优点：生态成熟，文件处理简单
- 缺点：包体积大（~150MB）
- 工作量：6 天

### 方案 C: 纯 Web（文件上传）

- 技术栈：React + Web File API + MiniMax API
- 优点：无需安装，浏览器直接用
- 缺点：文件大小限制，无法监听目录变化
- 工作量：5 天

## 工作量估算

| 功能 | 估算 | 难度 | 备注 |
|------|------|------|------|
| 文档解析（MD/PDF/TXT） | 1.5 天 | 中 | md 文件直接读取，PDF 用 pdf-parse |
| AI 提取 Skill | 2 天 | 中 | MiniMax API + JSON Schema 输出 |
| Skill 编辑器 | 1 天 | 低 | 表单编辑 + 预览 |
| 本地存储与共享 | 1.5 天 | 中 | JSON 文件存储，目录共享 |
| UI 打磨 | 1 天 | 低 |  |
| **总计** | **7 天** | | |

## 关键风险

1. **文档解析质量** — 复杂 PDF 解析效果差 → 缓解：优先支持 Markdown，PDF 用 pdf-parse
2. **AI 提取效果** — 提取的 Skill 可能不准确 → 缓解：提供编辑功能，用户可修改
3. **文件共享** — 团队成员如何同步 → 缓解：使用共享目录（如 NAS、Git）

## 关键依赖

- MiniMax API（需要 API Key）
- pdf-parse（PDF 解析）
- 本地文件系统（Rust / Node.js）
- 文件存储（JSON 格式）

## 建议

**技术栈：Tauri + React**

理由：
- 原生文件访问好，支持目录监听
- 打包体积小
- 7 天工作量可接受

**下一步：**
1. 确认技术方案
2. 运行 `/plan` 拆解任务
