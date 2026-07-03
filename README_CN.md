# DesignPointer (CN)

> Language: CN | [EN](README_EN.md)

指向 UI，画出你想要的样子，让 AI 理解这次修改。

## 项目简介

DesignPointer 是一个面向 AI 前端开发工作流的开源浏览器插件概念项目。

它的目标是帮助开发者在真实网页上直接标注局部 UI 修改意图，并把目标区域、参考绘制、截图、坐标、视口信息以及附近 DOM/CSS 上下文整理成结构化 payload，交给 AI coding agent 理解和修改代码。

简单说：当你觉得“这条线再弯一点”“这个卡片往左一点”“这个形状更像我画的这样”很难用语言描述时，DesignPointer 让你直接在页面上指给 AI 看。

## 问题

AI coding agents 正在变得越来越适合辅助前端开发，但它们仍然很难理解模糊的视觉修改需求。

开发者经常会说：

- “让这条线再弯一点。”
- “把这个卡片稍微往左移。”
- “让这个区域不要这么生硬。”
- “把这个形状改得更像这个参考。”

这些需求人眼很容易理解，但用文字表达往往不够精确。截图可以表达大概区域，但截图本身并不能告诉 AI：

- 用户具体在说页面上的哪一块？
- 用户希望它变成什么样？
- 这个修改对应哪个坐标、视口、滚动位置？
- 附近可能相关的 DOM/CSS 元素是什么？

DesignPointer 试图补上“人类视觉意图”和“AI 代码生成”之间缺失的一层。

## 核心想法

DesignPointer 会在当前网页上增加一个可视化标注层。

用户可以：

1. 用红色标出需要修改的目标区域。
2. 用蓝色画出期望的视觉参考。
3. 添加一句简短的自然语言说明。
4. 导出包含截图、标注、坐标、视口数据、滚动位置、URL 和附近 DOM/CSS 上下文的结构化 AI payload。

AI coding agent 可以基于这些更丰富的信息，更准确地理解需要修改的 UI 局部，并生成更可靠的前端代码建议或补丁。

## 核心定位

DesignPointer 不是一个设计工具。

DesignPointer 不是一个普通截图标注工具。

DesignPointer 是一个面向 AI 前端编码的视觉意图层。

它帮助 AI coding agents 回答三个关键问题：

1. 用户说的到底是 UI 的哪一部分？
2. 用户希望它变成什么样？
3. AI 应该基于什么页面、视口、坐标系统和附近 DOM/CSS 上下文来理解这次修改？

## 当前范围

这个仓库目前用于记录项目概念、产品需求、数据结构和开发路线图。

当前不包含 MVP 实现。

第一阶段实现可能会聚焦于：

- Chrome Extension Manifest V3
- 透明页面标注层
- 红色目标区域标注
- 蓝色期望形状绘制
- 当前视口截图捕获
- 基于 viewport CSS pixels 的坐标导出
- 附近 DOM/CSS 上下文提取
- AI prompt 和 JSON payload 生成

## 当前状态

本项目仍处于早期概念和规划阶段。

这个仓库会先用于保留项目名，并清晰记录产品方向。

## 文档

- [问题陈述](docs/problem-statement_CN.md)
- [产品需求](docs/product-requirements_CN.md)
- [AI Payload Schema](docs/ai-payload-schema_CN.md)
- [路线图](docs/roadmap_CN.md)
- [架构说明](docs/architecture-notes_CN.md)

## License

MIT
