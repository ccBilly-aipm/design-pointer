# Problem Statement (EN)

> Language: EN | [CN](problem-statement_CN.md)

AI-assisted coding has made it easier to generate, refactor, and modify frontend code. However, frontend UI work is often visual, local, and subtle. The hard part is not always writing the code. The hard part is communicating the exact visual intent to an AI coding agent.

Developers and product builders can usually see what feels wrong in a UI. A line may need to be more curved. A card may need to move slightly. A section may need better spacing. A shape may need to follow a different contour. These changes are easy to recognize with the human eye, but difficult to describe precisely in natural language.

Text instructions are often under-specified. Phrases like "move it a little left" or "make this feel softer" depend on the viewer's interpretation. AI coding agents may understand the broad request, but they often lack enough spatial context to identify the exact target, the expected visual outcome, or the relevant DOM and CSS.

Screenshots improve the situation, but screenshots alone are still incomplete. A screenshot can show the approximate area of interest, but it does not provide structured coordinates, viewport dimensions, scroll position, device pixel ratio, annotation intent, or nearby DOM/CSS context. The AI sees pixels, but not enough of the user's intent.

Frontend polish often lives in tiny details:

- Line curvature
- Spacing and rhythm
- Position and alignment
- Edges and outlines
- Shape direction
- Visual hierarchy
- Local layout balance

These details are frequently too specific for text and too contextual for screenshots alone.

DesignPointer proposes a missing layer between human visual intent and AI code generation: structured visual intent. Instead of asking users to describe every detail in words, DesignPointer lets them point at the live UI, mark the target area, draw a desired reference, and export a payload that combines annotations, screenshots, coordinates, viewport metadata, and nearby DOM/CSS context.

The goal is not to replace designers, developers, or AI coding agents. The goal is to make communication between them more precise. When the AI knows what part of the UI is being discussed, what visual change is desired, and what page context surrounds it, frontend code suggestions can become more accurate and easier to review.
