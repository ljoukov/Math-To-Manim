# Layout Understanding in Math-To-Manim

Short answer: the system **nudges** the LLM to think about spatial layout, but there is **no hard spatial reasoning engine** or validator. Layout is prompt-driven.

## Where layout is explicitly instructed
- `src/agents/visual_designer.py`: requires a `layout` description plus `camera_movement`, `transitions`, and element lists; also passes previous-scene context to encourage continuity.
- `src/agents/narrative_composer.py`: asks for **positions**, colors, timing, and step-by-step “Begin by… Next…” staging.
- `src/app_claude.py`: prompt expander asks for **positions and sizes** in detailed prompts.
- `Gemini3/src/agents.py`: VisualDesigner demands a **Global Style** + storyboard; CodeGenerator forces **3D axes + camera moves**, affecting layout.
- `KimiK2Thinking/agents/enrichment_chain.py`: `VISUAL_DESIGN_TOOL` includes `layout`, `camera_movement`, `transitions`, and `animation_description`.

## What it does NOT do
- No explicit layout solver or spatial constraint engine.
- No formal coordinate schema or collision checking.
- No post-render correction loop based on frame analysis (video review is QA, not correction).

## Practical implication
The LLM is encouraged to describe layout and staging, but spatial consistency is **not enforced** by code. If you need stronger guarantees, add a structured layout schema (anchors/coordinates) plus a validator or post-processor.
