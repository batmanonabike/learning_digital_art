# Shading and Highlighting in Procreate

- **Tool:** Procreate
- **Level:** Beginner
- **Beellionaire context:** Bee characters, symbol icons, and UI elements need depth to look polished. This tutorial covers how to add shading and highlights in Procreate without overcomplicating the process.

## Goal

Add convincing shading and highlights to flat base art using clipping masks, blend modes, and a small set of brushes — without needing to paint freehand shadows from scratch.

## Prerequisites

- A canvas with flat base colours on separate named layers
- Basic familiarity with the Layers panel

## Using Apple Pencil (USB-C)

If you are using **Apple Pencil (USB-C)**, pressure sensitivity is not available. You can still shade effectively by controlling opacity with layer settings and repeated passes.

Use this setup:

- Shadow layer: **Multiply**, layer opacity **55-70%**
- Highlight layer: **Screen** or **Add**, layer opacity **25-45%**
- Soft Airbrush opacity: **15-30%**
- Build tone in 3-6 light passes instead of pressing harder

Important: keep brush opacity fixed while doing those passes. Do not change opacity every pass. If the result is too strong or too weak, adjust **layer opacity** after the passes.

This workflow is slower than pressure shading, but it is consistent and easy to adjust non-destructively.

## How Light Works on Simple Shapes

Before touching brushes, decide where your light is coming from and stick to it. For Beellionaire, a consistent light source in the upper-left works well across all assets.

The pattern is always the same:
- **Shadow:** opposite side from the light, edges of rounded forms
- **Highlight:** facing the light, often a small sharp spot near the top
- **Midtone:** the base colour itself — don't paint over this, let it show through

For a bee body (a rounded oval), that means:
- Dark at the bottom and right edges
- Highlight dot near the top-left
- Base yellow in between

## Layer Setup

Never paint shading directly on your base colour layer. Use separate layers above it with blend modes — this keeps base colours clean and lets you redo shading without redrawing the art.

```
[Highlight layer]     — blend mode: Add or Screen
[Shadow layer]        — blend mode: Multiply
[Base colour layer]   ← never paint on this
```

Both the shadow and highlight layers should be set as **Clipping Masks** to the base layer below — this keeps all paint inside the shape automatically.

### Setting up a clipping mask

1. Create a new layer directly above the base colour layer
2. Tap the new layer in the Layers panel
3. Tap **Clipping Mask**
4. The layer gets an arrow pointing down — it now clips to the layer below

Do this for both the shadow layer and the highlight layer.

## Brushes to Use

You don't need many. These three cover most situations:

| Brush | Where to find it | Use for |
|---|---|---|
| **Soft Airbrush** | Airbrushing > Soft Brush | Large soft shadows and ambient shading |
| **Hard Airbrush** | Airbrushing > Hard Brush | Tighter shadow edges and harder forms |
| **Round Brush (Inking)** | Inking > Studio Pen | Sharp highlight dots, clean edge accents |

Start with the Soft Airbrush for almost everything. Switch to the Studio Pen only for precise highlights.

## Brush Size Guidelines

Size is relative to your canvas, but these starting points work well:

| Use | Size |
|---|---|
| Large shadow fill (body of a bee) | 20–40% |
| Mid shadow / transition | 10–20% |
| Tight shadow edge | 5–10% |
| Highlight dot | 3–8% |

Reduce opacity to around **30–50%** and build up in multiple passes rather than painting at full opacity. This gives you gradual falloff that looks more natural.

## Steps

### 1. Set up your layers

1. Confirm your base art has flat colours on separate layers — one layer per body part (body, wings, head, etc.)
2. For each part you want to shade, add two new layers directly above it: one for shadows, one for highlights
3. Set both as Clipping Masks to the base layer below
4. Rename them: `body-shadow`, `body-highlight` etc.

### 2. Paint shadows

1. Select the shadow layer
2. Set the layer blend mode to **Multiply**
3. Pick a colour — do not use black. Sample the base colour, then drag it in the HSB colour wheel toward a darker, slightly cooler or warmer hue. A dark warm brown works for yellows; a dark blue-purple works for blues.
4. Choose the Soft Airbrush at 20–30% opacity
5. Paint along the edges of the shape that face away from the light (bottom-right for upper-left lighting)
6. Build up in multiple strokes at the same brush opacity — you can always add more, harder to remove

### 3. Add a core shadow

Where two surfaces meet (e.g. where the bee's abdomen stripes sit), add a slightly harder, darker line. Switch to Hard Airbrush at 10–15% size and paint a thin stroke along that boundary.

### 4. Paint highlights

1. Select the highlight layer
2. Set the blend mode to **Add** (for a glowing effect) or **Screen** (softer)
3. Pick white or a very light, slightly warm version of the base colour
4. Use the Soft Airbrush at 5–10% opacity and small size
5. Paint a soft glow near the top-left of the shape
6. For a sharper specular dot (like light catching a shiny surface), switch to Studio Pen at 3–5% size and tap once — don't drag

### 5. Adjust overall intensity

If the shading looks too strong:
- Lower the **opacity** of the shadow or highlight layer in the Layers panel (swipe left → tap the layer → drag opacity)
- Or change the blend mode — Multiply at full opacity is strong; try dropping to 60%

If it looks too flat, increase layer opacity or add another pass.

### 6. Check at actual size

Pinch to zoom out to 100%. Shading that looks heavy at 300% zoom often looks right at actual size. Adjust if needed.

## Worked Example — Bee Body Segment

The bee's abdomen has alternating yellow and dark brown stripes. Here's the shading approach per segment:

1. **Base layer:** flat yellow fill for the yellow segments
2. **Shadow layer (Multiply):** dark warm brown, soft airbrush, painted at bottom edge of each segment and between stripe boundaries
3. **Highlight layer (Add):** light yellow-white, tiny soft airbrush spot near top of each segment
4. **Edge accent:** tiny dark stroke along the top edge of each brown stripe using Hard Airbrush — gives a sense of the stripe being slightly raised

## Tips

- **Sample your base colour first** before picking a shadow colour. Then shift it darker and cooler in the HSB wheel. Avoid using the same hue family for too long — ambient occlusion often has a cool/purple cast even on warm subjects.
- **Wings are special.** Bee wings are translucent — use a very light blue-grey for both shadow and highlight, at low opacity, to suggest the membrane without losing the transparency feeling.
- **No-pressure workflow works.** With Apple Pencil (USB-C), keep brush opacity low and build tone with multiple passes. Control intensity using layer opacity instead of pen pressure.
- **Don't shade everything.** Simple flat symbols (playing card suits, basic icons) often look better without shading. Shading is most valuable on organic, rounded forms — bee bodies, honey jars, hive cells.
- **Undo is your friend.** Procreate has generous undo (two-finger tap). Don't be afraid to paint a stroke and immediately undo it to compare.
- **Alpha lock vs clipping mask:** Alpha Lock (tap the layer > Alpha Lock) also keeps paint inside the shape, but it paints directly on the base layer — changes are destructive. Clipping masks keep base colours untouched. Prefer clipping masks.

## When to Hand Off to Sprite Illuminator Instead

If the shading feels too difficult to get right by hand, or you want the lighting to feel consistent across all symbols, consider exporting the flat base PNG and using **Sprite Illuminator** to add shading via normal map lighting instead. See the [Cross-Tool File Handoff Cheatsheet](../workflow/file-handoff.md) for where it fits.

## Next

- [06 — Painting Flat Art for Sprite Illuminator](06-flat-art-for-sprite-illuminator.md) — how to set up Procreate art so Sprite Illuminator can shade it effectively
- [03 — Exporting from Procreate](03-exporting.md) — once shading is done, export in the right format for the next tool
