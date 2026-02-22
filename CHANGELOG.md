# Changelog

## v0.1.0 (unreleased)

### Added
- GPU kernel emitters: ui_clear, ui_rect, ui_text
- Widget tree with parallel array storage
- Dark theme (8 semantic colors)
- Dirty flag system (frame-level render skipping)
- Render pipeline (VM dispatch chain — single vkQueueSubmit per frame)
- CPU layout engine (column, row containers with spacing/padding)
- Widgets: box, text, button, row, column
- Win32 platform layer with DWM dark mode and rounded corners
- Teal octopus window icon (16x16 pixel art)
- Reactive state management (value-binding with auto text updates)
- Press-to-click buttons (fires on mouse-down for instant response)
- Smart sleep (only when idle — zero latency on interaction frames)
- Separator widget (2px horizontal line in border color)
- Progress bar widget (track + fill, bind to reactive state)
- Checkbox widget (toggle with label, click or programmatic)
- Text input widget (single-line, keyboard input, cursor, focus system)
- Slider widget (horizontal drag, configurable min/max, value display)
- Focus system (click-to-focus, shared state in tree.flow)
- Keyboard input support (ui_key_pressed, ui_key_down)
- Mouse state queries (ui_mouse_x, ui_mouse_y, ui_mouse_down)
- Multi-level layout nesting (reverse-order Pass 1 for correct sizing)
- Text width auto-update on reactive state change (re-runs layout)
- Hit test helper function (ui_hit_test)
- Radio button group widget (mutually exclusive selection)
- Label widget (dimmed label + colored value pair)
- Tab key navigation (cycles focus through all focusable widgets)
- Focus border highlight (2px primary-color border on focused widget)
- Space/Enter keyboard activation for focused buttons
- Space key toggles focused checkboxes and radio buttons
- Enter key submission for text inputs (ui_textinput_submitted)
- Arrow key control for focused sliders (Left/Right adjusts value)
- 10 widget types: box, text, button, row, column, checkbox, textinput, slider, radio, label
- Full keyboard accessibility (Tab + Space + Enter + arrows)
- Examples: hello, counter, dashboard, timer, form, settings
- Documentation: quickstart, architecture, widgets (all widgets + keyboard)
- Tests: 18/18 passing (12 tree + 6 kernel)
