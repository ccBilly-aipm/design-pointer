# AI Payload Schema (CN)

> Language: CN | [EN](ai-payload-schema_EN.md)

本文档描述一种初始的结构化 payload 格式，用于把可视化 UI 修改意图传达给 AI coding agents。

Payload 应结合页面元数据、截图、用户标注、附近 DOM/CSS 上下文、自然语言说明和输出预期。

## 示例 Payload

```json
{
  "page_context": {
    "url": "https://example.com",
    "title": "Example Page",
    "viewport": {
      "width": 1440,
      "height": 900,
      "devicePixelRatio": 2
    },
    "scroll": {
      "x": 0,
      "y": 320
    },
    "screenshot": "base64-or-file-reference",
    "annotated_screenshot": "base64-or-file-reference"
  },
  "annotations": [
    {
      "id": "target_1",
      "role": "target",
      "label": "Area to change",
      "color": "red",
      "type": "lasso",
      "points": [
        { "x": 412, "y": 238 },
        { "x": 456, "y": 241 },
        { "x": 488, "y": 260 }
      ],
      "bbox": {
        "x": 408,
        "y": 230,
        "width": 95,
        "height": 48
      }
    },
    {
      "id": "reference_1",
      "role": "desired_shape",
      "label": "Desired visual reference",
      "color": "blue",
      "type": "path",
      "points": [
        { "x": 420, "y": 250 },
        { "x": 445, "y": 258 },
        { "x": 472, "y": 247 },
        { "x": 500, "y": 266 }
      ],
      "bbox": {
        "x": 420,
        "y": 247,
        "width": 80,
        "height": 19
      }
    }
  ],
  "dom_context": {
    "nearby_elements": [
      {
        "selector": "#hero-line path:nth-child(1)",
        "tag": "path",
        "outerHTML": "<path d=\"M10 20 C40 10, 80 10, 120 20\" />",
        "boundingClientRect": {
          "x": 400,
          "y": 220,
          "width": 120,
          "height": 60
        },
        "computedStyle": {
          "stroke": "#999999",
          "strokeWidth": "2px"
        }
      }
    ]
  },
  "user_instruction": "Make the red highlighted line follow the blue reference shape while keeping the original color, thickness, and style.",
  "output_expectation": {
    "type": "code_suggestion",
    "requirements": [
      "Only modify the UI element related to the red target region.",
      "Keep the original design style.",
      "Prefer minimal code changes.",
      "If the target element is uncertain, provide candidate elements and explain the uncertainty."
    ]
  }
}
```

## 字段说明

### page_context

包含创建标注时的网页信息。

- `url`: 当前页面 URL。帮助 AI 理解正在讨论的路由或页面状态。
- `title`: 当前文档标题。
- `viewport`: 以 CSS pixels 表示的可见浏览器视口。
- `viewport.width`: 视口宽度，单位为 CSS pixels。
- `viewport.height`: 视口高度，单位为 CSS pixels。
- `viewport.devicePixelRatio`: 浏览器 device pixel ratio。用于在截图像素和 CSS 坐标之间建立对应关系。
- `scroll`: 当前页面滚动偏移。
- `scroll.x`: 横向滚动偏移，单位为 CSS pixels。
- `scroll.y`: 纵向滚动偏移，单位为 CSS pixels。
- `screenshot`: 未标注视口截图的 base64 图像或文件引用。
- `annotated_screenshot`: 渲染了用户标注的截图 base64 图像或文件引用。

### annotations

包含用户创建的可视化标注。

- `id`: 标注的稳定标识符。
- `role`: 标注的语义用途。早期预期值包括 `target` 和 `desired_shape`。
- `label`: 标注的人类可读标签。
- `color`: 可见标注颜色。红色表示目标区域，蓝色表示期望参考。
- `type`: 标注几何类型，例如 `lasso`、`path`、`rectangle` 或 `arrow`。
- `points`: 按顺序记录的坐标点，单位为 viewport CSS pixels。
- `bbox`: 标注周围的边界框，单位为 viewport CSS pixels。
- `bbox.x`: 边界框左侧坐标。
- `bbox.y`: 边界框顶部坐标。
- `bbox.width`: 边界框宽度。
- `bbox.height`: 边界框高度。

### dom_context

包含附近页面结构，帮助 AI 把视觉目标映射到真实 UI 元素。

- `nearby_elements`: 选中或标注区域附近的候选 DOM 元素列表。
- `selector`: 可帮助定位元素的生成 selector。
- `tag`: DOM 标签名。
- `outerHTML`: 元素标记的紧凑表示。
- `boundingClientRect`: 元素在 viewport CSS pixels 中的位置和尺寸。
- `computedStyle`: 与视觉修改相关的部分 computed CSS 属性。

### user_instruction

用户的自然语言请求。它应简短、直接，并与可视化标注配合使用。

### output_expectation

描述 AI coding agent 应返回什么。

- `type`: 期望响应类型，例如 `code_suggestion`、`patch` 或 `analysis`。
- `requirements`: 对 AI 响应的约束。它们可以引导 agent 给出最小、聚焦、可审查的修改。

## 坐标系统

所有标注点和边界框都应使用 viewport CSS pixels，而不是原始截图像素。`devicePixelRatio` 用于帮助下游工具在 CSS 坐标和图像像素之间进行映射。

## 隐私说明

未来实现应在导出截图、DOM 内容或页面文本前考虑脱敏控制。有些网页可能包含私人用户数据、凭据、内部产品信息或客户内容。
