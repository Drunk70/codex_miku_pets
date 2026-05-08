# Codex Pets

<p align="center">
  <strong>English</strong> | <a href="README_zh.md">中文</a>
</p>

A collection of desktop pet assets for the [Codex desktop pet system](https://github.com/codexorg/codex-pets). Each pet ships with everything needed to drop into Codex: a `pet.json` descriptor, a `manifest.json` with animation state mappings, and a WebP spritesheet.

---

## Features

- **Two ready-to-use pets**: Q Miku Leek Pet and 兔子 (Tuzi the calico cat)
- **Pixel-art spritesheets**: 1536 x 1872 px, 8 columns x 9 rows, 192 x 208 px per cell
- **Full state coverage**: idle, walk, run, sleep, thinking, working, success, error, waiting
- **Zero code**: pure asset pack; drop the folder into Codex's pet directory

---

## Project Structure

```
pets/
├── README.md
├── q_miku_leek_pet/
│   ├── manifest.json      # State mapping & metadata
│   ├── pet.json           # Pet descriptor
│   └── spritesheet.webp   # Animation spritesheet
└── tuzi/
    ├── manifest.json
    ├── pet.json
    └── spritesheet.webp
```

---

## Installation

1. Clone or download this repository.
2. Copy one or both pet folders (`q_miku_leek_pet` and/or `tuzi`) into the Codex Pets assets directory. The typical path is:

   ```
   ~/.codex/pets/
   ```

   or, for a local Codex install:

   ```
   /path/to/codex/data/pets/
   ```

3. Restart Codex. The new pets should appear in the pet selector.

If pets do not appear, check that the `manifest.json` and `pet.json` files are directly inside each pet folder, not nested one level deeper.

---

## Pets

### Q Miku Leek Pet

| Property      | Value                                         |
|---------------|-----------------------------------------------|
| ID            | `q-miku-leek-pet`                             |
| Display Name  | Q Miku Leek Pet                               |
| Description   | A cute Q-style teal twin-tail pixel pet with futuristic headset and a green leek. |

**Supported states:** idle, running-right, running-left, waving, jumping, failed, waiting, running, review

---

### 兔子 (Tuzi)

| Property      | Value                                         |
|---------------|-----------------------------------------------|
| ID            | `tuzi`                                        |
| Display Name  | 兔子                                          |
| Description   | A chibi calico-tabby cat with green eyes, white chest and paws, and a soft blue scarf. |

**Supported states:** idle, running-right, running-left, waving, jumping, failed, waiting, running, review

---

## Configuration Format

### `pet.json`

The minimal pet descriptor loaded by Codex at runtime.

```json
{
  "id": "q-miku-leek-pet",
  "displayName": "Q Miku Leek Pet",
  "description": "A cute Q-style teal twin-tail pixel pet...",
  "spritesheetPath": "spritesheet.webp"
}
```

| Field            | Purpose                                      |
|------------------|----------------------------------------------|
| `id`             | Unique identifier for the pet                |
| `displayName`   | Human-readable name shown in Codex UI        |
| `description`    | Short description of the pet's appearance    |
| `spritesheetPath`| Filename of the spritesheet (relative path)  |

---

### `manifest.json`

Documents metadata and maps Codex action names onto the actual animation rows in the spritesheet. Codex itself does not read this file; it is for asset publishers.

```json
{
  "id": "q-miku-leek-pet",
  "folder": "q_miku_leek_pet",
  "displayName": "Q Miku Leek Pet",
  "description": "...",
  "codexPetFile": "pet.json",
  "spritesheet": {
    "path": "spritesheet.webp",
    "format": "WEBP",
    "mode": "RGBA",
    "width": 1536,
    "height": 1872,
    "cellWidth": 192,
    "cellHeight": 208,
    "columns": 8,
    "rows": 9
  },
  "requestedStateMapping": {
    "idle": "idle",
    "walk": "running-right / running-left",
    "run": "running-right / running-left",
    "sleep": "waiting",
    "thinking": "review",
    "working": "running",
    "success": "jumping / waving",
    "error": "failed",
    "waiting": "waiting"
  },
  "codexStates": [
    "idle", "running-right", "running-left", "waving",
    "jumping", "failed", "waiting", "running", "review"
  ],
  "notes": "..."
}
```

| Field                    | Purpose                                             |
|--------------------------|-----------------------------------------------------|
| `id`                     | Same as `pet.json` `id`                             |
| `folder`                 | Containing folder name                              |
| `codexPetFile`           | Filename Codex will load (`pet.json`)               |
| `spritesheet.path`       | Spritesheet filename                                |
| `spritesheet.format`     | Image format (`WEBP`)                               |
| `spritesheet.mode`       | Color mode (`RGBA`)                                 |
| `spritesheet.width/height` | Full spritesheet dimensions in pixels             |
| `spritesheet.cellWidth/cellHeight` | Size of each animation frame in pixels  |
| `spritesheet.columns/rows` | Grid layout of the spritesheet                   |
| `requestedStateMapping`  | Maps Codex action names to animation names in the sheet |
| `codexStates`            | List of all animation states this pet supports      |

---

## Spritesheet Spec

All pets share the same grid layout for easy tooling:

| Property      | Value |
|---------------|-------|
| Dimensions    | 1536 x 1872 px |
| Cell size     | 192 x 208 px |
| Layout        | 8 columns x 9 rows |
| Format        | WEBP (RGBA) |

Each row corresponds to one animation sequence. Rows are consumed top-to-bottom by Codex's pet engine.

---

## Contributing

Contributions are welcome. You can add a new pet by:

1. Creating a new subdirectory under the repo root.
2. Adding `pet.json`, `manifest.json`, and `spritesheet.webp`.
3. Following the spritesheet spec above (1536 x 1872 px, 8 x 9 grid, 192 x 208 px cells).
4. Updating this README to document the new pet in the Pets section.

Please keep `manifest.json` in sync with `pet.json` (same `id`, `displayName`, `description`).

---

## License

MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files, to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED AS IS, WITHOUT WARRANTY OF ANY KIND.
