# PSXD Serial Number Format

## Format

```
PSXD-XXXX
```

| Part | Meaning | Example |
|------|---------|---------|
| `PSXD` | PSX.DEV Homebrew | Fixed prefix |
| `-` | Separator | Always a hyphen |
| `XXXX` | Zero-padded 4-digit number | `0001` through `9999` |

## Assignment

- Serials are assigned **sequentially** in the order games are accepted into the database
- The first game accepted is `PSXD-0001`, the second is `PSXD-0002`, etc.
- Serials are **permanent** — they are never reused, reassigned, or changed
- Cancelled or removed games retain their serial (the slot is just marked `status: "Cancelled"`)

## Inspiration

The format mirrors original PlayStation disc serials:

```
SCUS-94163  →  Sony Computer Entertainment US (game #94163)
SLUS-00594  →  Sony Licensed US (game #594)
SCES-00001  →  Sony Computer Entertainment Europe
PSXD-0001   →  PSX.DEV Homebrew Database (game #1)
```

## Why four digits?

Original PS1 serials use 5 digits. We use 4 because the homebrew scene is smaller and `PSXD-0001` is more readable than `PSXD-00001`. If we ever exceed 9,999 games (a great problem to have!), we'll expand to 5 digits starting from `PSXD-10000`.

## Finding a serial

Every game page displays its serial prominently. You can also search serials directly in the database search bar on the main site.
