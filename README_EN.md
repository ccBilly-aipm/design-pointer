# DesignPointer (EN)

> Language: EN | [CN](README_CN.md)

Point at the UI. Draw what you want. Let AI understand the change.

DesignPointer is an open-source browser extension concept for AI-assisted frontend development. It helps developers communicate precise visual UI changes to AI coding agents by annotating live web pages with target regions, reference drawings, screenshots, coordinates, viewport data, and nearby DOM/CSS context.

## Problem

AI coding agents are becoming useful for frontend development, but they still struggle with vague visual instructions.

Developers often say things like:

- "Make this line a bit more curved."
- "Move this card slightly to the left."
- "Make this section feel less rigid."
- "Change this shape to look more like this."

Text is often too vague. Screenshots help, but screenshots alone do not tell the AI exactly where the issue is, what the user wants to change, what the desired visual result looks like, or which DOM/CSS element might be involved.

DesignPointer aims to solve this missing layer between human visual intent and AI code generation.

## Idea

DesignPointer adds a visual annotation layer on top of the current webpage.

The user can:

1. Mark the target area in red.
2. Draw the desired visual reference in blue.
3. Add a short natural-language instruction.
4. Export a structured AI payload containing screenshots, annotations, coordinates, viewport data, scroll position, URL, and nearby DOM/CSS context.

The AI coding agent can then use this richer context to understand what to modify and produce better frontend code suggestions or patches.

## Core Concept

DesignPointer is not a design tool.

DesignPointer is not a screenshot annotation tool.

DesignPointer is a visual intent layer for AI frontend coding.

It helps AI coding agents answer three questions:

1. What exact part of the UI is the user talking about?
2. What does the user want it to become?
3. What page, viewport, coordinate system, and nearby DOM/CSS context should be used to understand the change?

## Initial Scope

This repository currently documents the product concept, requirements, data structure, and development roadmap.

No MVP implementation is included yet.

The first implementation phase will likely focus on:

- Chrome Extension Manifest V3
- A transparent annotation overlay
- Red target annotations
- Blue desired-shape drawings
- Current viewport screenshot capture
- Coordinate export based on viewport CSS pixels
- Nearby DOM/CSS context extraction
- AI prompt and JSON payload generation

## Status

This project is in the early concept and planning stage.

The repository is created first to reserve the project name and document the product direction.

## Documentation

- [Problem Statement](docs/problem-statement_EN.md)
- [Product Requirements](docs/product-requirements_EN.md)
- [AI Payload Schema](docs/ai-payload-schema_EN.md)
- [Roadmap](docs/roadmap_EN.md)
- [Architecture Notes](docs/architecture-notes_EN.md)

## License

MIT
