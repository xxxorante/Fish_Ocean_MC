# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Pixel Bay (像素海湾)** — A single-page interactive prototype simulating the Hanauma Bay underwater ecosystem in 16-bit Minecraft pixel art style. Built with Pixi.js v8 and vanilla JavaScript, bundled with Vite.

Key docs: `PRD.md` (full product requirements), `tech-stack.md` (technology decisions).

## Tech Stack

- **Language:** JavaScript (ES6+) — no TypeScript
- **Rendering:** Pixi.js v8 (WebGL 2D, `pixelArt: true` for nearest-neighbor scaling)
- **Animation:** GSAP (optional, for easing/elastic effects)
- **Build:** Vite (dev server + production bundler)
- **Architecture:** "Modern Vanilla Web" — no React/Vue framework

## Build & Dev Commands

```bash
npm install          # Install dependencies
npm run dev          # Start Vite dev server with hot reload
npm run build        # Production build
npm run preview      # Preview production build locally
```

## Project Structure (Planned)

```
index.html              # Entry point
src/
  main.js               # App init: create Pixi Application, load assets, spawn entities
  entities/
    Fish.js             # Fish class: swimming, direction flip, bubble spawning
    Bubble.js           # Bubble particle: float upward and fade
  data/
    fish-data.json      # Fish metadata (12 species, names, descriptions)
  utils/                # Helpers (random range, etc.)
public/assets/
  sprites/              # Fish pixel art PNGs
  scene/                # Background, sea lantern textures
  ui/                   # Border frame, tooltip assets
```

## Core Application Logic

- **Initialization:** Randomly select 6 of 12 fish species per page load, distribute vertically to avoid overlap.
- **Fish behavior:** Horizontal swimming (left-right), randomized speed (0.5x–1.5x), auto-flip sprite based on direction, intermittent bubble emission from mouth.
- **Interaction:** Hover (desktop) / tap (mobile) highlights fish and shows a pixel-style tooltip with Chinese name, English name, and a one-line fun fact.
- **Scene elements:** Turquoise gradient background (#40E0D0 → #008B8B), sea lantern blocks with glow animation, fishing rod border frame.

## Pixi.js Patterns

Initialize with pixel art mode enabled:
```javascript
import { Application, Sprite } from 'pixi.js';
const app = new Application();
await app.init({ resizeTo: window, pixelArt: true });
document.body.appendChild(app.canvas);
```

Pixi v8 has built-in pointer event detection on sprites — use `sprite.eventMode = 'static'` and `sprite.on('pointerover', ...)` for hover/click interactions instead of manual hit-testing.
