# OctoUI

GPU-native UI rendering engine for [OctoFlow](https://github.com/octoflow-lang/octoflow).

Renders entire UI frames via GPU VM dispatch chains — layout, render, composite as a single `vkQueueSubmit`. Written entirely in `.flow` files. Zero compiler changes.

## Architecture

```
vm_dispatch("ui_clear.spv", ...)     // clear framebuffer
vm_dispatch("ui_rect.spv", ...)      // per-widget rectangle
vm_dispatch("ui_text.spv", ...)      // per-glyph bitmap text
vm_build(vm) → single VkCommandBuffer
vm_execute(prog) → single vkQueueSubmit
vm_read_globals → R, G, B channels
window_draw(r, g, b)                 // present
```

All rendering happens on the GPU. The CPU only handles layout (tree constraint propagation) and input events.

## Quick Start

```bash
octoflow run examples/counter.flow --allow-read --allow-write --allow-ffi
```

## Structure

```
octoui/
  kernels/          SPIR-V emitters + compiled .spv kernels
  engine/           Core engine (tree, layout, pipeline)
  widgets/          Widget library (box, text, button, row, column)
  themes/           Color themes
  platform/         Platform-specific code (Win32)
  state/            Reactive state management
  examples/         Example applications
  tests/            Test suite
  docs/             Documentation
```

## Requirements

- OctoFlow compiler (octoflow.exe)
- Vulkan-capable GPU
- Windows (Win32 presentation)

## License

Apache 2.0 — see [LICENSE](LICENSE)
