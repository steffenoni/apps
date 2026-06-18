# Apps — Documentation

Personal web apps hosted on GitHub Pages at `steffenoni.github.io/apps`.
Built as standalone HTML files — no framework, no build step, no dependencies.

---

## Structure

```
apps/
├── index.html          # Launcher — home screen hub
├── human-flag.html     # Human Flag training app
├── abs.html            # Abs training app
├── images/             # Exercise photos for abs.html
│   ├── ex-hollow-body-hold.jpg
│   ├── ex-hollow-90.jpg
│   ├── ex-hollow-plank.jpg
│   ├── ex-planche-lean.jpg
│   ├── ex-tuck-sit.jpg
│   ├── ex-pike-lean.jpg
│   ├── ex-pike-hold.jpg
│   ├── ex-hanging-hold.jpg
│   ├── ex-l-sit.jpg
│   └── ex-dragon-flag.jpg
└── DOCS.md             # This file
```

---

## Deployment

GitHub Pages serves the `main` branch directly. Commit and push → live in ~30s.
No build process. Edit HTML files directly.

**Live URL:** `https://steffenoni.github.io/apps/`

---

## How to install on iPhone

1. Open Safari → go to the URL
2. Tap the Share button → "Add to Home Screen"
3. Apps open full-screen with no browser chrome
4. To get updates after a commit: open the app → pull down to hard refresh

---

## Adding a new app

1. Create a new `your-app.html` file in the repo root
2. Add a card to `index.html` — copy an existing `<a class="app-card">` block and update `href`, icon emoji, name, and description
3. Each app is fully self-contained in its HTML file

---

## abs.html

**Purpose:** Guided isometric abs session — hollow body, compression, planche prep.

### Exercises (10 total)

| # | Name | Equipment |
|---|------|-----------|
| 1 | Hollow Body Hold | Floor |
| 2 | 90° Hollow | Floor |
| 3 | Hollow Plank | Floor |
| 4 | Planche Lean | Floor |
| 5 | Tuck Sit | Floor / Parallels |
| 6 | Pike Lean | Floor |
| 7 | Pike Hold | Elevated surface |
| 8 | Hanging Hold | Pull-up bar |
| 9 | L-sit | Parallels / Floor |
| 10 | Dragon Flag | Bench |

### Session structure

- 2 rounds × 10 exercises
- Hold duration set by level (see below)
- 20s rest between exercises (auto-advance)
- 60s round break between rounds

### Levels

| Level | Hold | Approx. duration |
|-------|------|-----------------|
| Beginner | 20s | ~10 min |
| Intermediate | 35s | ~14 min |
| Advanced | 50s | ~18 min |

### Key behaviour

- **Auto-advance:** timer hits zero → beep → rest screen → beep → next exercise. No taps needed mid-session.
- **Audio:** Web Audio API (no external files). Three countdown beeps at 3-2-1, ascending chime at hold completion, double beep at rest completion. iOS audio unlocked on first Start tap.
- **Images:** served from `images/` folder in repo root. If an image file is missing, the card shows no image — nothing breaks.
- **Dark mode:** fully supported via CSS `prefers-color-scheme`.
- **Offline:** works after first load (browser cache).

### To modify exercises

Edit the `EXERCISES` array in the `<script>` block of `abs.html`. Each entry has:
```js
{
  name: 'Exercise Name',      // must match key in IMAGES object
  equipment: 'Floor',
  detail: 'Execution cue...',
  tip: 'Coaching note...',
}
```
Also add the corresponding entry to the `IMAGES` object and upload the image to `images/`.

### To add a level

Edit the `LEVELS` array:
```js
{ name: 'Elite', hold: 60, meta: '2 rounds · ~20 min · 20s rest between exercises' }
```
Add a matching pill in the HTML home screen section.

### To change rest duration

Edit `REST_SECS` constant (default: `20`).

### To change number of rounds

Edit `ROUNDS` constant (default: `2`).

---

## index.html

Launcher page. Lists all apps as tappable cards.
Each card is an `<a>` tag with class `app-card`.
The `.app-icon.blue` modifier applies the blue background for the Abs app icon.
Future apps: copy a card block, update `href`, emoji, name, description.

---

## Design system

Both apps share the same CSS variable conventions:

| Variable | Role |
|----------|------|
| `--bg` / `--bg2` / `--bg3` | Background layers |
| `--text` / `--text2` / `--text3` | Text hierarchy |
| `--border` | Subtle borders |
| `--blue` / `--blue-dark` / `--blue-light` | Abs app accent |
| `--accent` | Launcher / Human Flag accent (teal) |

Dark mode overrides all variables via `@media (prefers-color-scheme: dark)`.

---

*Last updated: June 2026*
