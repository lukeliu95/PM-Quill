# 智能书签整理助手 — 可行性分析

> 基于：spec.md
> 分析时间：2026-02-15
> 结论：可行

## 技术方案对比

### 方案 A: React + Chrome Extension（推荐）

- 技术栈：React + Vite + chrome.bookmarks API
- 优点：生态成熟，开发体验好，组件复用方便
- 缺点：需要构建步骤，扩展包体积稍大
- 工作量：7 天
- 参考项目：MarkMind、BookmarkMind（均使用 React）

### 方案 B: 原生 JS + Chrome Extension

- 技术栈：原生 JS + HTML + chrome.bookmarks API
- 优点：无构建步骤，调试简单，体积小
- 缺点：代码维护性差，难以扩展
- 工作量：5 天

### 方案 C: Vue + Chrome Extension

- 技术栈：Vue 3 + Vite + chrome.bookmarks API
- 优点：开发效率高
- 缺点：与 React 相比生态略小
- 工作量：7 天

## 工作量估算

| 功能 | 估算 | 难度 | 备注 |
|------|------|------|------|
| 扩展脚手架搭建 | 1 天 | 低 | Vite + React + Chrome 插件模板 |
| 书签读取与展示 | 1 天 | 低 | chrome.bookmarks.getTree |
| AI 分类功能 | 2 天 | 中 | MiniMax API 调用，需处理并发 |
| 书签移动功能 | 1 天 | 低 | chrome.bookmarks.move |
| 语义搜索功能 | 2 天 | 中 | 需要 embedding 或关键词匹配 |
| 摘要功能 | 1 天 | 中 | 需要后台抓取网页内容 |
| **总计** | **8 天** | | |

## 关键风险

1. **网页内容抓取** — 跨域问题 → 缓解：使用 Chrome 的 declarativeNetRequest 或后台 service worker
2. **API 成本** — MiniMax API 调用次数和 token 消耗 → 缓解：批量处理，减少请求次数
3. **性能问题** — 500+ 书签处理慢 → 缓解：分批处理，显示进度条

## 关键依赖

- chrome.bookmarks API（浏览器原生，无需额外权限）
- MiniMax API（需要 API Key，可在设置页配置）
- 页面内容抓取（后台脚本，可用 fetch）

## 建议

**技术栈：React + Vite + Chrome Extension**

理由：
- React 生态成熟，参考项目多
- 8 天工作量可接受
- 核心风险可控（跨域可用 service worker 解决）

**下一步：**
1. 确认技术方案
2. 运行 `/plan` 拆解任务
3. 开始搭建原型
