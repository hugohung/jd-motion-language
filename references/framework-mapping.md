# Framework Mapping

This skill outputs a framework-agnostic motion description. The execution skill maps it to a specific framework.

## Output JSON Schema

```json
{
  "scene": "platform | campaign",
  "motion_pattern": "axis | morph | fade",
  "axis": "X | Y | Z",
  "type": "micro | macro",
  "duration_ms": 140,
  "easing": "linear | cubic | elastic | dramatic-cubic",
  "primary_element": "description",
  "secondary_elements": [],
  "ambient_elements": [],
  "stagger_ms": 0,
  "notes": "optional"
}
```

## Easing Token Mapping

| Token | CSS | Framer Motion | GSAP | Lottie (After Effects) |
|-------|-----|---------------|------|------------------------|
| `linear` | `linear` | `linear` | `none` | `Linear` |
| `cubic` | `cubic-bezier(0.66, 0, 0.34, 1)` | `[0.66, 0, 0.34, 1]` | `power2.inOut` | `Bezier(0.66, 0, 0.34, 1)` |
| `elastic` | `elastic-bezier(0.47, 0.20, 0.41, 1.37)` | spring config | `elastic.out(1, 0.5)` | Custom bezier approximating overshoot |
| `dramatic-cubic` | `cubic-bezier(0.84, 0, 0.16, 1)` | `[0.84, 0, 0.16, 1]` | `power4.inOut` | `Bezier(0.84, 0, 0.16, 1)` |

## Implementation Notes

- CSS transitions work best for simple state changes.
- Framer Motion is ideal for React components with layout animations.
- GSAP is best for complex campaign sequences and timeline control.
- Lottie is best for vector-based campaign illustrations exported from After Effects.
- The same motion description can drive any of these frameworks; the execution skill chooses based on the target platform.
