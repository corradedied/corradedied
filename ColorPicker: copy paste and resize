## ColorPicker: copy/paste buttons + resizable menu

- **Copy/Paste buttons in the popup menu** — Added "Copy color" / "Paste color" buttons directly inside the `ColorPicker`'s popup, sharing the same `Library.CopiedColor` state as the existing right-click menu. Right-click has no equivalent on touch screens, so mobile users previously had no way to copy/paste colors at all; this exposes the same functionality inline for them.
- **Resizable ColorPicker menu** — Added a drag handle to the bottom-right corner of the popup that scales the saturation/hue/alpha controls (140–320px). Added specifically for mobile: the fixed desktop-sized picker is a small, fiddly target on a phone screen, so this lets mobile users grow it to something they can actually see and drag accurately. Enabled by default via `Info.Resizable`, can be disabled per-picker.
```lua
LeftGroupBox:AddLabel("Color"):AddColorPicker("ColorPicker", {
	Default = Color3.new(0, 1, 0), -- Bright green
	Title = "colorpicker",
	Transparency = 0,
	Resizable = true, -- true/false

	Callback = function(Value)
		print("[cb] Color changed!", Value)
	end,
})
```
<img width="841" height="766" alt="image" src="https://github.com/user-attachments/assets/9f55160f-eb10-48ed-ae5a-e2634bd3e9e3" />
