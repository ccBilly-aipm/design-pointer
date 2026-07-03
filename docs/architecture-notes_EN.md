# Architecture Notes (EN)

> Language: EN | [CN](architecture-notes_CN.md)

DesignPointer is currently a planning-stage repository. This document outlines a possible future architecture without implementing the browser extension yet.

## Possible Future Technical Direction

- Chrome Extension Manifest V3
- Content script for page overlay
- Background service worker for screenshot capture
- Popup or side panel for controls
- Canvas overlay for annotations
- JSON payload builder
- DOM/CSS context extractor
- Optional local Node.js bridge
- Optional integration with Codex, Claude Code, Cursor, or other AI coding agents

## High-Level Components

### Browser Extension

The browser extension would provide the user-facing annotation experience. It would activate on the current page, inject or enable a transparent overlay, collect user drawings, and coordinate screenshot capture.

### Content Script

The content script would run inside the active page context. It could manage the annotation overlay, record pointer events, collect viewport metadata, and inspect nearby DOM elements around annotated regions.

### Background Service Worker

The background service worker could handle extension-level capabilities such as screenshot capture, message routing, and coordination between the content script and popup or side panel.

### Popup or Side Panel

A popup or side panel could provide controls for activating annotation mode, clearing drawings, entering instructions, exporting JSON, and copying AI prompts.

### Canvas Annotation Overlay

A transparent canvas overlay could record red target annotations and blue desired-shape drawings without permanently changing the underlying webpage.

### Payload Builder

The payload builder would combine screenshots, annotations, viewport metadata, scroll position, URL, page title, DOM candidates, selected computed styles, and the user's instruction into a structured JSON payload.

### DOM/CSS Context Extractor

The extractor could use methods such as `elementsFromPoint`, bounding-box sampling, selector generation, `outerHTML` extraction, and selected computed style capture. The goal is not to perfectly map pixels to source files, but to provide useful context around the likely UI target.

### Optional Local Node.js Bridge

A future local bridge could connect the browser extension to a local project folder. This would enable source-code search, candidate component detection, and controlled patch generation with user approval.

### AI Coding Agent Integrations

DesignPointer could export model-agnostic payloads and prompt templates for tools such as Codex, Claude Code, Cursor, or other AI coding agents. Direct integrations should remain optional so the core concept stays portable.

## Why Not Automatic Code Modification First?

The first version should not directly modify code because the browser extension alone does not have reliable access to the local source repository.

Without access to the local source repository, the extension can only infer changes from screenshots and DOM. That can be useful, but it is not enough to safely produce and apply patches.

Automatic patching requires local project access, framework awareness, file mapping, and user approval. It also needs a clear review flow so users can inspect changes before applying them.

The first useful step is to capture visual intent accurately. Once the project can reliably express what the user means, later versions can explore local agent bridges and controlled patch workflows.
