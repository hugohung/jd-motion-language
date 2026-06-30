# Easing Tables

## Curve Definitions

| Token | CSS / Lottie Equivalent | Character |
|-------|------------------------|-----------|
| `linear` | `linear` | Mechanical, immediate, no acceleration. |
| `cubic` | `cubic-bezier(0.66, 0, 0.34, 1)` | Balanced acceleration and deceleration; smooth and neutral. |
| `elastic` | `elastic-bezier(0.47, 0.20, 0.41, 1.37)` | Bouncy, playful, attention-seeking. |
| `dramatic-cubic` | `cubic-bezier(0.84, 0, 0.16, 1)` | Strong slow start and fast finish; cinematic. |

## Platform Scene

| Duration | Curve | Example |
|----------|-------|---------|
| ≤ 200 ms | `linear` | Button feedback, icon toggle, micro fade. |
| > 200 ms | `cubic` | Sheet slide, page transition, container morph. |
| Element enters/leaves viewport | `linear` | List item removal, infinite scroll. |

Platform restrictions:
- Do not use `elastic`.
- Do not use `dramatic-cubic`.
- Avoid `ease-in` for entrances and `ease-out` for exits.

## Campaign Scene

| Axis | Duration | Recommended Curve | Notes |
|------|----------|-------------------|-------|
| X or Y | 100–360 ms | `cubic` | Default for smooth campaign motion. |
| X or Y | 100–360 ms | `elastic` | Optional for small overshoots or playful moments. |
| X or Y | > 360 ms | `cubic` | Longer motions should not bounce. |
| Z (scale) | 100–200 ms | `cubic` | Fast emergence. |
| Z (scale) | 200–360 ms | `elastic` | Medium reveal with bounce. |
| Z (scale) | > 360 ms | `dramatic-cubic` | Large staged reveal. |

Campaign restrictions:
- Use `elastic` sparingly; never on long XY motions.
- Prefer `dramatic-cubic` only for large Z reveals (> 360 ms).
- Keep viewport enter/exit `linear` unless part of a staged campaign sequence.

## Common Mistakes

- Using `elastic` for error states or destructive actions.
- Using `dramatic-cubic` for micro feedback.
- Using `linear` for long, large transitions (> 200 ms) in campaign scenes.
