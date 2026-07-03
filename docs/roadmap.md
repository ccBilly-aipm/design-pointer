# Roadmap

## Phase 0: Repository Bootstrap

Goal: Reserve the project name and document the concept.

Deliverables:

- GitHub repository
- README
- License
- Problem statement
- Product requirements
- AI payload schema
- Roadmap

## Phase 1: Browser Overlay Prototype

Goal: Build a minimal browser overlay for visual annotation.

Deliverables:

- Chrome Extension Manifest V3
- Content script
- Transparent canvas overlay
- Floating toolbar
- Red target annotation
- Blue reference drawing
- Clear and undo actions

## Phase 2: Screenshot and Payload Export

Goal: Capture the current viewport and export structured data.

Deliverables:

- Current viewport screenshot
- Annotated screenshot
- Viewport metadata
- devicePixelRatio
- Scroll position
- Annotation JSON export

## Phase 3: DOM/CSS Context Extraction

Goal: Collect nearby DOM and computed CSS context around the selected region.

Deliverables:

- elementsFromPoint sampling
- Nearby element detection
- Selector generation
- outerHTML extraction
- computedStyle extraction
- boundingClientRect capture

## Phase 4: AI Prompt Builder

Goal: Convert screenshot, annotation, and DOM context into a high-quality AI coding prompt.

Deliverables:

- Prompt template
- JSON payload formatter
- Copy-to-clipboard export
- Optional model-specific prompt formats

## Phase 5: Local Agent Bridge

Goal: Connect DesignPointer with local AI coding agents.

Deliverables:

- Local Node.js bridge
- Project folder connection
- Source file search
- Candidate component detection
- AI patch request

## Phase 6: Patch Generation and Review

Goal: Let AI produce code changes and allow users to review them before applying.

Deliverables:

- Diff preview
- Patch application
- User approval flow
- Rollback support
