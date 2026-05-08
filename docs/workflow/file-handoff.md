# Cross-Tool File Handoff Cheatsheet

- **Tool:** Procreate · Affinity (unified app, build 4351) · Spine 2D · Phaser 3
- **Level:** Beginner
- **Beellionaire context:** Every asset in the game passes through at least two tools. This cheatsheet maps what format to hand off at each stage and when Affinity is actually needed.

## Goal

Know which file format to export at each handoff point, and understand when Affinity (and which persona) is worth the extra step vs. going straight to the next tool.

---

## Full Pipeline at a Glance

```
Procreate (iPad)
      |
      | AirDrop → Mac
      |
      ├─── PSD ──────────────────► Affinity (Vector persona)  (UI, icons, vector cleanup)
      │                                   |
      │                                   | SVG / PNG / PSD
      │                                   ↓
      ├─── PSD ──────────────────► Affinity (Pixel persona)   (raster compositing, resize)
      │                                   |
      │                                   | PNG (flat or per-part)
      │                                   ↓
      └─── PNG (per layer zip) ──► Spine 2D           (rig, animate, pack atlas)
                                          |
                                          | .skel + .atlas + .png
                                          ↓
                                   Phaser 3 + SvelteKit  (runtime, game logic, UI)
```

---

## Handoff Map by Asset Type

### Bee characters (worker bee, queen bee)

| Step | From | To | Format | Notes |
|---|---|---|---|---|
| 1 | Procreate | Affinity — Pixel persona *(optional)* | PSD | Clean up edges, fix blend modes, adjust levels if needed |
| 2 | Affinity *(or Procreate directly)* | Spine 2D | PSD direct import or per-layer PNGs | See Procreate exporting doc for both paths |
| 3 | Spine 2D | Phaser | `.skel` + `.atlas` + `.png` | Use `spine-phaser` plugin to load |

**Skip Affinity if:** the Procreate PSD is clean, correctly sized, and blend modes look right. Import PSD directly into Spine.

**Use Affinity (Pixel persona) if:** parts have fringing, need colour grading, or the canvas was too small and needs resizing before Spine import.

---

### Reel frame and slot chrome

| Step | From | To | Format | Notes |
|---|---|---|---|---|
| 1 | Procreate | Affinity — Vector persona | PSD or PNG | Procreate sketch is reference only — redraw as vector |
| 2 | Affinity — Vector persona | Phaser | PNG | Export at target resolution (e.g. 1920×1080 for the full frame) |

**Affinity (Vector persona) is required here.** The reel frame needs hard, clean edges and must scale cleanly to different screen sizes. Vector is the only practical approach.

---

### Symbol icons (honey jar, hive, queen bee icon, flowers, playing card suits)

| Step | From | To | Format | Notes |
|---|---|---|---|---|
| 1 | Procreate *(sketch)* | Affinity — Vector persona | PSD or PNG *(reference)* | Redraw as vector for clean scalable output |
| 2 | Affinity — Vector persona | Phaser (via atlas packer) | PNG | Export each symbol at 512×512 px |

**Affinity (Vector persona) is strongly recommended.** Symbols appear at multiple sizes (reel, paytable, win overlay) — vector means one source file, any output size.

**Skip Affinity if:** symbols are hand-painted and intentionally textured. In that case export flat PNG from Procreate at the largest size you need.

---

### Painted backgrounds and textures (honeycomb, hive environment)

| Step | From | To | Format | Notes |
|---|---|---|---|---|
| 1 | Procreate | Affinity — Pixel persona *(optional)* | PSD | Composite layers, adjust colour, resize to power-of-two |
| 2 | Affinity *(or Procreate directly)* | Phaser | PNG | Flat, power-of-two dimensions (e.g. 2048×1024) |

**Skip Affinity if:** the Procreate canvas is already the right size and the flat PNG export looks correct.

**Use Affinity (Pixel persona) if:** you need to composite multiple Procreate pieces, adjust levels/colour, or resize to exact power-of-two without quality loss.

---

### Paytable and help screens

| Step | From | To | Format | Notes |
|---|---|---|---|---|
| 1 | Procreate *(sketch layout)* | Affinity Publisher | PSD *(reference)* | Build final layout in Publisher with consistent type and symbol placement |
| 2 | Affinity Publisher | SvelteKit | PNG or PDF | Export as PNG for use as an image overlay, or build as HTML/CSS in SvelteKit directly |

---

## When Affinity Is Optional vs. Required

| Affinity persona | Required for | Optional / skip for |
|---|---|---|
| **Vector** | Reel frame, slot chrome, symbol icons (clean vector) | Painted symbols, backgrounds |
| **Pixel** | Compositing multiple layers, resizing to exact px, fixing blend modes | Clean single-layer Procreate exports that are already the right size |
| **Layout** | Paytable layout, help screen multi-page layout | Simple UI overlays built directly in SvelteKit |

---

## File Naming at Each Handoff

Follow kebab-case throughout. The name set in Procreate (gallery title) carries through:

```
Procreate canvas:   "bee-queen"
Layer export:       bee-queen-body.png, bee-queen-wing-left.png ...
Spine project:      bee-queen.spine
Spine export:       bee-queen.skel, bee-queen.atlas, bee-queen.png
Phaser key:         'bee-queen'
```

Keeping names consistent across tools avoids mismatches when Spine looks for image files by name.

---

## Format Reference Summary

| Format | From | To | Carries |
|---|---|---|---|
| `.procreate` | Procreate | Archive only | Everything — master backup |
| `.psd` | Procreate | Affinity Designer / Photo | Layers, groups, common blend modes |
| `.afdesign` | Affinity | Archive | Vector objects, symbols, artboards — opens in any persona |
| `.png` (flat) | Any | Phaser / Spine / atlas packer | Pixels + transparency |
| `.png` (per layer zip) | Procreate | Spine 2D | Individual body part PNGs |
| `.skel` | Spine 2D | Phaser | Binary skeleton + animation data |
| `.atlas` | Spine 2D | Phaser | Texture atlas metadata |

---

## Tips

- **Name layers in Procreate before exporting.** Layer names become filenames in the per-layer ZIP and image names in Spine. Renaming after the fact means updating references in Spine too.
- **Always keep the `.procreate` and `.afdesign` source files.** PNGs and PSDs can be re-exported; the original project files are your edit safety net.
- **Spine expects images in a specific folder at import.** Set up your Spine project's image path to point at `exports/bee-queen/` before importing — saves relinking every image.
- **Power-of-two canvas sizes all the way through.** Start in Procreate at 2048×2048, export at 1024×1024 or 512×512 as needed. Never upscale.

## Next

- [Naming Conventions and Folder Structure](naming-conventions.md) — the exact folder layout and file naming rules for the whole project
- [Spine to Phaser Integration Cheatsheet](spine-to-phaser.md) — the Spine-specific handoff in detail
