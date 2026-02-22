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
- Examples: hello, counter (Phase 1 acceptance test)
- Documentation: quickstart, architecture, widgets
- Tests: 18/18 passing (12 tree + 6 kernel)
