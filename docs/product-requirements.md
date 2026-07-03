# Product Requirements

## Product Goal

DesignPointer aims to help developers communicate precise local UI modification intent to AI coding agents through visual annotations on live web pages.

## Target Users

- Frontend developers using AI coding agents
- Designers who work with AI-assisted coding workflows
- Indie hackers building UI with Vibe Coding
- Product builders who frequently iterate frontend details

## Core User Story

As a developer, I want to point at a specific UI area and draw the desired change directly on the webpage, so that an AI coding agent can understand exactly what I want to modify.

## Main Workflow

1. User opens a webpage.
2. User activates DesignPointer.
3. A transparent annotation layer appears.
4. User marks the target region in red.
5. User draws the desired reference shape or position in blue.
6. User adds a short instruction.
7. DesignPointer captures page context and annotations.
8. DesignPointer generates a structured payload and AI prompt.
9. User sends the payload to an AI coding agent.
10. AI returns a frontend modification suggestion or code patch.

## MVP Scope

First implementation should support:

- Current viewport only
- Manual visual annotations
- Red target region
- Blue desired reference drawing
- Text instruction
- Screenshot capture
- Annotated screenshot generation
- Viewport metadata
- devicePixelRatio
- Scroll position
- URL and page title
- Annotation point data
- Bounding boxes
- Nearby DOM/CSS extraction
- JSON payload export
- AI prompt generation

## Out of Scope for MVP

- Automatic code modification
- Full-page screenshot
- Figma-style layer detection
- Complex DOM diff
- Multi-user collaboration
- History management
- Source-code repository patching
- Automatic framework detection
- Canvas internal object recognition

## Success Criteria

- User can clearly mark what needs to change.
- User can visually show the desired change.
- The exported payload contains enough context for an AI coding agent to understand the request.
- The AI output becomes more accurate than using text or screenshot alone.

## Functional Requirements

- The extension should provide an annotation mode on top of the current webpage.
- The annotation layer should preserve the page underneath without permanently modifying the page DOM.
- Users should be able to create at least two semantic annotation roles: target and desired visual reference.
- Target annotations should use red by default.
- Desired reference drawings should use blue by default.
- Users should be able to enter a short natural-language instruction.
- The payload should preserve coordinates in viewport CSS pixels.
- The payload should include enough metadata to make the coordinate system interpretable.
- The payload should include nearby DOM/CSS context when it can be collected safely.

## Non-Goals

- DesignPointer is not intended to be a full design tool.
- DesignPointer is not intended to replace issue trackers or design review workflows.
- DesignPointer is not intended to apply code changes automatically in the first implementation.
- DesignPointer is not intended to infer the full source-code structure of an application without local project access.
