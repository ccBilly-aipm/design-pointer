# 路线图 (CN)

> Language: CN | [EN](roadmap_EN.md)

## Phase 0: Repository Bootstrap

目标：保留项目名并记录项目概念。

交付物：

- GitHub 仓库
- README
- License
- 问题陈述
- 产品需求
- AI payload schema
- 路线图

## Phase 1: Browser Overlay Prototype

目标：构建一个用于可视化标注的最小浏览器覆盖层原型。

交付物：

- Chrome Extension Manifest V3
- Content script
- 透明 canvas 覆盖层
- 浮动工具栏
- 红色目标区域标注
- 蓝色参考绘制
- 清除和撤销操作

## Phase 2: Screenshot and Payload Export

目标：捕获当前视口并导出结构化数据。

交付物：

- 当前视口截图
- 带标注截图
- 视口元数据
- devicePixelRatio
- 滚动位置
- 标注 JSON 导出

## Phase 3: DOM/CSS Context Extraction

目标：收集选中区域附近的 DOM 和 computed CSS 上下文。

交付物：

- elementsFromPoint 采样
- 附近元素检测
- selector 生成
- outerHTML 提取
- computedStyle 提取
- boundingClientRect 捕获

## Phase 4: AI Prompt Builder

目标：把截图、标注和 DOM 上下文转换成高质量 AI coding prompt。

交付物：

- Prompt 模板
- JSON payload 格式化器
- 复制到剪贴板导出
- 可选的模型专用 prompt 格式

## Phase 5: Local Agent Bridge

目标：把 DesignPointer 连接到本地 AI coding agents。

交付物：

- 本地 Node.js bridge
- 项目文件夹连接
- 源文件搜索
- 候选组件检测
- AI patch 请求

## Phase 6: Patch Generation and Review

目标：让 AI 生成代码修改，并让用户在应用前审查。

交付物：

- Diff 预览
- Patch 应用
- 用户审批流程
- 回滚支持
