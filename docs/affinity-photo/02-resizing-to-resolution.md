# Resizing an Image to a Specific Resolution

- **Tool:** Affinity (Pixel/Photo workflow)
- **Level:** Beginner
- **Beellionaire context:** Use this when a painted symbol, background, or exported texture needs to match an exact game resolution like `1024x1024` or `2048x1024` without accidentally just trimming the edges.

## Goal

Resize an existing image to a specific pixel resolution in Affinity's raster workflow, understand when to use **Resize Document** versus **Resize Canvas**, and avoid confusing resizing with cropping.

## Prerequisites

- Affinity installed
- An image already opened in Affinity
- A target size you want to hit, for example `1024x1024`, `2048x1024`, or `512x512`

## First Check: Are You In The Right App And Persona?

If your install shows personas like **Vector**, **Pixel**, **Layout**, and **Canva AI**, you have the newer unified Affinity app. That is fine.

For this tutorial, use the **Pixel** or photo-editing workflow inside that app.

On desktop Affinity, the commands in this tutorial are in:

- **Resize → Resize Document**
- **Resize → Resize Canvas**

If you do **not** see those menu items, the usual cause is that you are not currently in the **Pixel** or photo-editing persona/workflow.

If you are in the **Vector** workflow instead, the menu layout and the intended use are different. Vector is better for clean geometric artwork, but this tutorial is specifically for **raster image resizing**.

Quick rule:

- **Pixel / photo-editing workflow** -> use this tutorial as written
- **Vector workflow** -> use document setup, page sizing, or export sizing instead

If needed, switch to the **Pixel** persona/workflow first, then look in the **Document** menu again.

## The Key Difference

Before touching anything, separate these three actions clearly:

| Action | What it changes | What happens to the artwork |
|---|---|---|
| **Crop** | Visible area | Cuts parts away |
| **Resize Canvas** | Document bounds | Adds or removes empty space around the image, or clips edges if the canvas becomes smaller |
| **Resize Document** | Pixel dimensions of the image itself | Scales the artwork up or down |

If your goal is "make this image exactly `1024x1024`", the main command you want is usually **Document → Resize Document**.

If your goal is "keep the artwork the same size but put it on a larger or smaller sheet", use **Document → Resize Canvas**.

## When To Use Each

### Use Resize Document when

- the whole image needs to become a new pixel size
- you are preparing a final PNG for Phaser or Spine
- you need to scale the artwork proportionally

### Use Resize Canvas when

- you need a fixed export area around the artwork
- you want to add transparent padding
- you need to fit an existing image into a power-of-two canvas like `1024x1024`

## Steps

### 1. Check the current size

Open the image, then go to **Resize → Resize Document**.

Look at:

- **Width**
- **Height**
- **DPI**

For game assets, **pixel width and height matter far more than DPI**. A game engine reads the actual pixel dimensions of the exported PNG.

### 2. Decide whether you are scaling or padding

Ask one simple question:

> Do I want the artwork itself to become bigger or smaller, or do I just need the document to end up at a specific size?

Use this rule:

- **Artwork changes size** → **Resize Document**
- **Artwork stays the same, document area changes** → **Resize Canvas**

### 3. Resize the image itself

If you need to scale the image to a new resolution:

1. Go to **Resize → Resize Document**
2. Enter the target **Width** and **Height** in pixels
3. Keep the **lock icon** enabled if you want to preserve aspect ratio
4. Choose a resampling method
5. Click **Resize**

If the lock icon is enabled and you type `1024` for width, the height updates automatically to keep the image from stretching.

If you disable the lock and force both width and height manually, the image can distort. That is only useful when you deliberately want a stretch, which is rare for art assets.

### 4. Pick the right resampling method

When shrinking or enlarging raster art, Affinity has to recalculate pixels. That is called **resampling**.

Good practical defaults:

| Situation | Suggested resampling |
|---|---|
| Reducing painted art | **Lanczos 3 (non-separable)** |
| Enlarging painted art a little | **Bicubic** or **Lanczos 3** |
| Pixel art | **Nearest Neighbour** |

For most Procreate paintings, icons with soft shading, or textured backgrounds, **Lanczos 3** is the safest default.

### 5. Use canvas resize if you need an exact frame size

If the image must sit inside a fixed-size canvas, for example turning an `880x880` symbol into a `1024x1024` export with transparent margins:

1. Go to **Resize → Resize Canvas**
2. Enter the target **Width** and **Height**
3. Use the anchor grid to keep the artwork centered
4. Click **Resize**

This does **not** scale the artwork. It changes the document area around it.

If the new canvas is larger, you get extra transparent space.

If the new canvas is smaller, the edges get cut off.

### 6. Combine both when needed

Sometimes the correct workflow is:

1. Go to **Resize → Resize Document** to scale the art down to a sensible size
2. Then go to **Resize → Resize Canvas** to place it inside the exact final export dimensions

This is common for game assets because the art and the export frame are often not the same thing.

## Worked Example — Honey Jar Symbol to `1024x1024`

Imagine you painted a honey jar symbol in Procreate and opened it in Affinity Photo. The current image size is `1600x1400`, but your slot symbol export must be exactly `1024x1024`.

### Option A: Scale the whole image to fit inside `1024x1024` without distortion

1. Go to **Resize → Resize Document**
2. Set the width to `1024` with aspect ratio locked
3. Let the height adjust automatically
4. Click **Resize**
5. Then go to **Resize → Resize Canvas**
6. Set canvas size to `1024x1024`
7. Center the artwork

Result: the honey jar stays proportional, and the final document is exactly `1024x1024` with transparent padding if needed.

### Option B: Force the artwork itself to exactly `1024x1024`

1. Go to **Resize → Resize Document**
2. Turn off aspect ratio lock
3. Enter `1024` by `1024`
4. Click **Resize**

Result: the image becomes exactly square, but it may look stretched. Usually this is the wrong choice for painted art.

## Tips

- **Do not rely on DPI for game exports.** `1024x1024` is `1024x1024` whether the DPI says 72 or 300.
- **Downscaling is safer than upscaling.** Making a large image smaller usually looks good. Making a small image much larger usually softens detail.
- **Vectors belong in Affinity Designer.** If the asset is really a clean geometric UI element, resizing the vector source in Designer is better than enlarging a raster export in Photo.
- **Use transparent padding instead of stretching** when you need a fixed-size frame for the engine.
- **Keep the original file.** Save an editable Affinity file before resizing for export so you do not overwrite your highest-quality source.

## Next

[01 — Texture Editing and Compositing](01-texture-editing.md) — continue in Affinity Photo when the asset needs paint cleanup, texture balancing, or final polish before export.