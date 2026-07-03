# 产品需求 (CN)

> Language: CN | [EN](product-requirements_EN.md)

## 产品目标

DesignPointer 旨在帮助开发者通过真实网页上的可视化标注，把精确的局部 UI 修改意图传达给 AI coding agents。

## 目标用户

- 使用 AI coding agents 的前端开发者
- 参与 AI 辅助编码工作流的设计师
- 使用 Vibe Coding 构建 UI 的独立开发者
- 经常迭代前端细节的产品构建者

## 核心用户故事

作为开发者，我希望能在网页上指向某个具体 UI 区域，并直接画出期望的修改效果，这样 AI coding agent 就能准确理解我要修改什么。

## 主要工作流

1. 用户打开一个网页。
2. 用户激活 DesignPointer。
3. 页面上出现透明标注层。
4. 用户用红色标记目标区域。
5. 用户用蓝色绘制期望的参考形状或位置。
6. 用户添加一条简短说明。
7. DesignPointer 捕获页面上下文和标注信息。
8. DesignPointer 生成结构化 payload 和 AI prompt。
9. 用户把 payload 发送给 AI coding agent。
10. AI 返回前端修改建议或代码补丁。

## MVP 范围

第一版实现应支持：

- 仅当前视口
- 手动可视化标注
- 红色目标区域
- 蓝色期望参考绘制
- 文本说明
- 截图捕获
- 带标注截图生成
- 视口元数据
- devicePixelRatio
- 滚动位置
- URL 和页面标题
- 标注点数据
- 边界框
- 附近 DOM/CSS 提取
- JSON payload 导出
- AI prompt 生成

## MVP 不包含

- 自动修改代码
- 全页面截图
- 类 Figma 图层识别
- 复杂 DOM diff
- 多人协作
- 历史记录管理
- 源码仓库补丁应用
- 自动框架识别
- Canvas 内部对象识别

## 成功标准

- 用户可以清楚标记需要修改的内容。
- 用户可以用视觉方式展示期望的变化。
- 导出的 payload 包含足够上下文，使 AI coding agent 能理解请求。
- 相比只使用文字或截图，AI 输出更准确。

## 功能需求

- 插件应在当前网页上提供标注模式。
- 标注层应保留页面下方内容，不永久修改页面 DOM。
- 用户应至少能创建两种语义标注角色：目标区域和期望视觉参考。
- 目标区域默认使用红色。
- 期望参考绘制默认使用蓝色。
- 用户应能输入简短自然语言说明。
- payload 应保留基于 viewport CSS pixels 的坐标。
- payload 应包含足够元数据，使坐标系统可解释。
- 在安全可行的情况下，payload 应包含附近 DOM/CSS 上下文。

## 非目标

- DesignPointer 不打算成为完整设计工具。
- DesignPointer 不打算替代 issue tracker 或设计评审工作流。
- DesignPointer 第一版不打算自动应用代码修改。
- DesignPointer 不打算在没有本地项目访问权限的情况下推断完整源码结构。
