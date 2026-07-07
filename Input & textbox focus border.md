### Input/textbox focus border

**What changed:** `TextBox` elements (main `Input`, and the ColorPicker's Hue/RGB boxes) now tween their `UIStroke.Color` between `OutlineColor` → `AccentColor` on `Focused`/`FocusLost`, using the existing `Library.TweenInfo` (0.1s).

**Why:** Text inputs previously had no visual acknowledgment of focus state beyond the blinking cursor — easy to lose track of which box you're typing in, especially with several stacked in a groupbox. Reusing `AccentColor`/`Library.TweenInfo` ties it to the same visual language already used for toggles/sliders instead of introducing a new color or timing.

**Not behind an `Animations` flag:** that table only gates larger structural transitions (window show/hide, tab switching, dropdown expand) where there's a meaningful "instant" fallback state to snap to. This is a one-property color tween on a native input event, same class as the existing unconditional hover/toggle tweens (e.g. `Toggle:Display`) — not a distinct animation sequence worth its own opt-out.
