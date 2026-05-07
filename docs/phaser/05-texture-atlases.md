# Creating a Texture Atlas for Phaser from Trimmed PNGs

- **Tool:** Affinity (asset prep) + atlas packer + Phaser 3
- **Level:** Beginner
- **Beellionaire context:** Pack trimmed reel symbols, UI parts, and effects into one atlas so Phaser draws fewer textures and keeps memory usage cleaner.
- **Tech context:** Phaser 3 `this.load.atlas(...)` with PNG + JSON atlas data.
- **Affinity version:** Baseline in this repo is **Affinity April '26 (build 4351)**.

## Goal

Create a Phaser-ready texture atlas from multiple PNG files (with whitespace trimmed), load it in Phaser, and render frames by name.

## Prerequisites

- A folder of exported PNG assets with transparent backgrounds
- Phaser 3 project running
- Any atlas packer that exports PNG + JSON for Phaser

Recommended beginner option:
- **Free Texture Packer** by CodeAndWeb (desktop GUI)

## Why Atlas Instead of Sprite Sheet Here

When you trim transparent whitespace, each image usually ends up a different width and height.

- **Sprite sheet:** Best when all frames are the same size in a fixed grid
- **Texture atlas:** Best when frame sizes vary (trimmed assets)

For Beellionaire symbol art and UI cutouts, atlas is usually the right default.

## Steps

### 1. Prepare source PNGs in Affinity

1. In Affinity, clean edges and remove accidental background pixels.
2. Export each element as a separate PNG with transparency.
3. Use clear names in kebab-case, for example:
   - `queen-bee.png`
   - `honey-jar.png`
   - `wild-hive.png`
4. Put all source PNGs in one folder, for example:
   - `assets/source/reel-symbols/`

Note: Trimming whitespace at source is fine. Atlas metadata preserves the frame rectangle and size info Phaser needs.

### 2. Create the atlas project in your packer

1. Open your atlas packer.
2. Add all PNGs from `assets/source/reel-symbols/`.
3. Set output files to:
   - `assets/atlases/reel-symbols.png`
   - `assets/atlases/reel-symbols.json`

### 3. Use game-safe packing settings

Set these options (names vary slightly by tool):

- **Trim mode:** On
- **Inner padding:** 2
- **Extrude / border duplicate:** 2
- **Max atlas size:** 2048x2048 (good default for web and mobile)
- **Power-of-two size:** On
- **Data format:** Phaser-compatible JSON (Hash format preferred)

Why these settings matter:
- Padding and extrude reduce texture bleeding at frame edges
- 2048 cap keeps textures practical for many devices

### 4. Publish the atlas

Export (or publish) the atlas. You should get:

- one PNG texture
- one JSON metadata file with frame names and rectangles

If your packer created multiple pages, keep each PNG and JSON page together and load accordingly.

### 5. Load atlas in Phaser

In your scene `preload`:

```ts
preload() {
  this.load.atlas(
    'reel-symbols',
    'assets/atlases/reel-symbols.png',
    'assets/atlases/reel-symbols.json'
  );
}
```

In `create`, render a frame by file name:

```ts
create() {
  this.add.image(300, 200, 'reel-symbols', 'honey-jar.png');
  this.add.image(500, 200, 'reel-symbols', 'queen-bee.png');
}
```

Frame names usually match the original source filenames.

### 6. Keep symbol placement consistent after trimming

Because trimmed frames have different dimensions, visual alignment can shift if you place everything by raw top-left logic.

Use one of these approaches:

- Place symbols by center (`setOrigin(0.5, 0.5)`) and consistent reel cell centers
- Store per-symbol placement offsets in data
- Keep symbol art centered before export for predictable bounds

### 7. Validate quickly in a debug scene

Create a small test scene that renders all frames in a grid and labels each by frame name.

Check for:
- edge bleeding
- unexpected offset jumps
- wrong frame names
- blurry output caused by scaling

## Common Mistakes

- Exporting sprite sheet JSON instead of atlas JSON
- Forgetting padding/extrude, causing thin seams
- Mixing naming styles (`HoneyJar.png` vs `honey-jar.png`)
- Packing too many assets into a 4096 atlas too early

## Tips

- Group atlases by usage, not by art tool:
  - `reel-symbols`
  - `ui-controls`
  - `fx-particles`
- Keep source art and packed output in separate folders.
- Rebuild atlas whenever source PNGs change.
- For Spine character exports, keep using Spine's own atlas pipeline.

## Next

- Create a simple reel prototype scene that reads symbol frame names from data and spawns images from the atlas.
- Add an asset naming convention doc so frame names stay stable across the team.
