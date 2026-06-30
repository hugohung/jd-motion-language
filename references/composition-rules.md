# Composition Rules

## Path Order

- Continuity-driven transitions should follow smooth, readable paths.
- Respect gravity: downward motion accelerates; upward motion decelerates.
- Avoid making an element leave the viewport just to re-enter at a new position. Move it directly.

## XY Dual-Axis Motion

- Campaign scenes may use curved arcs instead of straight lines.
- Y acceleration should be gentle at the start and steeper near the end.
- Do not add a second axis unless the content relationship supports it.

## XY Single-Axis Motion

- Platform single-axis motion must use `linear` or `cubic` only.
- Campaign single-axis motion may use `elastic` only for small overshoots at the end.
- Do not introduce a second decorative axis.

## Grid Reordering

- When grid items reorder, move each item along the shortest straight path to its new cell.
- Preserve spatial proximity so users can track individual items.
- Avoid path crossings that make items appear to swap identities.

## Platform Loading

- Prefer skeleton screens over spinners for content loads.
- After content loads, introduce primary content before secondary content.
- Limit guided highlights to one per session to avoid fatigue.

## Campaign Staging

- Structure campaign motion in beats:
  1. **Prepare** — hint, anticipation, or entrance of stage.
  2. **Release** — main action or reveal.
  3. **Follow-through** — secondary elements settle, ambient particles trail.
- Primary element moves first; secondary elements trail; ambient elements settle last.
- Decorative motion must not compete with the main message.

## Layering

| Layer | Role | Timing |
|-------|------|--------|
| Primary | Main subject or action | Leads the motion. |
| Secondary | Supporting information | Trails primary by a small offset. |
| Ambient | Background atmosphere | Settles last, may loop. |

Do not let secondary or ambient layers move faster or longer than the primary layer.
