# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

**Pop!** — A full-screen toddler game (ages 2–4) where children click/tap colorful circles that explode into the background color. Single HTML file, no build step, no dependencies.

## Running locally

```bash
npx serve -p 3000 .
# open http://localhost:3000
```

The `.claude/launch.json` is already configured — use `preview_start` with the `pop-game` config to serve it in the preview panel.

## Deploying

Push to `main` and GitHub Pages auto-deploys within ~1 minute:
```bash
git add index.html && git commit -m "..." && git push
```
Live URL: https://ibrahimghailani.github.io/toddler-mouse/

## Architecture

Everything lives in `index.html` — no framework, no build tooling, vanilla JS + CSS.

**Three screens** (CSS `display` toggled):
- `#mode-screen` — Endless vs Survival picker shown on launch
- `#game-screen` — the active game
- `#gameover-screen` — survival end state with score

**Game modes:**
- **Endless** — fixed circle size (20% of `min(vw, vh)`), runs forever
- **Survival** — circle shrinks by 3% every 10 clicks *or* every 60 seconds (whichever comes first); game ends when size hits 5%

**Core loop (`onCircleClick`):**
1. Play chime via Web Audio API (each color maps to a pentatonic note)
2. Trigger CSS `pop` animation (circle scales ×30 to flood the screen)
3. At 160 ms: swap `document.body` background to the circle's color
4. At 320 ms: check survival shrink logic → reposition circle with `appear` bounce animation

**Color system:** 8 curated colors in the `COLORS` array. `pickColor(exclude)` always picks a color different from the current background so circle and bg never clash.

**Audio:** Web Audio API only — no audio files. `playChime(colorIndex)` creates a sine oscillator with a frequency glide and fast gain envelope. AudioContext is lazily created on first interaction (required for iOS autoplay policy).

## Key constants (top of `<script>`)

| Constant | Default | Purpose |
|---|---|---|
| `START_SIZE` | 20 | Starting circle size as % of min(vw,vh) |
| `MIN_SIZE` | 5 | Size at which survival game ends |
| `SHRINK_BY` | 3 | Percentage points lost per shrink event |
| `CLICKS_PER_SHRINK` | 10 | Clicks before survival shrinks |
| `LEVEL_TIME` | 60 | Seconds before auto-shrink in survival |
