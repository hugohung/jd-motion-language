# Axis Mapping

## Axis Semantics

| Axis | Spatial Meaning | Emotional Association |
|------|-----------------|----------------------|
| X | Lateral, side-to-side | Switching, browsing, pagination |
| Y | Vertical, up-and-down | Gravity, sheets, banners, scrolling |
| Z | Depth, forward-and-back | Emergence, focus, elevation |

## Common Component Mappings

### X Axis

| Component | Motion | Notes |
|-----------|--------|-------|
| Tabs | Slide content left/right | Content moves with the selected tab. |
| Carousel | Slide panels horizontally | Keep velocity constant or use `cubic`. |
| Stepper | Advance/retreat horizontally | Step content replaces previous content. |
| Swipe list item | Reveal actions on swipe | Actions slide in from the swipe direction. |

### Y Axis

| Component | Motion | Notes |
|-----------|--------|-------|
| Bottom sheet | Slide up/down | Use `cubic` in platform; may overshoot in campaign. |
| Dropdown | Expand list downward | List items may stagger in. |
| Banner | Drop from top/bottom | Campaign banners may use overshoot. |
| Toast | Slide up into view | Keep short; exit downward. |
| Pull-to-refresh | Pull down, snap back | Use spring-like behavior; respect release threshold. |

### Z Axis

| Component | Motion | Notes |
|-----------|--------|-------|
| Dialog | Scale up from center | Primary campaign dialog may be slow and elastic. |
| Popup/tooltip | Scale from trigger origin | Keep micro popups fast (100–140 ms). |
| Badge | Pop on update | Use elastic only for campaign badges. |
| FAB | Scale/elevation change | Platform FAB should be restrained. |

## Multi-Axis Rules

- XY dual-axis: use only when the content has both lateral and vertical relationships. Prefer curved paths in campaigns.
- XYZ: generally avoided. If an element moves in X/Y and scales in Z, treat Z as a separate layer (e.g., background dims while foreground slides).
- Never add an axis purely for visual interest.
