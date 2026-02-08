# CLAUDE.md - AI Assistant Guide for Pixel Bay (Fish_Ocean_MC)

## Project Overview

**Pixel Bay - Hanauma Prototype** (像素海湾 - 恐龙湾场景原型) is a web-based interactive pixel-art ocean ecosystem visualization. It simulates a tropical coral reef scene inspired by Hawaii's Hanauma Bay, featuring animated pixel fish, Minecraft-inspired visual elements, and hover/tap interactions.

**Current status:** Design specification phase. The repository contains a bilingual (Chinese/English) development proposal (`proposal_1`) but no implementation code yet.

**Deliverable:** A runnable demo page (HTML/Canvas or widget prototype) with dynamic fish animations and interaction feedback.

## Repository Structure

```
Fish_Ocean_MC/
├── CLAUDE.md            # This file - AI assistant guide
├── proposal_1           # Development requirements specification (bilingual CN/EN)
└── (no source code yet)
```

### Planned Structure (from proposal)

```
Fish_Ocean_MC/
├── index.html           # Entry point
├── assets/
│   └── fish/            # Pixel sprite sheets (12 species)
├── src/                 # Application source code
└── data/
    └── fish_pool.json   # Fish database configuration
```

## Technology Stack

The proposal recommends **Option A (Canvas-based)**:

- **HTML5 Canvas** as the rendering surface
- **Pixi.js** or **Phaser** as the 2D rendering / game engine
- Chosen for smooth pixel animations, particle effects, and cross-platform support

Alternative (Option B): Pure CSS3 Animation + DOM nodes (lighter but limited for particle effects and many fish).

No build system, package manager, or framework has been chosen yet. When implementation begins, expect a Node.js/npm project setup with one of the above engines.

## Key Design Specifications

### Visual Style
- **Art style:** 16-bit or 32-bit pixel art
- **Color palette:** High saturation, bright tropical colors
- **Water gradient:** Turquoise `#40E0D0` to Dark Cyan `#008B8B`
- **Scene:** Sunny shallow tropical sea, sandy bottom, pixelated coral reef

### Minecraft-Inspired Elements (Required)
- **Sea Lanterns** on the ocean floor with soft glow effects
- **Seagrass / coral blocks** with wool/terracotta material feel
- **Fishing Rod UI frame** - border styled as fishing line, with a pixel rod handle in a corner

### Fish Database
12 species are defined, 6 randomly selected per page load:

| ID | Name (CN) | Name (EN) | Rarity |
|----|-----------|-----------|--------|
| 01 | 斜带吻棘鲀 | Reef Triggerfish | common |
| 02 | 黄高鳍刺尾鱼 | Yellow Tang | common |
| 03 | 角镰鱼 | Moorish Idol | common |
| 04 | 横带刺尾鱼 | Convict Tang | common |
| 05 | 阿基里斯刺尾鱼 | Achilles Tang | common |
| 06 | 五彩鹦嘴鱼 | Parrotfish | common |
| 07 | 小米蝴蝶鱼 | Milletseed Butterflyfish | common |
| 08 | 长嘴蝴蝶鱼 | Longnose Butterflyfish | common |
| 09 | 管口鱼 | Trumpetfish | common |
| 10 | 箱鲀 | Boxfish | common |
| 11 | 绿海龟 | Green Sea Turtle | **rare** |
| 12 | 孔雀比目鱼 | Flowery Flounder | common |

### Animation Requirements
- Fish swim left-right across screen at random speeds (0.5x - 1.5x)
- Z-depth layering for occlusion (fish behind coral/seagrass)
- Pixel bubble particles from fish mouths, floating upward and growing before disappearing

### Interaction Requirements
- **Desktop:** Mouse hover highlights fish with edge glow / brightness increase
- **Mobile:** Tap triggers the same highlight
- **Tooltip:** Pixel-styled info box showing Chinese name, English name, and a fun fact

### Data Model
```json
{
  "id": "f01",
  "name": "斜带吻棘鲀",
  "name_en": "Reef Triggerfish",
  "rarity": "common",
  "sprite_sheet": "assets/fish/triggerfish.png",
  "description": "夏威夷州鱼，遇到危险会躲进岩缝锁住背鳍。"
}
```

## Development Workflow

### Getting Started
No implementation exists yet. When starting development:
1. Initialize a Node.js project (`npm init`)
2. Install the chosen rendering engine (e.g., `npm install pixi.js`)
3. Set up an `index.html` entry point with a Canvas element
4. Create the fish data JSON from the proposal's 12-species table

### Branching
- Development branches follow the pattern `claude/<description>-<session-id>`
- Commit messages should be clear and descriptive

### Testing
No test framework is configured yet. When adding tests:
- Visual/rendering tests may require canvas snapshot testing
- Interaction logic should have unit tests for hover detection, fish selection, tooltip display
- Animation logic (speed randomization, Z-depth ordering) should be unit-testable

### CI/CD
No CI/CD pipeline exists. To be set up as the project matures.

## Conventions for AI Assistants

1. **Bilingual support:** The project uses Chinese for content/data and English for code/technical terms. Maintain this pattern.
2. **Pixel art fidelity:** All visual implementations must respect the 16/32-bit pixel art constraint. Avoid smooth gradients or anti-aliased graphics on game elements.
3. **Minecraft references:** Sea Lanterns, fishing rod frame, and block-style vegetation are mandatory design elements, not optional.
4. **Proposal is the source of truth:** Until implementation begins, `proposal_1` defines all requirements. Reference it for any design questions.
5. **6-from-12 randomization:** Each page load must randomly select 6 fish from the full pool of 12. This is a core mechanic.
6. **Performance awareness:** The Canvas approach was chosen specifically for performance with many animated sprites and particles. Keep this in mind when making implementation decisions.
7. **Mobile-first interactions:** Support both hover (desktop) and tap (mobile) from the start. Do not build desktop-only interactions.
