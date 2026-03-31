# Asterisk JS

A minimal, single-file browser game built with vanilla HTML5 Canvas and JavaScript. Guide a glowing dot through a field of `*` asterisks, survive to the right edge, and rack up levels — all while leaving a permanent trail of where you've been.

---

## How to Play

Open `asterisk.html` in any modern browser. No install, no build step, no dependencies.

Click **Start Game** to begin.

### Controls

| Input | Action |
|---|---|
| Hold `Space` or `Enter` | Move **up** |
| Release | Move **down** |
| Tap and hold (mobile) | Move **up** |
| Release (mobile) | Move **down** |

The dot moves to the right automatically. Your only job is controlling the vertical axis.

### Goal

Reach the **right edge of the screen** without hitting any asterisks or the top/bottom walls. Do that and you advance to the next level.

---

## Game Mechanics

### Movement

The dot travels horizontally at a constant speed that increases each level. Vertically, the movement is binary — there is no gravity or momentum. When you hold the key, the dot moves up at a fixed rate. The instant you release, it moves down at the same rate. This produces a clean zigzag path.

### Obstacles

Each level is a fresh screen of randomly placed `*` asterisks. The number of asterisks grows with every level. A small safe zone at the left edge is always kept clear so you have a moment to orient yourself when a new level starts.

### The Trail

Every position the dot passes through is permanently painted onto the canvas as a glowing line. When you complete a level, your trail from that run stays on screen — slightly dimmed — as the next level loads on top of it. Over many levels, the canvas builds up a layered history of every path you've taken, with each difficulty tier drawn in a different color.

Trail colors by difficulty:

| Levels | Tier | Color |
|---|---|---|
| 1–3 | Easy | Green |
| 4–7 | Medium | Yellow |
| 8–12 | Hard | Orange |
| 13–18 | Very Hard | Red |
| 19+ | INSANE | Magenta |

### Difficulty Scaling

Each level increases:

- **Horizontal speed** — the dot moves faster across the screen
- **Vertical speed** — up/down snapping is faster, giving you less reaction time
- **Obstacle count** — starts at 6, adds 3 per level (so level 10 has 33 asterisks)

### Records

Your highest level reached is saved to `localStorage` along with your name. The record is displayed in the top-right corner and persists between sessions. If you beat the record, you'll be prompted to enter your name.

---

## Tips

- **Short taps beat long holds.** Because movement snaps instantly, a quick press-and-release produces a shallow V-shape. Long holds send you to the wall.
- **Read ahead.** Asterisks are static — scan where the gaps are before you commit to a direction.
- **The trail is a map.** Past trails show you paths that worked (or didn't). On later levels when the canvas is dense with previous runs, familiar corridors can guide you.
- **Survive the first second.** The safe zone only extends a short way from the left edge. Get your bearings fast.

---

## Technical Notes

- Pure HTML/CSS/JavaScript — one file, zero dependencies
- Two stacked `<canvas>` elements: one for the persistent trail, one for the live game layer (player + obstacles), cleared every frame
- Records stored in `localStorage` under keys `ast2_rl` and `ast2_rn`
- Runs at native display refresh rate via `requestAnimationFrame`
- Touch events supported for mobile play
