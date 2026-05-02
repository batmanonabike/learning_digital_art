# Learning Digital Art — Game Asset Pipeline

Personal documentation library for mastering the tools and workflow used to create game assets for **Beellionaire** (bee-themed slot game) and future projects.

---

## Toolchain Overview

### Art Tools

| Tool | Platform | Role in Pipeline |
|---|---|---|
| **Procreate** | iPad + Apple Pencil | Concept art, character sketching, texture painting |
| **Affinity Designer** | Mac + Windows PC | Vector UI, slot frames, icons, sprite cleanup — vectors scale to any resolution with clean lines; export to PSD for compatibility with other tools |
| **Affinity Photo** | Mac + Windows PC | Raster compositing, texture editing, image prep |
| **Affinity Publisher** | Mac + Windows PC | Paytables, help screens, multi-page layout |
| **Spine 2D** | Mac / Windows | Character rigging, skeletal animation, runtime export |

### Game Tech Stack

| Technology | Role |
|---|---|
| **TypeScript** | Primary language throughout |
| **Svelte / SvelteKit** | App shell, routing, UI overlays (paytable, settings, win screens) |
| **Phaser 3** | Game canvas, scene management, rendering, input |
| **Spine Phaser Plugin** (`@esotericsoftware/spine-phaser`) | Loads and plays Spine skeletal animations at runtime |

---

## Asset Pipeline

```
1. CONCEPT (Procreate / iPad)
   Sketch characters, environments, UI layouts
   ↓
2. CLEAN ART (Procreate + Affinity Designer)
   Refine linework, build vector UI elements, paint textures
   ↓
3. PREP FOR RIGGING (Affinity Designer/Photo)
   Slice characters into named parts (body, wings, head, etc.)
   Export individual PNGs at correct resolution
   ↓
4. RIG & ANIMATE (Spine 2D)
   Assemble skeleton, weight meshes, create animation states
   Export: .atlas + .json/.skel + spritesheet
   ↓
5. ENGINE INTEGRATION (Phaser + SvelteKit)
   Load .skel + .atlas via Phaser asset pipeline
   Wire Spine animation states to slot game logic (SpineGameObject)
   SvelteKit UI overlays (paytable, win screens) sit outside Phaser canvas
```

---

## Hardware

| Device | Primary Use |
|---|---|
| iPad + Apple Pencil | Procreate — sketching, painting |
| M1 Mac | Affinity Suite, Spine 2D (primary workstation) |
| Windows Laptop | Affinity Suite, Spine 2D, game engine integration |

## iPad File Transfer and Asset Store

Getting work off the iPad quickly is a regular part of the workflow. **Google Drive** is the chosen cloud store — cross-platform, already tied to the existing Google account, 15GB free, and easy folder sharing with collaborators.

**Transfer workflow:**

```
iPad  --AirDrop-->  Mac (working files in Google Drive folder)
                            |
                    Google Drive syncs automatically in background
                            |
                    Windows laptop (same folder via Google Drive for Desktop)
                    Collaborators (share folder by email)
```

| Transfer | Method |
|---|---|
| iPad → Mac (daily) | **AirDrop** — instant, zero friction |
| Mac → cloud (backup + sync) | **Google Drive for Desktop** — asset folder syncs automatically |
| Windows access | **Google Drive for Desktop** — folder appears as a local drive |
| Sharing with collaborators | Share Google Drive folder by email (no Google account required to view) |
| Large files / offline | **USB-C direct** — iPad → Mac via Finder |

**Export formats from Procreate:**

| Format | Use case |
|---|---|
| `.procreate` | Archive — preserves all layers, Procreate-only |
| **PSD** | Best for handoff to Affinity — layers fully intact |
| **PNG (flat)** | Final flattened asset ready for Phaser or Spine |
| **PNG (per layer)** | Share > Layers exports a zip of individual layer PNGs |

---

## Project: Beellionaire

A bee-themed slot game. All tutorials and worked examples in this library use Beellionaire assets as the reference subject.

**Asset types needed:**
- Bee characters (idle, win, react animations)
- Honeycomb and hive environment backgrounds
- Reel window frame and slot chrome (vector)
- Symbol icons (bees, queen, hive, honey jar, flowers, playing card suits)
- UI buttons, paytable, win overlays
- Particle effects (pollen, sparkle, coin burst)

**Spine animation states per character:**
`idle` · `win_small` · `win_big` · `intro` · `react`

---

## Documentation Index

### Procreate
- [01 — Canvas Setup for Game Assets](docs/procreate/01-canvas-setup.md)
- [02 — Layer Structure for Character Art](docs/procreate/02-layer-structure.md)
- [03 — Exporting from Procreate: Formats and When to Use Each](docs/procreate/03-exporting.md)
- [04 — Transferring Files from iPad to Mac and Windows](docs/procreate/04-file-transfer.md)

### Affinity Designer
- [01 — Why Vector? Clean Lines, Scaling, and PSD Export](docs/affinity-designer/01-why-vector.md)
- [02 — Document Setup and Personas](docs/affinity-designer/02-document-setup.md)
- [03 — Vector UI: Slot Frame Walkthrough](docs/affinity-designer/03-slot-frame.md)
- [04 — Slicing Characters for Spine](docs/affinity-designer/04-slicing-for-spine.md)
- [05 — Export Persona and Batch Export](docs/affinity-designer/05-export-persona.md)

### Affinity Photo
- [01 — Texture Editing and Compositing](docs/affinity-photo/01-texture-editing.md)

### Spine 2D
- [01 — Project Setup and Image Import](docs/spine2d/01-project-setup.md)
- [02 — Rigging a Bee Character](docs/spine2d/02-rigging-bee.md)
- [03 — Animation States for Slot Games](docs/spine2d/03-animation-states.md)
- [04 — Mesh Deformation and IK](docs/spine2d/04-mesh-and-ik.md)
- [05 — Exporting for Game Engines](docs/spine2d/05-exporting.md)

### Phaser 3
- [01 — Project Setup with SvelteKit](docs/phaser/01-project-setup.md)
- [02 — Loading Spine Assets in Phaser](docs/phaser/02-loading-spine-assets.md)
- [03 — SpineGameObject and Animation States](docs/phaser/03-spine-game-object.md)
- [04 — Slot Reel Logic and Scene Structure](docs/phaser/04-reel-logic.md)
- [05 — Texture Atlases and Asset Management](docs/phaser/05-texture-atlases.md)

### SvelteKit / UI
- [01 — SvelteKit + Phaser Architecture](docs/sveltekit/01-architecture.md)
- [02 — UI Overlays over the Phaser Canvas](docs/sveltekit/02-ui-overlays.md)
- [03 — Paytable and Help Screen Layout](docs/sveltekit/03-paytable-layout.md)

### Workflow
- [Cross-Tool File Handoff Cheatsheet](docs/workflow/file-handoff.md)
- [Naming Conventions and Folder Structure](docs/workflow/naming-conventions.md)
- [Resolution and Canvas Size Reference](docs/workflow/resolution-reference.md)
- [Spine to Phaser Integration Cheatsheet](docs/workflow/spine-to-phaser.md)
- [Google Drive Asset Store Setup](docs/workflow/google-drive-setup.md)

---

## Doc Format

Each tutorial follows this structure:

```
# Title

> **Tool:** Procreate / Affinity Designer / Spine 2D / Phaser / SvelteKit
> **Level:** Beginner / Intermediate
> **Beellionaire context:** what this applies to in the game
> **Tech context:** relevant only for Phaser/SvelteKit docs — TS patterns, plugin versions, etc.

## Goal
What you will be able to do after this tutorial.

## Prerequisites
What you need to have done or know first.

## Steps
Numbered, screenshot-friendly steps.

## Tips
Non-obvious gotchas and shortcuts.

## Next
Link to the logical next tutorial.
```

---

## Key Conventions

- Canvas sizes are always **power-of-two** (512, 1024, 2048) unless layout requires otherwise
- Character parts exported as **individual PNGs with transparent backgrounds**
- Spine atlases packed at **2048×2048 max** unless targeting low-end mobile
- All file names use **kebab-case**: `bee-queen-body.png`, `reel-frame-base.afdesign`
- Layer/bone names are **descriptive and consistent** across tools: `wing-left`, `wing-right`, `antenna-left`, etc.
