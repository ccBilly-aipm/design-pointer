# 架构说明 (CN)

> Language: CN | [EN](architecture-notes_EN.md)

DesignPointer 当前仍处于规划阶段。本文档描述一个可能的未来架构方向，但暂不实现浏览器插件。

## 可能的未来技术方案

- Chrome Extension Manifest V3
- 用于页面覆盖层的 content script
- 用于截图捕获的 background service worker
- 用于控制操作的 popup 或 side panel
- 用于标注的 canvas 覆盖层
- JSON payload builder
- DOM/CSS context extractor
- 可选的本地 Node.js bridge
- 可选集成 Codex、Claude Code、Cursor 或其他 AI coding agents

## 高层组件

### 浏览器插件

浏览器插件会提供面向用户的标注体验。它可以在当前页面激活，注入或启用透明覆盖层，收集用户绘制内容，并协调截图捕获。

### Content Script

Content script 会运行在当前页面上下文中。它可以管理标注覆盖层、记录 pointer events、收集视口元数据，并检查标注区域附近的 DOM 元素。

### Background Service Worker

Background service worker 可以处理扩展级能力，例如截图捕获、消息路由，以及 content script 与 popup 或 side panel 之间的协调。

### Popup 或 Side Panel

Popup 或 side panel 可以提供激活标注模式、清除绘制、输入说明、导出 JSON 和复制 AI prompts 的控制能力。

### Canvas 标注覆盖层

透明 canvas 覆盖层可以记录红色目标标注和蓝色期望形状绘制，同时不永久改变底层网页。

### Payload Builder

Payload builder 会把截图、标注、视口元数据、滚动位置、URL、页面标题、DOM 候选元素、选定 computed styles 和用户说明组合成结构化 JSON payload。

### DOM/CSS Context Extractor

Extractor 可以使用 `elementsFromPoint`、bounding-box sampling、selector generation、`outerHTML` extraction 和 selected computed style capture 等方式。目标不是完美地把像素映射到源码文件，而是提供目标 UI 附近的有用上下文。

### 可选本地 Node.js Bridge

未来的本地 bridge 可以把浏览器插件连接到本地项目文件夹。这将支持源码搜索、候选组件检测，以及带用户审批的受控补丁生成。

### AI Coding Agent 集成

DesignPointer 可以为 Codex、Claude Code、Cursor 或其他 AI coding agents 导出模型无关的 payload 和 prompt 模板。直接集成应保持可选，以保证核心概念的可移植性。

## 为什么第一版不直接做自动代码修改？

第一版不应直接修改代码，因为仅靠浏览器插件并不能可靠访问本地源码仓库。

在没有本地源码仓库访问权限的情况下，插件只能从截图和 DOM 中推断变化。这有价值，但不足以安全地生成和应用补丁。

自动 patch 需要本地项目访问、框架认知、文件映射和用户审批。它还需要清晰的审查流程，让用户在应用前检查修改。

第一步真正有价值的事情，是准确捕获视觉意图。当项目能够可靠表达用户想要什么之后，后续版本再探索本地 agent bridge 和受控 patch 工作流会更稳妥。
