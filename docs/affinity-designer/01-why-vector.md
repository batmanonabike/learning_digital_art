# Why Vector? Clean Lines, Scaling, and PSD Export

> **Tool:** Affinity Designer
> **Level:** Beginner
> **Beellionaire context:** Slot game assets — reel frames, UI buttons, symbol icons — need to look crisp at multiple screen sizes. Vector makes this free.

## Goal

Understand why vector is the right choice for game UI and icon assets, how Affinity Designer handles both vector and raster in one app, and how to export to PSD so your work flows cleanly into other tools.

## Raster vs Vector — The Short Version

| | Raster (Procreate, Photoshop) | Vector (Affinity Designer) |
|---|---|---|
| Made of | Pixels | Maths (points, curves, fills) |
| Scale up | Goes blurry | Stays perfectly sharp |
| Scale down | Fine | Fine |
| File size | Large | Small |
| Best for | Painting, textures, photos | Logos, UI, icons, line art |

**Raster** is what you draw in Procreate — it's great for painterly work and textures, but every canvas has a fixed resolution. If you paint at 1024×1024 and later need 2048×2048, you've lost quality.

**Vector** stores shapes as geometry. A circle is defined by a centre point and radius — not pixels. Resize it to any dimension and it redraws perfectly. For a slot game that might run on a phone, a tablet, and a desktop browser, that matters.

## Why This Matters for Game Assets

Slot game UI in particular — reel frames, buttons, win overlays, paytable borders — tends to be reused at different sizes and on different screen densities. Drawing these as vectors in Affinity Designer means:

- One source file works for all output sizes
- Crisp edges at any resolution with no extra work
- Easy to tweak colours, proportions, or shapes later
- Symbols (like a honey jar icon) stay sharp whether they're 64px or 256px on screen

Painted textures and character art still belong in Procreate. The rule of thumb:

> **Structural / geometric shapes → Affinity Designer (vector)**
> **Organic / painterly / textured → Procreate (raster)**

## Affinity Designer's Two Modes

Affinity Designer is unusual in that it handles both vector and raster in the same file via **Personas** — modes you switch between using the icons at the top left of the screen:

| Persona | Icon | What it does |
|---|---|---|
| **Vector Persona** | Pentagon | Draw and edit vector shapes, curves, text |
| **Pixel Persona** | Grid of squares | Paint raster strokes directly on pixel layers |
| **Export Persona** | Arrow | Define slices and export assets |

For game asset work you'll spend most time in Vector Persona, occasionally drop into Pixel Persona to paint detail on top, then use Export Persona to output final PNGs.

## PSD Export — Why It's Useful

Affinity Designer can export to PSD (Photoshop Document format), which acts as a universal handoff format across the creative toolchain:

- **Procreate → Affinity:** open a PSD from Procreate with all layers intact as a reference or raster base layer
- **Affinity → Affinity Photo:** pass a file between Designer and Photo while keeping layers
- **Affinity → any other tool:** PSD is the most widely supported layered file format

Vector layers in Affinity export to PSD as high-resolution rasterised layers — they won't stay editable as vectors in another app, but they'll be pixel-perfect at the resolution you choose.

## Worked Example — Strawberry

You have `strawberry-sketch.psd` exported from Procreate and sitting in your Google Drive source folder. Here's how to open it in Affinity Designer and use it as a vector tracing base:

1. **Open the file** — File → Open → select `strawberry-sketch.psd`. Affinity imports it with layers intact.
2. **Lock the sketch layer** — in the Layers panel, click the padlock icon on the Procreate layer. This prevents accidental edits to your reference.
3. **Create a new layer above it** — this is where your vector artwork will live.
4. **Switch to Vector Persona** (top left pentagon icon)
5. **Use the Pen tool** (P) to trace the outline of the strawberry — click to place anchor points, drag to create curves
6. **Add a fill** — with the shape selected, click a colour in the swatches panel
7. **Build up shapes** — separate vector shapes for the body, seeds, and leaf work better than one complex path

When done, File → Export → PSD to save a layered version, or use Export Persona to slice out individual PNGs.

## Tips

- **Zoom to 100% and 200%** while working — vector looks great at any zoom but it's good to check your anchor point placement at actual size.
- **Node tool (A)** selects and moves individual anchor points on a path. **Move tool (V)** moves whole objects.
- Use **Edit → Snap to Grid** to keep UI elements aligned precisely — important for slot reel frames.
- Affinity Designer files (`.afdesign`) open on both Mac and Windows from your shared Google Drive folder — no conversion needed.
- Undo history is generous but not infinite — save often with Cmd/Ctrl+S.

## Next

[02 — Document Setup and Personas](02-document-setup.md) — set up an Affinity Designer document correctly for game asset work before building anything serious.
