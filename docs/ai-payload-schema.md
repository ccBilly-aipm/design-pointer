# AI Payload Schema

This document describes an initial structured payload format for communicating visual UI modification intent to AI coding agents.

The payload should combine page metadata, screenshots, user annotations, nearby DOM/CSS context, a natural-language instruction, and output expectations.

## Example Payload

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

## Field Reference

### page_context

Contains information about the webpage where the annotation was created.

- `url`: The current page URL. This helps the AI understand which route or page state is being discussed.
- `title`: The current document title.
- `viewport`: The visible browser viewport in CSS pixels.
- `viewport.width`: The viewport width in CSS pixels.
- `viewport.height`: The viewport height in CSS pixels.
- `viewport.devicePixelRatio`: The browser device pixel ratio. This helps reconcile screenshot pixels with CSS pixel coordinates.
- `scroll`: The current page scroll offset.
- `scroll.x`: Horizontal scroll offset in CSS pixels.
- `scroll.y`: Vertical scroll offset in CSS pixels.
- `screenshot`: A base64 image or file reference for the unannotated viewport screenshot.
- `annotated_screenshot`: A base64 image or file reference for the screenshot with user annotations rendered on top.

### annotations

Contains visual annotations created by the user.

- `id`: A stable identifier for the annotation.
- `role`: The semantic purpose of the annotation. Expected early values include `target` and `desired_shape`.
- `label`: A human-readable label for the annotation.
- `color`: The visible annotation color. Red indicates the target area. Blue indicates the desired reference.
- `type`: The annotation geometry type, such as `lasso`, `path`, `rectangle`, or `arrow`.
- `points`: Ordered coordinate points in viewport CSS pixels.
- `bbox`: The bounding box around the annotation in viewport CSS pixels.
- `bbox.x`: Left coordinate of the bounding box.
- `bbox.y`: Top coordinate of the bounding box.
- `bbox.width`: Width of the bounding box.
- `bbox.height`: Height of the bounding box.

### dom_context

Contains nearby page structure that may help the AI map the visual target to real UI elements.

- `nearby_elements`: A list of candidate DOM elements near the selected or annotated region.
- `selector`: A generated selector that can help locate the element.
- `tag`: The DOM tag name.
- `outerHTML`: A compact representation of the element markup.
- `boundingClientRect`: The element's position and size in viewport CSS pixels.
- `computedStyle`: Selected computed CSS properties relevant to the visual change.

### user_instruction

The user's natural-language request. This should be short, direct, and paired with the visual annotations.

### output_expectation

Describes what the AI coding agent should return.

- `type`: The expected response type, such as `code_suggestion`, `patch`, or `analysis`.
- `requirements`: Constraints for the AI response. These can guide the agent toward minimal, focused, reviewable changes.

## Coordinate System

All annotation points and bounding boxes should use viewport CSS pixels, not raw screenshot pixels. The `devicePixelRatio` value is included so downstream tools can map between CSS coordinates and image pixels when needed.

## Privacy Notes

Future implementations should consider redaction controls before exporting screenshots, DOM content, or page text. Some web pages may contain private user data, credentials, internal product information, or customer content.
