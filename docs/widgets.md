# OctoUI Widget Reference

## Widget Types

| Constant | Value | Description |
|----------|-------|-------------|
| UI_BOX | 1.0 | Colored rectangle |
| UI_TEXT | 2.0 | Text label |
| UI_BUTTON | 3.0 | Clickable button |
| UI_ROW | 4.0 | Horizontal container |
| UI_COLUMN | 5.0 | Vertical container |

## Core Widgets

### Box — `widgets/core/box.flow`

A simple colored rectangle.

```
use "octoui/widgets/core/box"

let rect = ui_box(parent, 100.0, 50.0, UI_COLOR_PRIMARY)
```

**Parameters:**
- `parent` — Parent widget ID (-1 for root-level)
- `w` — Width in pixels
- `h` — Height in pixels
- `color_idx` — Theme color index (UI_COLOR_*)

### Text — `widgets/core/text.flow`

A text label rendered with the bitmap font.

```
use "octoui/widgets/core/text"

let label = ui_text(parent, "HELLO", UI_COLOR_TEXT)
```

**Parameters:**
- `parent` — Parent widget ID
- `content` — Text string (uppercase recommended, lowercase maps to uppercase)
- `color_idx` — Theme color index for text color

**Auto-sizing:** Width = `len(content) * 10` pixels (at scale 2). Height = 16 pixels.

### Button — `widgets/input/button.flow`

A clickable button with hover and press visual states.

```
use "octoui/widgets/input/button"

let btn = ui_button(parent, 120.0, 40.0, "CLICK ME")

// In event loop:
if ui_button_clicked(btn) == 1.0
  // Handle click
end
```

**Parameters:**
- `parent` — Parent widget ID
- `w` — Width in pixels
- `h` — Height in pixels
- `label` — Button text (centered)

**Functions:**
- `ui_button_clicked(id)` — Returns 1.0 if button was clicked this frame
- `ui_button_clear_clicks()` — Clears per-frame click state (called by input system)
- `ui_button_update_visual(id)` — Updates button color based on state

**Click behavior:** Press-to-click (fires on mouse-down). The visual press state and any state updates render in the same frame for instant responsiveness.

**States:**
- Normal (0) — Surface color
- Hovered (1) — Hover color
- Pressed (2) — Active color

### Separator — `widgets/core/separator.flow`

A thin horizontal line for visual grouping between widgets.

```
use "octoui/widgets/core/separator"

let sep = ui_separator(parent, 300.0)  // 300px wide, 2px tall
```

**Parameters:**
- `parent` — Parent widget ID
- `w` — Width in pixels

Rendered as a 2px tall rectangle in the border color.

### Progress Bar — `widgets/core/progress.flow`

A horizontal progress bar with track and fill. Bind to a reactive state for automatic updates.

```
use "octoui/widgets/core/progress"

let pbar = ui_progress(parent, 300.0, 12.0)    // 300px wide, 12px tall
let pct_state = ui_state(50.0)                  // 50%
let _bp = ui_bind_progress(pbar, pct_state)     // Bind

// In event loop (after state changes):
let _pu = ui_progress_update()                  // Sync fill width
```

**Parameters:**
- `parent` — Parent widget ID
- `w` — Total width in pixels
- `h` — Height in pixels (typically 8-16)

**Functions:**
- `ui_bind_progress(track_id, state_id)` — Bind fill to reactive state (0.0 - 100.0)
- `ui_progress_update()` — Sync all progress bar fills to their bound states

The track renders in border color, the fill in primary color.

## Layout Widgets

### Column — `widgets/layout/column.flow`

Arranges children vertically.

```
use "octoui/widgets/layout/column"

let col = ui_column(parent, 10.0)  // 10px spacing between children
```

### Row — `widgets/layout/row.flow`

Arranges children horizontally.

```
use "octoui/widgets/layout/row"

let row = ui_row(parent, 20.0)  // 20px spacing between children
```

## Theme Colors

Defined in `themes/dark.flow`:

| Constant | Index | RGB | Description |
|----------|-------|-----|-------------|
| UI_COLOR_BG | 0 | (30, 30, 35) | Window background |
| UI_COLOR_SURFACE | 1 | (45, 45, 50) | Widget surface |
| UI_COLOR_PRIMARY | 2 | (90, 130, 240) | Primary accent |
| UI_COLOR_TEXT | 3 | (220, 222, 228) | Main text |
| UI_COLOR_TEXT_DIM | 4 | (140, 142, 148) | Dimmed text |
| UI_COLOR_BORDER | 5 | (80, 82, 88) | Borders |
| UI_COLOR_HOVER | 6 | (75, 78, 85) | Hover state |
| UI_COLOR_ACTIVE | 7 | (90, 130, 240) | Active/pressed |

## Reactive State

```
use "octoui/state/reactive"

let counter = ui_state(0.0)                // Create state
ui_bind_text(display_widget, counter)      // Bind to widget
ui_state_set(counter, ui_state_get(counter) + 1.0)  // Update
```

When `ui_state_set` changes a value, all bound widgets automatically update their text and the frame is marked dirty.

## Keyboard Input

```
use "octoui/platform/desktop/input"

// In event loop (after ui_poll_events):
if ui_key_pressed("escape") == 1.0
  // Escape key was pressed this frame
end

if ui_key_pressed("space") == 1.0
  // Space bar was pressed this frame
end

let key = ui_key_down()  // Get last key name (" " if none)
```

**Functions:**
- `ui_key_pressed(key)` — Returns 1.0 if key was pressed this frame
- `ui_key_down()` — Returns key name of last key-down event

**Key names:** `"escape"`, `"space"`, `"enter"`, `"a"`-`"z"`, `"0"`-`"9"`, etc.

## Tree Operations

Low-level tree functions (from `engine/tree.flow`):

```
ui_tree_add(type, parent, w, h, text)  // Add widget → returns ID
ui_tree_set_color(id, r, g, b)         // Set RGB color
ui_tree_set_text(id, text)             // Update text content
ui_tree_set_pos(id, x, y)             // Set position
ui_tree_set_size(id, w, h)            // Set size
ui_tree_set_spacing(id, spacing)      // Set container spacing
ui_tree_set_padding(id, padding)      // Set container padding
ui_tree_count()                        // Total widget count
ui_tree_is_container(id)              // Check if ROW or COLUMN
```
