# Text Adventure Game — Web Build

This repository contains a **browser-playable web build** of the Text Adventure Game.
The web version runs entirely client-side with PyScript/Pyodide and uses a button-driven UI (no terminal input required).

> Looking for the terminal version? The classic CLI game still exists, but this README documents the **web build only**.

---

## Quick Start (Web)

From the project root:

```bash
python3 -m http.server 8080
```

Then open:

- `http://localhost:8080/web/index.html`

On first load, PyScript downloads the Pyodide runtime. After that, it is typically cached by your browser.

---

## Web Build Features

| Feature | Status |
|---|---|
| Character creation (name + class) | ✅ |
| World map navigation | ✅ |
| Town services (Shop, Bank, Rest) | ✅ |
| Turn-based combat + class abilities | ✅ |
| Random world events | ✅ |
| Inventory + potion use + equipment | ✅ |
| Fields gathering (herbs) | ✅ |
| Mines gathering (ore) | ✅ |
| Dungeon gameplay loop | ✅ |
| Save / Load in browser flow | ✅ |

---

## Controls (Web UI)

The web build is fully click-driven:

- Use **menu buttons** to travel, open systems, and progress encounters.
- In combat, use **action buttons** (attack, defend, dodge, potion, abilities, escape).
- Use **inventory/equipment buttons** to consume potions and equip gear.

There are no typed commands required for normal gameplay in the web build.

---

## Web Architecture

```text
web/
  index.html      # App shell + panel layout + PyScript bootstrap
  main.js         # Browser-side glue for UI wiring / lifecycle helpers
  style.css       # Web styling and responsive layout
  web_game.py     # Main web controller and state transitions
  state.py        # Session/game state container
  screens.py      # Screen rendering helpers
  ui.py           # Shared UI update utilities
  combat.py       # Combat flow for web state machine
  events.py       # Random event handlers
  shop.py         # Shop interactions
  bank.py         # Bank interactions
  dungeon.py      # Dungeon loop and rewards
  save.py         # Save/load behavior for the web build
```

The web build reuses core game data and systems while adapting interaction to a non-blocking, event-driven browser loop.

---

## Troubleshooting

### PyScript assets fail to load

If the PyScript CDN version in `web/index.html` changes or is deprecated, update the `core.css` and `core.js` URLs to a valid release from:

- <https://pyscript.net>

### Opening the wrong page

If you open the repository root (`/`) you may not see the game UI. Be sure to open:

- `http://localhost:8080/web/index.html`

---

## Project Notes

- The web build is intended to be the primary player-facing experience documented here.
- Keep web docs in sync with `web/` feature behavior when adding systems or changing flows.
