# 🌾 Farm Match

**Match. Harvest. Build Your Dream Farm.**

A self-contained, premium-feel Match-3 farming game — playable entirely from a single HTML file, no install or build step required.

## How to run

1. Open `farm-match.html` in any modern browser (Chrome, Safari, Firefox, Edge).
2. Works on desktop, tablet, and mobile (tap or click).
3. That's it — no server, no dependencies.

Your progress (coins, gems, stars, completed levels, farm buildings, boosters, quests, achievements, settings) saves automatically as you play and is restored the next time you open the file in the same environment.

## What's included

- **Match-3 engine** — 8×8 board, tap-to-select-and-swap, cascades with a combo multiplier, and special crops:
  - Match 4 → **Row/Column Harvester** (clears a full line)
  - Match 5 → **Golden Seed** (clears every crop of that type)
  - L/T-shaped match → **Farm Bomb** (clears a 3×3 area)
  - Weed obstacles that clear when a crop next to them is matched
  - Automatic shuffle if no valid move remains
- **20 data-driven levels** in the Green Meadow world, generated from a difficulty curve (simple harvest goals → multi-crop goals with weeds → score-attack goals with fewer moves), star ratings, and per-level rewards
- **Farm progression** — unlockable land plots, 11 upgradable buildings (Farmhouse, Barn, Chicken Coop, Cow Shed, Vegetable Garden, Windmill, Water Tower, Market, Bakery, Workshop, Orchard), Farm Level & XP
- **Meta-game systems**:
  - Quests (rotating pool, claimable rewards)
  - Achievements (auto-tracked, claimable)
  - Shop — spend coins/gems on boosters (Extra Moves, Farm Hammer, Rainbow Seed, Tractor, Water Bucket) or an extra life
  - 7-day daily login reward cycle
  - Lives system with time-based regeneration
  - Settings — music/sound toggle, reduced-motion mode, reset progress
  - A short first-time tutorial on Level 1
- **Persistent save** using the app's built-in storage — refreshing or reopening the file does not reset progress
- Lightweight generated sound effects (Web Audio) — no external audio files needed

## Architecture notes

Everything lives in one HTML file for portability, but the code is organized into clearly separated sections that mirror a modular design:

- `Engine` — board generation, match detection, gravity/refill, no-move detection
- `Levels` — data-driven level generator (`Levels.generate(id)`), easy to extend well past 20 levels
- `ACHIEVEMENTS` / `QUEST_POOL` / `SHOP_ITEMS` / `BUILDINGS` / `LAND_PLOTS` / `DAILY_REWARDS` — plain data tables, easy to tune or extend
- `Audio2` — small Web Audio helper for sound effects
- `State` + `loadState()` / `queueSave()` — save/load layer, structured so a real backend could replace the storage calls later
- `Game` — the active runtime for whichever level is currently in progress
- UI render functions (`renderMap`, `renderFarm`, `renderQuests`, `renderShop`, `renderAchievements`, `renderSettings`, `renderBoard`, etc.) — one function per screen

## Known limitations (honest scope notes)

- 20 levels are included (not the full 500+ envisioned); the level generator is built so adding more is a one-line change to `Levels.TOTAL` plus tuning the generator's tiers.
- Farm decorations and wandering animals are represented in the data model but don't yet have a drag-and-drop placement UI.
- Sound is generated tones for feedback (selects, matches, combos, wins/losses) rather than produced music tracks or sound design assets.
- Only one world ("Green Meadow") is active; the level generator already tags a `world` field per level so more worlds can be added without restructuring.

## File list

- `farm-match.html` — the complete game
- `README.md` — this file
