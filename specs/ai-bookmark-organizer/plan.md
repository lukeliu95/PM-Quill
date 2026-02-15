# 智能书签整理助手 — 执行计划

> 基于：spec.md + feasibility.md
> 技术方案：React + Vite + Chrome Extension
> MVP 范围：AI 一键整理 + 书签展示，验证核心需求
> 预计工期：5 天

## 任务列表

### Phase 1: 基础搭建（Day 1）

#### Task 1.1: 初始化 Chrome Extension 项目
- 目标：搭建可运行的 React + Vite Chrome 扩展脚手架
- 步骤：
  1. 使用 `npm create vite@latest` 创建 React 项目
  2. 配置 Chrome Extension 所需的 manifest.json
  3. 配置 Vite 打包输出为 Chrome 扩展
  4. 安装并配置 chrome-extension-devtools（如需要）
- 验收标准：能够本地加载扩展到 Chrome，弹出框可正常显示
- 给 AI 的提示词：
  > 创建一个 React + Vite 的 Chrome Extension 项目。要求：
  > 1. 使用 Vite + React
  > 2. 配置 manifest.json，包含 bookmarks 权限和 popup
  > 3. 弹出框能正常打开并显示简单 UI
  > 4. 能够通过 `npm run build` 打包
  > 5. 扩展可以手动加载到 Chrome 中测试
  > 
  > 参考：https://developer.chrome.com/docs/extensions/mv3/getstarted

#### Task 1.2: 书签读取与展示
- 目标：在弹出框中展示用户书签
- 步骤：
  1. 调用 chrome.bookmarks.getTree 读取所有书签
  2. 渲染树形结构展示书签
  3. 支持点击文件夹展开/折叠
- 验收标准：能看到用户所有书签，结构清晰
- 给 AI 的提示词：
  > 在 Chrome Extension 中实现书签读取和展示：
  > 1. 使用 chrome.bookmarks.getTree 读取所有书签
  > 2. 在 React 组件中渲染树形结构（支持文件夹展开/折叠）
  > 3. 显示每个书签的标题和 URL
  > 4. 区分文件夹和书签的样式

### Phase 2: 核心功能（Day 2-3）

#### Task 2.1: MiniMax API 集成
- 目标：能调用 MiniMax API 进行分类
- 步骤：
  1. 在设置页面让用户配置 API Key
  2. 实现调用 MiniMax API 的服务函数
  3. 处理 API 错误和超时
- 验收标准：输入 API Key 后能成功调用 MiniMax
- 给 AI 的提示词：
  > 实现 MiniMax API 集成：
  > 1. 创建设置页面，允许用户输入 MiniMax API Key（保存到 chrome.storage）
  > 2. 实现调用 MiniMax Chat API 的函数（使用 OpenAI 兼容格式）
  > 3. 使用 MiniMax-M2.5 模型
  > 4. 添加错误处理和加载状态
  > 
  > API 端点：https://api.minimax.io/v1/chat/completions
  > 模型：MiniMax-M2.5

#### Task 2.2: AI 分类功能
- 目标：批量分析书签并生成分类建议
- 步骤：
  1. 实现批量获取书签内容（需要抓取网页摘要）
  2. 构建 Prompt 发送给 MiniMax
  3. 解析 AI 返回的分类结果
  4. 展示分类建议给用户确认
- 验收标准：选择若干书签，能得到 AI 分类建议
- 给 AI 的提示词：
  > 实现 AI 分类功能：
  > 1. 用户选择要分类的书签（支持多选）
  > 2. 对每个 URL 发送 HEAD 请求获取页面标题和 meta 描述
  > 3. 构建 Prompt，让 AI 分析内容并分类到合适的主题文件夹
  > 4. 解析 AI 返回的 JSON 格式分类结果
  > 5. 显示分类建议，包含目标文件夹和标签
  > 
  > Prompt 示例：
  > "分析以下书签内容，将其分类到合适的主题类别。返回 JSON 格式：[{url, title, category, tags}]"

#### Task 2.3: 书签移动功能
- 目标：用户确认后执行分类移动
- 步骤：
  1. 创建分类文件夹（如果不存在）
  2. 调用 chrome.bookmarks.move 移动书签
  3. 更新界面显示
- 验收标准：确认分类后，书签被移动到对应文件夹
- 给 AI 的提示词：
  > 实现书签移动功能：
  > 1. 用户确认 AI 的分类建议后，点击"确认整理"
  > 2. 对每个分类建议，创建对应的文件夹（如不存在）
  > 3. 使用 chrome.bookmarks.move 将书签移动到对应文件夹
  > 4. 移动完成后刷新书签列表
  > 5. 显示整理结果（成功移动多少个）

### Phase 3: 优化与 MVP 收尾（Day 4-5）

#### Task 3.1: 基础搜索功能
- 目标：支持关键词搜索书签
- 步骤：
  1. 实现基于标题/URL 的关键词搜索
  2. 在顶部添加搜索框
  3. 搜索结果高亮显示
- 验收标准：输入关键词能过滤显示匹配的书签
- 给 AI 的提示词：
  > 实现基础搜索功能：
  > 1. 在书签列表顶部添加搜索框
  > 2. 支持按标题和 URL 关键词过滤
  > 3. 实时过滤，无需点击搜索按钮
  > 4. 无结果时显示提示

#### Task 3.2: UI 优化与错误处理
- 目标：体验流畅，错误有提示
- 步骤：
  1. 添加加载状态和进度条
  2. 错误提示（API 失败、网络问题等）
  3. 基本的响应式布局
- 验收标准：各状态有清晰反馈
- 给 AI 的提示词：
  > 完善 UI 和错误处理：
  > 1. 添加加载状态（API 调用中显示 spinner）
  > 2. API 错误时显示友好提示
  > 3. 整理过程中显示进度条
  > 4. 基本的 CSS 美化（参考 Chrome 扩展风格）

#### Task 3.3: 本地测试与打包
- 目标：扩展可正常安装使用
- 步骤：
  1. 修复可能的问题
  2. 打包为 .zip
  3. 手动安装测试
- 验收标准：扩展能正常安装，核心功能可用
- 给 AI 的提示词：
  > 完成最后的测试和打包：
  > 1. 修复所有 console 错误
  > 2. 运行 `npm run build` 打包
  > 3. 在 Chrome 中加载已解压的扩展测试
  > 4. 验证核心流程：读取书签 → 选择 → AI 分类 → 确认移动

## 风险缓解

| 风险 | 触发条件 | 应对方案 |
|------|---------|---------|
| 跨域请求失败 | 抓取网页内容时遇到 CORS | 使用后台 service worker 发起请求 |
| API 调用失败 | MiniMax API 不可用 | 显示错误提示，支持重试 |
| 分类效果不好 | AI 分类结果不准确 | 用户可手动调整分类目标 |

## 发布清单

- [ ] 扩展可加载到 Chrome
- [ ] 书签读取和展示正常
- [ ] AI 分类功能可用
- [ ] 书签移动功能正常
- [ ] 基础搜索功能
- [ ] 基本错误处理
- [ ] README 或使用说明
