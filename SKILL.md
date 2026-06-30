---
name: jd-motion-language
version: "1.1.0"
description: This skill should be used when translating a motion design intent into the JD WeChat-domain motion language. It provides the coordinate system, motion patterns, duration tables, easing curves, and composition rules for platform UI and campaign interactions. Use it as the parameterization layer after the jd-motion-principles skill (or a similar twelve-principles foundation) has established the scene character and emotional direction. It is designed to work in tandem with jd-motion-principles for JD WeChat-domain motion workflows.
author: honghaoxiang
agent_created: true
trigger:
  - 京东动效
  - 京东微信域动效
  - 京东动效语言
  - 京东运动语言
  - JD动效
  - 京东界面动效
---

# 京东微信域界面动效语言

## Core Philosophy

- Use a shared coordinate system (X, Y, Z) so every motion is described in the same spatial language.
- Choose a motion pattern first, then pick duration and easing. Do not start with a curve.
- Keep platform scenes functional and fast; keep campaign scenes expressive and deliberate.
- Treat duration and easing as part of the brand voice. The same transition feels different at 140 ms vs. 480 ms.
- This skill gives parameters, not principles. Pair it with a 12-principles motion foundation skill for judgment and review.

## When to Use

Use this skill when:
- Designing or implementing motion for JD WeChat-domain products.
- Converting a motion requirement into concrete duration, easing, and axis choices.
- Writing a prompt for an execution skill that outputs Lottie JSON, CSS, Motion, or GSAP.
- Reviewing whether an existing animation follows the JD motion language.

Do not use this skill for:
- Deciding whether motion is needed at all. That is a UX/product decision.
- 3D/shader effects beyond scale-based Z simulation.
- Non-JD products unless explicitly adapting the language.

## Coordinate System

All motion is described in X, Y, Z:

| Axis | Direction | Notes |
|------|-----------|-------|
| X | Horizontal left/right | Primary axis for lateral switches, carousels, tab transitions. |
| Y | Vertical up/down | Primary axis for sheets, banners, dropdowns, gravity-driven motion. |
| Z | Perpendicular to screen (depth) | Usually simulated with scale; may use real 3D transforms when supported. |

Rules:
- A single-axis motion should have a clear reason for that axis.
- Prefer Z (scale) for emergence/dismissal of floating layers.
- Prefer X or Y for spatial continuity between states.

## Motion Types

| Type | Scope | Examples |
|------|-------|----------|
| Micro | Element-level feedback | Button press, icon toggle, input shake, like burst, delete confirmation. |
| Macro | Component-level or above | Sheet slide, page push, container morph, banner drop, page transition. |

Match the duration table to the type and scene.

## Motion Patterns

Choose exactly one pattern for each transition:

| Pattern | Trigger | Typical Use |
|---------|---------|-------------|
| Axis motion | A spatial relationship exists between before and after states | Tab switch (X/Y), sheet enter/exit (Y), popup scale (Z). |
| Container morph | Shared content transforms into a child or related state | Card expands to detail page, search bar expands to results. |
| Fade in/out | No logical progression between the two states | Unrelated elements appearing or disappearing independently. |

Rules:
- Do not combine axis motion and fade for the same element unless one is a background layer.
- For container morph, preserve the shared element's identity; do not let it disappear and reappear.

## Scene Classification

The language splits every requirement into one of two scenes:

| Scene | Goal | Character |
|-------|------|-----------|
| Platform | Efficiency, clarity, low friction | Fast, restrained, no elastic. |
| Campaign | Delight, engagement, brand expression | Slower, expressive, elastic allowed. |

Determine the scene before choosing any parameter.

## Duration Tables

### Platform Scene

| Element / Motion | Duration |
|------------------|----------|
| Micro transform or fade in/out | 100 ms |
| Component micro transform or fade in/out | 200 ms |
| Component element axis motion | 140 ms |
| Popup/dialog scale (Z) | 140 ms |
| Sheet slide up/down (Y) | 140 ms |
| Dropdown menu | 140 ms |
| Container morph | 200 ms |
| Page-level transition | 200 ms |

### Campaign Scene

| Element / Motion | Duration |
|------------------|----------|
| Micro transform or fade in/out | 100 ms |
| Component micro transform or fade in/out | 200 ms |
| Component element axis motion | 140–240 ms |
| Popup/dialog scale (Z) | 360–480 ms |
| Sheet slide up/down (Y) | 360–480 ms |
| Dropdown menu | 240 ms |
| Banner | 360 ms |
| Ambient entrance effect | 0–800 ms |
| Container morph | 240–360 ms |

Rules:
- For campaign, choose the shorter end when the motion is a response to user action; choose the longer end for ambient or staged reveals.
- Never exceed 1000 ms for UI feedback. Entrance ambience may approach 800 ms but should feel like background, not blocking.

## Easing Tables

### Platform Scene

| Duration | Allowed Easing | Notes |
|----------|---------------|-------|
| ≤ 200 ms | `linear` | Short functional motions read as immediate. |
| > 200 ms | `cubic-bezier(0.66, 0, 0.34, 1)` | Smooth acceleration and deceleration. |
| Element entering/leaving viewport | `linear` | Avoid drama for viewport transitions. |

Platform rules:
- Do not use elastic easing.
- Do not use `ease-in` for entrances or `ease-out` for exits.

### Campaign Scene

| Axis | Duration | Primary Easing | Alternative |
|------|----------|----------------|-------------|
| X or Y | 100–360 ms | `cubic-bezier(0.66, 0, 0.34, 1)` | `elastic-bezier(0.47, 0.20, 0.41, 1.37)` |
| X or Y | > 360 ms | `cubic-bezier(0.66, 0, 0.34, 1)` | — |
| Z (scale) | 100–200 ms | `cubic-bezier(0.66, 0, 0.34, 1)` | — |
| Z (scale) | 200–360 ms | `elastic-bezier(0.47, 0.20, 0.41, 1.37)` | — |
| Z (scale) | > 360 ms | `cubic-bezier(0.84, 0, 0.16, 1)` | — |

Campaign rules:
- Elastic is allowed only for Z-axis scale or small XY overshoots.
- For long scale motions (> 360 ms), use the dramatic cubic curve.
- For elements entering or leaving the viewport, prefer `linear` unless the element is part of a staged campaign reveal.

## Axis-Specific Rules

### X Axis
- Use for lateral continuity: tabs, carousels, step indicators.
- Single-axis X motion should feel like a sliding panel, not a bouncing object.
- In platform scenes, keep X motion strictly linear or cubic; no elastic.

### Y Axis
- Use for vertical gravity: sheets, banners, dropdowns, toasts.
- Upward motion should decelerate; downward motion should accelerate to feel natural.
- For campaign banners, allow a slight overshoot on settle.

### Z Axis
- Use for depth/emergence: dialogs, popups, tooltips, badges.
- Prefer scale simulation. Real 3D is optional and should degrade gracefully.
- Small Z pops (badges, toasts) should be fast (100–140 ms).
- Large Z reveals (campaign dialogs) can be slower (360–480 ms) with elastic.

## Composition Rules

### Path Order
- Continuity-driven content uses smooth paths that respect gravity and reading direction.
- Do not make elements exit the viewport only to re-enter for a layout change.

### XY Dual Axis
- For staged campaign motion, use curved paths rather than straight lines.
- Y-axis acceleration should be gentle at the start and steeper near the end.
- Avoid adding a second axis purely for decoration.

### XY Single Axis
- Non-campaign single-axis motion must not use elastic easing.
- Do not introduce a second axis if the content relationship is single-dimensional.

### XY Dual-Axis Grid Motion
- When reordering grid items, move each item along the shortest straight path to its new cell.
- Preserve spatial proximity; do not cross paths in a way that swaps identities.

### Platform Loading
- Prefer skeleton screens over spinners for content loading.
- After content loads, introduce primary content before secondary content.
- Limit guided highlights to one occurrence per session.

### Campaign Staging
- Build a clear beat structure: prepare → release → follow-through.
- Let the primary element move first, secondary elements trail, and ambient elements settle last.
- Do not let decorative particles steal attention from the main message.

## Mapping to Lottie / CSS / Motion / GSAP

This skill does not prescribe framework syntax. Pass the output to an execution skill with these fields:

```json
{
  "scene": "platform | campaign",
  "motion_pattern": "axis | morph | fade",
  "axis": "X | Y | Z",
  "type": "micro | macro",
  "duration_ms": 140,
  "easing": "linear | cubic | elastic | dramatic-cubic",
  "primary_element": "...",
  "secondary_elements": ["..."],
  "ambient_elements": ["..."],
  "notes": "..."
}
```

Execution skill maps:
- `cubic` → `cubic-bezier(0.66, 0, 0.34, 1)`
- `elastic` → `elastic-bezier(0.47, 0.20, 0.41, 1.37)`
- `dramatic-cubic` → `cubic-bezier(0.84, 0, 0.16, 1)`

## Integration with Motion-Principles Skill

When paired with a 12-principles foundation skill, use this order:

1. Foundation skill decides the scene character and emotional intent.
2. This skill picks the JD-specific coordinate system, pattern, duration, and easing.
3. Execution skill renders the final animation.
4. Foundation skill reviews the result against anti-patterns.

This skill is the parameterization layer; the foundation skill is the judgment layer.

## References

Load these references when more detail is needed:

- `references/timing-table.md` — Complete platform/campaign duration matrix.
- `references/easing-table.md` — Curve definitions and permitted combinations.
- `references/axis-mapping.md` — XYZ axis usage and common component mappings.
- `references/composition-rules.md` — Expanded composition and staging rules.
- `references/framework-mapping.md` — How the JSON output maps to common animation frameworks.

## Anti-Patterns

- Choosing a curve before choosing a motion pattern.
- Using elastic easing in a platform scene.
- Using a single duration for every element in a campaign animation.
- Animating unrelated elements in perfect synchrony.
- Letting decorative motion compete with the primary action.
- Ignoring the difference between X, Y, and Z semantics.
- Applying dramatic cubic curves to micro interactions.
