# Transferring Files from iPad to Mac and Windows

- **Tool:** Procreate + AirDrop + Google Drive
- **Level:** Beginner
- **Beellionaire context:** Every asset starts on the iPad — getting it off quickly and into the right place is part of every session

## Goal

Export a finished Procreate piece in the right format and get it onto your Mac (for Affinity work) and into Google Drive (for backup, Windows access, and collaborator sharing) with minimal friction.

## Prerequisites

- Google Drive for Desktop installed on Mac and Windows laptop
- A local Google Drive folder set up on the Mac (e.g. `~/Google Drive/beellionaire-assets/`)
- AirDrop enabled on iPad and Mac (Bluetooth + WiFi on for both)

## The Workflow

```
Procreate (iPad)
      |
      | AirDrop
      ↓
Mac Downloads folder  →  move to Google Drive folder
                                    |
                          syncs automatically in background
                                    |
                     ┌──────────────┴──────────────┐
               Windows laptop                 Collaborators
          (Google Drive for Desktop)        (shared folder link)
```

## Steps

### 1. Choose your export format

In Procreate, tap the **wrench icon** (top left) → **Share**, then pick the right format for what you need next:

| Format | When to use |
|---|---|
| **PSD** | Handing off to Affinity Designer/Photo — all layers preserved |
| **Procreate** | Archiving — full layer/group/mask data, Procreate-only |
| **PNG** | Final flat asset ready for Phaser or Spine |
| **PNG (layers)** | Tap Share > Layers — exports a zip of individual PNGs per layer |

For most Affinity handoffs, **PSD is the right choice.**

### 2. AirDrop to Mac

1. After tapping your export format, the share sheet appears
2. Tap **AirDrop** and select your Mac from the list
3. On the Mac, accept the incoming file — it lands in `~/Downloads`

> Make sure both devices have WiFi and Bluetooth on. AirDrop range is about 9 metres.

### 3. Move to Google Drive

Move the file from `~/Downloads` into your Google Drive asset folder in Finder. Google Drive for Desktop syncs it automatically — no manual upload needed.

A suggested folder structure:

```
Google Drive/
└── beellionaire-assets/
    ├── source/          ← .procreate and .psd working files
    ├── exports/         ← final PNGs ready for engine
    └── reference/       ← mood boards, style references
```

### 4. Access on Windows

Open File Explorer on the Windows laptop. The Google Drive folder appears as a local drive and contains the same files automatically.

### 5. Share with collaborators

Right-click any file or folder in Google Drive (web or desktop app) → **Share** → enter their email. They can view without a Google account, or edit with one.

## Worked Example — Strawberry

1. Finish the strawberry illustration in Procreate
2. Wrench → Share → **PSD**
3. AirDrop to Mac → lands in Downloads
4. Move `strawberry.psd` to `Google Drive/beellionaire-assets/source/`
5. Open in Affinity Designer on Mac — all layers intact, ready to trace as vector

## Tips

- Rename files **before** AirDropping — Procreate exports with generic names like `image.psd`. Rename to `strawberry-sketch.psd` first via the canvas title.
- If AirDrop fails, check both devices are on the same WiFi network and discoverable (Settings → General → AirDrop → Everyone for 10 Minutes).
- The `source/` folder preserves your working files. Never put raw `.psd`/`.procreate` files directly into `exports/` — keep those clean for final PNGs only.
- Google Drive's free 15GB fills up — `.procreate` files can be 100–300MB each. Archive old projects locally and keep Drive lean.

## Next

[01 — Why Vector? Clean Lines, Scaling, and PSD Export](../affinity-designer/01-why-vector.md) — open the strawberry PSD in Affinity Designer and start working with it as a vector base.
