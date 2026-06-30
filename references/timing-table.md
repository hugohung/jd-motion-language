# Duration Tables

All durations are in milliseconds. Choose a scene first, then match the motion type.

## Platform Scene

Goal: efficiency and clarity. Motion should feel nearly instantaneous.

| Motion Type | Element | Duration |
|-------------|---------|----------|
| Fade in/out | Micro element | 100 ms |
| Fade in/out | Component element | 200 ms |
| Scale (Z) | Popup, dialog, tooltip | 140 ms |
| Slide Y | Sheet, dropdown, banner | 140 ms |
| Slide X | Tab switch, stepper | 140 ms |
| Axis motion | Component element | 140 ms |
| Container morph | Card → detail, search bar → results | 200 ms |
| Page transition | Full page push/replace | 200 ms |

## Campaign Scene

Goal: engagement and brand expression. Motion can be slower and more staged.

| Motion Type | Element | Duration |
|-------------|---------|----------|
| Fade in/out | Micro element | 100 ms |
| Fade in/out | Component element | 200 ms |
| Axis motion | Component element | 140–240 ms |
| Scale (Z) | Popup, dialog | 360–480 ms |
| Slide Y | Sheet, banner | 360–480 ms |
| Dropdown menu | Menu list | 240 ms |
| Banner | Top/bottom banner | 360 ms |
| Ambient entrance | Background atmosphere | 0–800 ms |
| Container morph | Hero card expansion | 240–360 ms |

## Selection Guidance

- User-initiated response → shorter end of the range.
- System-initiated or ambient reveal → longer end of the range.
- The same element should not change duration between visits unless the state changes.
- Micro feedback must stay at 100 ms regardless of scene.
