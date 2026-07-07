### Input/textbox focus border

`TextBox` elements (main `Input`, and the ColorPicker's Hue/RGB boxes) now tween their `UIStroke.Color` between `OutlineColor` → `AccentColor` on `Focused`/`FocusLost`, using the existing `Library.TweenInfo` (0.1s).

Text inputs previously had no visual acknowledgment of focus state beyond the blinking cursor — easy to lose track of which box you're typing in, especially with several stacked in a groupbox. Reusing `AccentColor`/`Library.TweenInfo` ties it to the same visual language already used for toggles/sliders instead of introducing a new color or timing.

**Why is this not behind an `Animations` flag?** that table only gates larger structural transitions (window show/hide, tab switching, dropdown expand) where there's a meaningful "instant" fallback state to snap to. This is a one-property color tween on a native input event, same class as the existing unconditional hover/toggle tweens (e.g. `Toggle:Display`) — not a distinct animation sequence worth its own opt-out.

### Dropdown & menu item hovering

**What changed:** Added hover tweens (`Library.TweenInfo`) to the Dropdown value list, the KeyPicker's mode-select buttons, and the ColorPicker's right-click menu (Copy/Paste color, Copy Hex, Copy RGB) — background and text transparency shift on `MouseEnter`/`MouseLeave`.

**Why:** These list-style menu items had no hover feedback, unlike buttons and checkboxes elsewhere in the library. Same tween timing as the checkbox/toggle hover keeps selecting from any list feeling consistent across the UI.



# PR
Title:
feat: input borders, dropdown list option tween, and add selection tweens for other menus
