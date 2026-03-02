# CLAUDE.md — AI Assistant Guide for `index`

## Repository Overview

**Become Who You Are** — a philosophical self-improvement and accountability tracker built as a single-page HTML/CSS/JS application. Inspired by Aristotle and Nietzsche, it gamifies personal growth across five life domains with an XP/leveling system, streak tracking, emotional check-ins, grounding tools, and journaling.

## Project Structure

```
index/
├── CLAUDE.md          # This file — AI assistant guidelines
└── index.html         # Entire application (single-file SPA)
```

This is a **zero-dependency, single-file app**. All HTML, CSS, and JavaScript live in `index.html`. There is no build step, no bundler, no framework, and no package manager.

## Tech Stack

- **HTML5** — semantic markup, mobile-optimized viewport
- **CSS3** — custom properties, animations, gradients, responsive layout
- **Vanilla JavaScript** — no frameworks or libraries
- **Google Fonts** — EB Garamond (serif) and IBM Plex Mono (monospace), loaded via CDN
- **localStorage** — all user data persisted client-side under the key `philo_practice_v1`

## Development Setup

No build tools required. Open `index.html` in a browser, or serve it with any static file server:

```sh
# Option A: open directly
open index.html

# Option B: local server (Python)
python3 -m http.server 8000

# Option C: local server (Node)
npx serve .
```

## Application Architecture

### State Management

A single global state object `S` holds all UI and session state. The `render()` function re-renders the entire `#app` container on every state change (immediate-mode UI pattern).

Persistent data lives in `S.data` and is saved to localStorage via `sv()`. The app attempts migration from several older storage keys on load.

### Key Data Structures

- **`S.data.entries[]`** — Daily practice entries with responses, reflections, steps, gratitude
- **`S.data.checkins[]`** — Emotional check-in logs (emotion, trigger, body sensation, story)
- **`S.data.wins[]`** — Boundary win journal entries
- **`S.data.xp`** — Total experience points
- **`S.data.ua[]`** — Unlocked achievement IDs

### Five Domains (scored 1-3 per prompt)

| Domain | ID | Prompts |
|---|---|---|
| Emotional Regulation | `regulation` | 4 |
| Relationships & Boundaries | `boundaries` | 4 |
| Discipline & Daily Habits | `discipline` | 4 |
| Fitness & Body | `fitness` | 3 + step tracker |
| Identity & Self-Worth | `identity` | 4 |

### Tabs

1. **Practice** (`checkin`) — Daily domain scoring, reflections, gratitude, save for XP
2. **Tools** (`tools`) — Emotional check-in, grounding exercises (with box breathing), trigger log, boundary wins
3. **Trophies** (`achievements`) — Unlockable achievements based on streaks, entries, and milestones
4. **Wisdom** (`principles`) — Philosophical principles from Aristotle and Nietzsche
5. **Journey** (`journey`) — Historical view of all past entries with SVG ring charts

### XP & Leveling

10 levels from "Unexamined Life" (0 XP) to "Ubermensch" (5500 XP). XP earned from daily saves, prompt scores, reflections, step goals, challenges, achievements, and emotional check-ins.

### Key Functions

| Function | Purpose |
|---|---|
| `render()` | Full UI re-render from state |
| `saveEntry()` | Save daily practice, calculate XP, check achievements |
| `init()` | Load data, restore today's entry if exists, initial render |
| `gs()` | Calculate current streak |
| `gl(xp)` / `nl(xp)` | Get current / next level for XP value |
| `gc()` / `gq()` | Get daily challenge / quote (deterministic by date) |
| `ring()` | Generate SVG ring chart for domain scores |
| `saveCheckin()` | Log emotional check-in |
| `saveWin()` | Log boundary win |
| `startBreath()` | Start/stop box breathing timer |
| `exportData()` / `importData()` | JSON export/import of all user data |

## Code Conventions

- **Minified variable names** — The codebase uses short variable/function names (e.g., `sv` for save, `td` for today, `gl` for get-level). Maintain this style when editing existing code.
- **CSS class names** are also abbreviated (e.g., `.ctn` for container, `.hdr` for header, `.lvb` for level box). Follow existing naming patterns.
- **CSS custom properties** defined in `:root` — use `var(--g)` for gold, `var(--gl)` for gold-light, `var(--t)` for text, `var(--bg)` for background, etc.
- **String-based HTML rendering** — The `render()` function builds HTML via string concatenation. Follow this pattern rather than introducing DOM manipulation or templating.
- **No semicolons** are sometimes omitted; be consistent with surrounding code.
- **User input sanitization** — `.replace(/</g, "&lt;")` is used when rendering user text. Always sanitize user content when inserting into HTML strings.

## Git Workflow

- Write clear, descriptive commit messages summarizing the "why" not just the "what"
- Keep commits focused — one logical change per commit
- Push feature work to feature branches; open pull requests for review

## Guidelines for AI Assistants

1. **Read before writing.** Always read `index.html` before modifying it. Understand the render cycle and state model.
2. **Keep it single-file.** Do not split the app into multiple files unless explicitly asked. The single-file design is intentional.
3. **Match the style.** Use short variable names, abbreviated CSS classes, and string-concatenation rendering consistent with the existing code.
4. **Sanitize user input.** Any user-provided text rendered into HTML must be escaped to prevent XSS.
5. **Preserve localStorage compatibility.** Don't change the `philo_practice_v1` storage key or break the data schema without migration logic.
6. **No frameworks.** Don't introduce React, Vue, jQuery, or any library. This is vanilla JS by design.
7. **Test in browser.** The only way to test this app is to open it in a browser and interact with it. There is no test suite.
8. **Keep it simple.** Avoid over-engineering. This is a personal tool — favor directness over abstraction.
