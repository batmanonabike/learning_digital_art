# Exporting from Procreate: Formats and When to Use Each

- **Tool:** Procreate
- **Level:** Beginner
- **Beellionaire context:** Every bee character, symbol icon, and painted texture starts in Procreate. Choosing the right export format determines whether downstream tools (Affinity, Spine, Phaser) get clean, usable files.

## Goal

Know which Procreate export format to use for each step in the pipeline, and export Beellionaire assets correctly the first time.

## Prerequisites

- A finished or in-progress Procreate canvas with named layers
- Basic familiarity with the Procreate interface

## The Core Formats

| Format | What you get | Use when |
|---|---|---|
| **Procreate** | Full archive — layers, blend modes, animation frames, brush strokes | Backup; never delete these |
| **PSD** | Layered file, Photoshop-compatible | Handing off to Affinity (any persona) |
| **PDF** | Vector-preserving (if using Procreate vector layers) | Rarely needed for game assets |
| **JPEG** | Flat, lossy | Reference images only — never for assets |
| **PNG** | Flat, lossless, transparent background | Final engine-ready asset (Phaser, Spine) |
| **Animated GIF / MP4** | Flattened animation preview | Quick previews only |
| **Animated PNG** | Frame-by-frame lossless animation | Not used in this pipeline — Spine handles animation |
| **Layered PNG** (Share > Layers) | One PNG per layer, zipped | Character parts when you need individual PNGs before Spine; secondary to PSD import |

For Beellionaire, you will use **Procreate + PSD + PNG** the most. Everything else is occasional.

## Steps

### 1. Open the Share sheet

Tap the **wrench icon** (top left) → **Share**. The export format list appears.

### 2. Export a Procreate backup

Before anything else, export a `.procreate` file and move it to `Google Drive/beellionaire-assets/source/`. This is your master archive. It preserves:

- All layers and groups
- Blend modes that may not survive PSD conversion
- Animation frames (if used)
- Timelapse recording

Do this every session. Storage is cheap; lost work is not.

### 3. Export PSD for Affinity handoff

Choose **PSD** when you are done with a piece and want to continue in Affinity.

What transfers well:
- Layer names and groups
- Normal and common blend modes
- Opacity values
- Masks

What may not transfer:
- Procreate-specific blend modes (check the result in Affinity before proceeding)
- Text layers (rasterised on export)

Save PSD files to `Google Drive/beellionaire-assets/source/`.

### 4. Export flat PNG for the engine

Choose **PNG** when an asset is finished and needs to go directly into Phaser or Spine as a texture.

- Background must be transparent — confirm in Procreate before export (checkerboard pattern = transparent)
- Use the full resolution of your canvas; resize in Affinity (Pixel persona) or at import time, not in Procreate
- Name the file in kebab-case before export: rename in Finder after AirDrop if Procreate uses the canvas name

Save flat PNGs to `Google Drive/beellionaire-assets/exports/`.

### 5. Hand off character parts to Spine

When a character (like the worker bee or queen bee) is ready to be rigged in Spine, you need each body part visible as a separate element. There are two ways to do this:

**Primary: Import PSD directly into Spine (recommended)**

Spine can read a `.psd` file natively via **File > Import > Import PSD**. It reads each layer as a separate image, names everything after the layer names, and positions parts relative to each other automatically — no manual splitting needed.

1. Export the character as **PSD** from Procreate and AirDrop it to Mac
2. In Spine, go to **File > Import > Import PSD**
3. Select the PSD — Spine creates a slot and image for each layer, preserving positions
4. Layer names from Procreate become slot/image names in Spine — get them right before exporting (`wing-left`, `wing-right`, `antenna-left`, etc.)

This is the faster path and preserves relative layer positions, which makes bone placement much easier.

**Alternative: Share > Layers (per-layer PNG zip)**

Use this when you need to inspect or modify individual part PNGs before Spine sees them, or when a PSD blend mode needs to be flattened in Affinity (Pixel persona) first.

1. Tap **Share > Layers** (scroll down past the format list in the Share sheet)
2. Procreate exports a `.zip` containing one PNG per layer
3. Unzip on Mac, move the folder to `Google Drive/beellionaire-assets/exports/bee-queen/`
4. Import the folder into Spine via **File > Import > Import Images**

Note: groups in Procreate are merged into a single PNG in the Layers export. If you need `wing-left` and `wing-right` as separate files, they must be ungrouped individual layers.

### 6. Choose resolution before exporting

Procreate exports at the canvas resolution. To check pixel dimensions: tap the **wrench icon** → **Canvas** → **Crop & Resize** — the current width and height are shown at the top. You don't need to commit to any change; just check the numbers and cancel.

**Target sizes for Beellionaire:**

| Asset type | Target resolution |
|---|---|
| Symbol icons (flat PNGs) | 512×512 px |
| Character body parts for Spine | 512–1024 px on the longest side per part |
| Backgrounds / full-scene textures | 2048×1024 or 2048×2048 |

**If the canvas is too large:** export at full resolution, then resize in Affinity (Pixel persona → Resize → Resize Document) before handing the asset to Spine or the atlas packer. Resize once, at full quality, before the asset enters any tool that bakes its dimensions. Do not resize multiple times — each resample degrades a raster image.

**If the canvas is too small:** redo it at a higher resolution in Procreate rather than upscaling. Upscaling raster art never recovers lost detail.

**Why resize before Spine specifically:** Spine records image dimensions at import. If you bring in a 2048px wing and later swap it for a 512px version, all bone placements and mesh weights will be at the wrong scale. Get it right before import.

## Format Decision Cheat Sheet

```
Finished session, nothing to hand off yet?
  → Export .procreate (backup)

Handing off to Affinity for cleanup or vector tracing?
  → Export PSD

Asset is done, going into Phaser or Spine as a flat texture?
  → Export PNG

Character body parts ready for Spine rigging?
  → Export PSD → import directly into Spine (preferred)
  → Share > Layers (per-layer PNG zip) if you need to QA or edit parts first
```

## Common Mistakes

- Exporting JPEG for anything that needs transparency — JPEG has no alpha channel
- Skipping the `.procreate` backup — a corrupted PSD with no backup is unrecoverable
- Layer names left as "Layer 1", "Layer 2" — these become meaningless filenames in the Layers export
- Exporting at the wrong canvas resolution and only noticing after Spine import — resize in Affinity (Pixel persona) before Spine, not after
- Forgetting that some Procreate blend modes flatten incorrectly in PSD — always check the Affinity result

## Tips

- Keep layer naming consistent from the start: `wing-left`, `wing-right`, `body`, `head`, `antenna-left`, `antenna-right`. These names carry all the way through to Spine bone naming.
- Use Procreate **Groups** to organise parts (e.g. a "wings" group containing "wing-left" and "wing-right"). Groups become folders in the PSD.
- For symbols (honey jar, hive, flowers), a single flat PNG export is usually all you need — no need for layer exports unless the symbol has animated states.
- If a PSD blend mode looks wrong when opened in Affinity, flatten that layer in Procreate before exporting.

## Next

- [04 — Transferring Files from iPad to Mac and Windows](04-file-transfer.md) — get your exports into Google Drive and onto the Windows machine
