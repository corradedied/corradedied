### Groupbox Resize, Rotating Chevron & KeyPicker Action Menu

**What changed**
- `Groupbox:Resize()` tweens size instead of snapping; `Groupbox:SetCollapsed()` tweens the collapse arrow's rotation instead of snapping.
- `AddContextMenu`'s open/close tween now accepts an `AnimationFlag` (defaults to `"Dropdown"`, unchanged for existing menus) so different menus can animate independently.
- The keypicker's action-type menu (Always/Toggle/Hold) now opens/closes with its own tween via a new `KeyPickerMenu` flag.
- Fixed `List == 1` context menus (keypicker menu included) not actually animating: their `ScrollingFrame` uses `AutomaticSize.Y`, which overrides any tween on that axis. Now `AutomaticSize` is temporarily disabled and driven manually for the duration of the open/close tween, then restored.
- New flags: `Library.Animations.GroupboxResize`, `RotatingChevron`, `KeyPickerMenu` (all default `false`, opt-in), settable via `Library:CreateWindow({ Animations = { ... } })`.

**Why**
- These UI elements resized/rotated/opened in a single frame, which felt abrupt next to the rest of the animated UI. Bringing them in line required generalizing the shared menu code so each menu type can have its own tween instead of being hardcoded to `Dropdown`, and fixing a conflict between `AutomaticSize` and Size tweens that was silently no-op'ing the keypicker menu's animation.
