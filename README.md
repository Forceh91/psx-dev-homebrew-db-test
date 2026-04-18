# 🎮 PSX.DEV Homebrew Database (PSXD)

> The unofficial community registry for PlayStation 1 homebrew games.

**Live site:** `https://Forceh91.github.io/psx-dev-homebrew-db`  
**Submit a game:** [Open a GitHub Issue](https://github.com/Forceh91/psx-dev-homebrew-db/issues/new/choose)

---

## What is this?

The **PSX.DEV Homebrew Database (PSXD)** is a community-maintained registry of PS1 homebrew games. Every listed game receives a permanent **PSXD serial number** — a unique identifier in the style of the original PlayStation's game serials (like `SCUS-94163` or `SLUS-00594`).

This database is:

- Served entirely from this GitHub repository (no backend required)
- Open to all PS1 homebrew games — free or not, complete or demos
- Community-maintained via GitHub Issues
- Built to be forkable: the whole site is a single `index.html`

---

## Serial Number Format

Every game in the database is assigned a serial in the format:

```
PSXD-XXXX
```

Where:

- **`PSXD`** — PSX.DEV Homebrew (our database prefix)
- **`XXXX`** — A four-digit zero-padded number (e.g. `0001`, `0042`, `1337`)

Serials are assigned **sequentially by submission date** and are permanent — they never change or get reassigned.

### Examples

```
PSXD-0001  →  Lunar Drift
PSXD-0002  →  Crypts of Karanor
PSXD-0003  →  Starfield Zero
```

This mirrors the original Sony PS1 serial format:

```
SCUS-XXXXX  →  Sony Computer Entertainment US
SLUS-XXXXX  →  Licensed by Sony (US)
PSXD-XXXX   →  PSX.DEV Homebrew Database
```

---

## Repository Structure

```
/
├── index.html              # The entire website (single file)
├── games.json              # Master index of all games
├── games/
│   ├── PSXD-0001.json      # Full detail for each game
│   ├── PSXD-0002.json
│   └── ...
├── assets/
│   ├── boxart/
│   │   ├── PSXD-0001-front.png
│   │   ├── PSXD-0001-back.png
│   │   ├── PSXD-0001-disc.png
│   │   └── PSXD-0001-thumb.png
│   └── screenshots/
│       ├── PSXD-0001-01.png
│       └── ...
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   └── game-submission.yml   # Submission form
│   └── workflows/
│       └── validate.yml          # (Optional) JSON validation CI
└── SERIAL_FORMAT.md              # Serial number documentation
```

---

## Data Format

### `games.json` (Master Index)

The master index is the source of truth for the game list. It's loaded on page load.

```json
{
  "version": "1.0",
  "last_updated": "2025-01-01",
  "total_games": 1,
  "games": [
    {
      "serial": "PSXD-0001",
      "title": "Lunar Drift",
      "slug": "lunar-drift",
      "developer": "PixelBrew Studios",
      "year": 2023,
      "genre": ["Racing", "Arcade"],
      "region": "Worldwide",
      "status": "Complete",
      "thumbnail": "assets/boxart/PSXD-0001-thumb.png"
    }
  ]
}
```

### `games/PSXD-XXXX.json` (Per-Game Detail)

Loaded on demand when a user clicks a game card.

```json
{
  "serial": "PSXD-0001",
  "title": "Lunar Drift",
  "slug": "lunar-drift",
  "developer": "PixelBrew Studios",
  "publisher": "PixelBrew Studios",
  "year": 2023,
  "genre": ["Racing", "Arcade"],
  "players": "1-2",
  "region": "Worldwide",
  "status": "Complete",
  "language": ["English"],
  "description": "A fast-paced arcade racer set on the lunar surface.",
  "release_date": "2023-06-15",
  "version": "1.2.0",
  "download_url": "https://github.com/...",
  "source_url": "https://github.com/...",
  "disc_image_format": ["BIN/CUE", "ISO"],
  "emulator_compatibility": {
    "duckstation": "Perfect",
    "pcsx_redux": "Perfect"
  },
  "hardware_tested": true,
  "hardware_notes": "Tested on SCPH-7502 (PAL).",
  "screenshots": ["assets/screenshots/PSXD-0001-01.png"],
  "boxart": {
    "front": "assets/boxart/PSXD-0001-front.png",
    "back": "assets/boxart/PSXD-0001-back.png",
    "disc": "assets/boxart/PSXD-0001-disc.png"
  },
  "credits": {
    "programming": ["Alice Mercer"],
    "art": ["Bob Tanaka"],
    "music": ["Clara Voss"]
  },
  "links": {
    "website": "",
    "discord": "",
    "itch_io": "https://itch.io/..."
  },
  "submitted_by": "PixelBrew",
  "submission_date": "2023-07-01",
  "last_updated": "2024-02-10"
}
```

### Status Values

| Status             | Meaning                        |
| ------------------ | ------------------------------ |
| `Complete`         | Full, finished release         |
| `Demo`             | Public demo, limited content   |
| `Beta`             | Feature-complete, in testing   |
| `Work In Progress` | Incomplete, actively developed |
| `Cancelled`        | Development stopped            |

---

## Submitting a Game

### Step 1: Open a GitHub Issue

Click **[Submit a Homebrew Game](https://github.com/Forceh91/psx-dev-homebrew-db/issues/new?template=game-submission.yml)** and fill out the form. You'll need:

- Game title and developer name
- Release year and status
- A download link
- A short description
- Any artwork (attach as images to the issue)

### Step 2: Attach Artwork

Drag and drop images directly onto the GitHub issue. We accept:

| Type        | Recommended Size | Filename Convention   |
| ----------- | ---------------- | --------------------- |
| Front cover | 750×1050px       | `title-front.png`     |
| Back cover  | 750×1050px       | `title-back.png`      |
| Disc art    | 512×512px        | `title-disc.png`      |
| Thumbnail   | 200×280px        | `title-thumb.png`     |
| Screenshots | 1024×768px       | `title-screen-01.png` |

Artwork should be original — not using Sony's trade dress or copyrighted assets.

### Step 3: Wait for Review

A maintainer will:

1. Verify the submission is homebrew (not a pirated commercial game)
2. Assign a `PSXD-XXXX` serial
3. Create the JSON files and commit them to the repo
4. Close the issue with the assigned serial

---

## Maintaining the Database

### Adding a Game (Maintainers)

1. Assign the next available serial (check `games.json` for the last number)
2. Create `games/PSXD-XXXX.json` using the template in `games/PSXD-0001.json`
3. Add boxart to `assets/boxart/PSXD-XXXX-*.png`
4. Add screenshots to `assets/screenshots/PSXD-XXXX-*.png`
5. Add the summary entry to `games.json`
6. Update `total_games` and `last_updated` in `games.json`
7. Close the submission issue with a comment including the assigned serial

### Updating a Game

Open a PR or issue referencing the serial number. Include what changed (new version, fixed links, new artwork, etc.).

---

## Deployment

This site is a single static HTML file with no build step required.

### GitHub Pages

1. Go to **Settings → Pages**
2. Set source to `main` branch, `/ (root)`
3. The site will be live at `https://Forceh91.github.io/psx-dev-homebrew-db`

### Update `index.html`

After deployment, update the `REPO_RAW` constant at the top of the `<script>` in `index.html`:

```js
const REPO_RAW = "https://raw.githubusercontent.com/Forceh91/psx-dev-homebrew-db/main";
```

---

## Contributing

- **Submit a game:** Open a [game submission issue](https://github.com/Forceh91/psx-dev-homebrew-db/issues/new/choose)
- **Fix bad data:** Open a PR with corrections
- **Improve the site:** PRs welcome — keep it a single HTML file
- **Maintainers:** Label issues `submission`, `pending-review`, `approved`, `rejected`

---

## License

Database content (JSON files, artwork) is contributed by individual developers and remains their property.  
The site code (`index.html`) is MIT licensed.  
This project is not affiliated with Sony Computer Entertainment.
