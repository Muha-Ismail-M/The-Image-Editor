# The Image Editor

The Image Editor is a modern, browser-based **image editing prototype** built with **React + TypeScript**. It focuses on a clean “upload → adjust → preview → export” workflow, with a polished UI for **advanced adjustments**, **quick presets**, **history (undo/redo)**, and a **layers panel** (visibility, opacity, blend modes, ordering).

All editing runs locally in the browser using the HTML5 Canvas rendering pipeline—no backend required.

---

## What you can do

### Upload & start editing fast
- Drag-and-drop or browse to upload an image.
- Works as a single-page editing experience designed for quick iteration.

### Professional-style adjustments (sliders)
Includes a rich set of adjustment controls such as:
- Brightness, contrast, saturation, hue
- Blur
- Rotation and scale
- Exposure, highlights, shadows
- Vibrance, warmth, tint
- Vignette and film grain
- Sharpen (UI + parameter support)

### Quick presets
One-click looks like:
- Vintage, B&W, Vibrant, Soft, Dramatic, Film  
These presets apply a curated set of slider values to quickly change the “feel” of an image.

### Non-destructive edit history
- Maintains a timeline of adjustments using **undo/redo stacks**.
- A dedicated History panel lets you jump back to earlier states and reset to the original.

### Layers panel (editing workflow + foundation for compositing)
A Layers panel UI supports:
- Add, duplicate, delete layers
- Reorder layers (drag-and-drop)
- Visibility toggle, locking
- Opacity control
- Blend mode selection (normal, multiply, screen, overlay, etc.)

> Note: In the current version, adjustments are applied through the main canvas pipeline. The layers panel is designed as a strong UI foundation for extending the editor into true multi-layer compositing.

### Canvas controls (preview like a real editor)
- Zoom in/out + zoom percentage display
- Pan/drag the canvas
- Fit-to-screen toggle
- Grid / rule-of-thirds overlay
- “Hold to show original” preview mode

### Export & local save
- Export the current canvas as a high-quality PNG.
- Save a “project snapshot” to browser local storage (so you can persist your last saved state on the same device/browser).

---

## How it works (high level)

### Editing pipeline
- The editor renders the image to an HTML `<canvas>` and applies adjustments using:
  - Canvas `ctx.filter` (for brightness/contrast/saturation/blur/hue, etc.)
  - Additional pixel-level effects for things like grain and vignette
- Transforms (rotation/scale) are applied using canvas transform operations before drawing.

### State model
- The UI maintains a single “settings” object for all adjustments.
- Undo/redo is handled by keeping previous settings states in stacks.
- Layers are tracked as structured objects (id, name, visibility, opacity, blend mode), making the editor easy to extend.

### Local-first by design
- No server, no database, no account system required.
- Optional “Save” writes the current rendered image + settings into `localStorage`.

---

## Tech stack

- React + TypeScript
- Vite
- Tailwind CSS
- lucide-react (icons)

---

## Repository structure (where to look first)

This repo contains the Vite project inside:

- `The Image Editor/project/`
  - `src/components/ImageEditor.tsx` — main editor orchestration (upload, settings, filter application, export/save, history)
  - `src/components/Sidebar.tsx` — sliders + presets UI
  - `src/components/Canvas.tsx` — zoom/pan/grid/original-preview canvas wrapper
  - `src/components/LayersPanel.tsx` — layers UI and layer management logic
  - `src/components/HistoryPanel.tsx` — history timeline + jump-to-state UI
  - `src/components/FileUpload.tsx` — drag-and-drop upload experience

---

## Known limitations (current state)

- Some tools shown in the toolbar (e.g., brush/eraser/text/shapes) are primarily **UI scaffolding** and can be wired into real drawing/text/shape rendering as a next step.
- Layer controls are implemented as a strong UI + data model; full pixel-level compositing across layers can be added later.
- Project persistence is currently local-only (browser storage). Refresh/device changes may require reloading assets depending on browser behavior.

---

## Roadmap ideas (high-impact upgrades)

- True multi-layer compositing (render layers into a single final canvas using blend modes + opacity)
- Crop tool that outputs a new canvas/image state (not just an overlay)
- Brush/eraser tool with stroke smoothing + adjustable hardness/opacity
- Text tool and shapes tool as real canvas layers
- Import/export project files (not only localStorage)
- Export formats (JPG/WebP) and quality controls

---

## License

No license file is currently included. 
