# Generative 3D (NEXUS)

Generative-3D is a small **interactive 3D web experience** built with **Next.js** and **React Three Fiber**. It renders a full-screen scene (branded **NEXUS**) where a “crystal core”, orbiting satellites, and a reactive grid animate in real time and respond to your mouse movement—while you can orbit and zoom the camera.

This repo is best thought of as a **creative 3D landing page / portfolio hero**: minimal UI, high visual motion, and simple interactions.

---

## What you’ll see

- A full-screen 3D scene rendered in the browser
- A central “core” element that **floats, rotates, and pulses**
- Multiple “satellite” objects that **orbit** around the scene
- A grid-like field that **waves over time** and reacts to cursor proximity
- An on-screen overlay that explains the controls

---

## Controls

- **Move mouse** → influences the interactive elements
- **Drag** → orbit the camera
- **Scroll** → zoom in/out

---

## How it works (high level)

### Real-time animation loop
The scene uses a frame-by-frame render loop to update motion continuously. Animations are driven by time (elapsed seconds) plus normalized mouse coordinates.

### Mouse interaction model
Mouse movement is mapped into a normalized range (roughly `-1 → 1`) and used to influence:
- the core object’s position and rotation
- satellite orbit offsets
- the grid’s height displacement (strongest closest to the cursor)

### Performance-minded grid update
The grid is implemented as a set of points using typed arrays. Each frame updates only the **z-height** of each grid point to create:
- a base wave pattern
- a mouse-distance “bump” effect

The grid resolution is intentionally reduced to keep the scene responsive on typical laptops.

### Lighting & camera controls
The scene uses:
- an environment preset for fast, pleasing lighting
- orbit controls for a familiar “drag to rotate” camera interaction

---

## Tech stack

- **Next.js** (App Router)
- **React + TypeScript**
- **Three.js** via **@react-three/fiber**
- **@react-three/drei** for helpers (OrbitControls, Environment)
- **Tailwind CSS** (with CSS variables/theme tokens)
- **Geist fonts** for typography

The project is also configured for a shadcn-style component setup (aliases + theme tokens), making it easy to add UI panels later if you expand beyond a single-page experience.

---

## Project layout (where to look first)

- `app/page.tsx`  
  Main page + the entire 3D scene (core object, satellites, interactive grid, overlay UI)

- `app/layout.tsx`  
  Global layout + metadata + font wiring

- `app/globals.css`  
  Tailwind + theme tokens (CSS variables for light/dark styling)

- `lib/utils.ts`  
  Utility helper for composing Tailwind class names

---

## Current status

- The repository is a **single-scene interactive demo** (no backend, no database).
- It’s ideal as a base for:
  - a portfolio landing page
  - an interactive “brand intro” page
  - a Three.js / R3F learning project

---

## Practical next steps (nice upgrades)

- Add a small **settings panel** (toggle grid, adjust orbit speed, change colors)
- Add mobile-friendly interactions (touch input tuning)
- Add optional post-processing (bloom, vignette) for extra polish
- Replace primitives with custom models (GLTF) and add a loading state
- Tighten dependencies (the template includes many UI packages you may not need for a pure 3D scene)

---

## License

No license file is currently included.
