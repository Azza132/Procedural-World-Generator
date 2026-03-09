# Procedural World Generator — User Guide
**v9.0 · Made by Aaron Sermon**

A single HTML file that runs entirely in your browser — no install, no server, no sign-in required. Open the file and a world is generated automatically. Every world is fully interactive, zoomable, customisable, and documented through the built-in World Codex.

---

## Quick Start

1. Open `world-generator.html` in any modern browser (Chrome, Firefox, Edge, Safari).
2. A world generates automatically on load.
3. Click **◆ Generate World** at any time to create a new one.
4. Scroll to zoom, click-drag to pan, double-click to reset the view.

---

## The Interface

The screen is divided into three areas:

- **Map (centre)** — the main interactive canvas
- **Sidebar (right)** — all controls, panels, and information
- **Footer (bottom)** — seed info and status

---

## Generating Worlds

### Random Generation
Click **◆ Generate World** in the sidebar. A new world is generated from a random seed. The seed is shown in the Seed panel — every seed always produces the exact same world.

### Using a Seed
In the **Seed** panel at the bottom of the sidebar, type any number or word into the text field and click **Use** (or press Enter). Words are hashed into a number automatically, so typing `myworld` always gives the same world.

### Map Size
In the **World Shape** panel, use the **Map Size** dropdown before generating:

| Option | Grid | Best for |
|---|---|---|
| Small | 80×80 | Quick preview, fast generation |
| Standard | 120×120 | Default balanced size |
| Large | 160×160 | Detailed regions |
| XL | 200×200 | Epic campaigns |
| Huge | 240×240 | Full continent maps |

Larger sizes take longer to generate, especially roads.

---

## Noise & Terrain Controls

These sliders shape the fundamental terrain before biomes are applied. Changes take effect on the next generation.

| Slider | What it does |
|---|---|
| **Octaves** | More octaves = more fine detail in the terrain |
| **Scale** | Lower = zoomed-in features; higher = broad sweeping terrain |
| **Domain Warp** | Twists the noise field to create more organic, chaotic coastlines |
| **Persistence** | How much each octave contributes; higher = rougher terrain |

---

## World Shape Controls

| Slider | What it does |
|---|---|
| **Sea Level** | Moves the water/land threshold; higher = more ocean |
| **Island Falloff** | Pushes elevation down near edges, creating island worlds |
| **Ridge Amount** | Blends in ridge noise to create sharper mountain chains |

---

## View Modes

Six overlay modes are available via the button row in the **Actions** panel:

| Mode | Shows |
|---|---|
| **Terrain** | Full biome-coloured map with hillshading |
| **Elev** | Greyscale elevation map |
| **Moisture** | Base atmospheric moisture before rain shadows |
| **Temp** | Temperature gradient from equator to poles |
| **Rainfall** | Actual precipitation after wind and rain shadows |
| **Wind** | Rainfall underlayer with wind direction arrows |

The **Wind** view shows three circulation bands colour-coded by latitude: yellow (trade winds near the equator), green (westerlies in the mid-latitudes), and pale blue (polar easterlies near the poles).

Toggle **⊞ Grid View** to switch between smooth bilinear scaling and crisp pixel-per-tile mode. Useful at high zoom levels for precise tile identification.

---

## Navigating the Map

| Action | Result |
|---|---|
| Mouse wheel scroll | Zoom in/out (smooth animated) |
| Click and drag | Pan the map |
| Double-click | Reset to full-world view |
| ⟲ Reset View button | Same as double-click |
| Click any tile | Inspect that tile in the sidebar |

The **Overview minimap** in the bottom-right corner shows the full world at all times, with a dashed rectangle indicating your current viewport. City markers and map pins are visible on the minimap.

The **zoom badge** (top-left of the map) shows the current zoom level. The **coordinate bar** (bottom-left) shows the tile under your cursor with biome, elevation, rainfall, temperature, and territory info in real time.

---

## Rivers

The river system uses realistic hydrology:

| Slider | What it does |
|---|---|
| **River Sources** | How many rivers to attempt |
| **Min Source Elev** | Rivers only start above this elevation threshold |
| **Min River Length** | Shorter rivers are discarded |

Rivers flow downhill following digital elevation model flow directions, pool-filling depressions, then smooth using Chaikin subdivision. They appear as glowing blue lines on the map.

Toggle **~~ Rivers Visible** to show or hide all rivers.

---

## Civilizations

| Slider | What it does |
|---|---|
| **Cities** | Number of cities to place |
| **Kingdoms** | Number of kingdoms to divide cities between |

Cities are placed using a terrain scoring system that prefers flat, fertile, accessible land with river access. Capitals are distributed using a max-min distance algorithm so kingdoms don't cluster together.

Roads connect cities to their kingdom capital and capitals to each other via A* pathfinding that follows valleys, avoids mountains, and shares corridors where possible. Major roads (between capitals) are thicker and brighter than minor roads.

Toggle **⚔ Civilizations Visible** or **⊘ Roads Visible** to show or hide each layer independently.

---

## Biomes

Twenty biome types are classified using elevation, rainfall (after wind and rain shadows), and temperature — similar to a Whittaker biome diagram. The **Biome Legend** panel lists all biomes present in the current world with their percentage coverage.

The **Elevation Profile** histogram shows the distribution of land elevation across the world. The vertical blue line marks sea level.

---

## Tile Inspector

Click any tile on the map to open the full inspector in the sidebar. It shows:

- **Coordinates** — X and Y position in the grid
- **Biome** and **group** type
- **Elevation**, **Temperature**, **Rainfall**, **Base Moisture** — with gradient bars
- **Wind direction** — based on the latitude atmospheric circulation model
- **River status** — whether this tile carries a river
- **Road status** — whether this tile is on a major or minor road
- **Kingdom territory** — which kingdom controls this tile (if any)
- **City info** — name and status if a city is here, or the nearest city and its distance

### Tile Notes
At the bottom of the Inspector is a **Tile Notes** text area. Type anything here to attach a note to that tile. Notes are saved automatically and appear as purple pin markers on the map and minimap. Zoom in to 1.5× or more to see the pin title label.

Click **📓 Open in World Codex** to jump directly to the Map Pins tab in the Codex.

---

## World Codex

Click **📓 Open World Codex** in the Actions panel (or press **Escape** to close it). This is a dedicated full-screen editor for all world customisation.

### World Tab
- **World Name** — Override the generated world name. Used everywhere the name appears.
- **Epithet** — Override the world's epithet (e.g. "The Ancient Realm").
- **World Notes** — A large free-form notes area for anything about the world: history, mythology, themes, secrets, campaign notes.

### Kingdoms Tab
One card per kingdom, colour-coded to match the map. For each kingdom you can:
- **Rename** the kingdom — the new name updates on the map labels, lore panel, and inspector immediately.
- **Write notes** — free-form text about the kingdom's culture, politics, history, etc.
- The card also shows the capital city, city count, and estimated population.

### Cities Tab
All cities grouped by kingdom. For each city you can:
- **Rename** the city — updates instantly on map labels and in the inspector.
- **Write notes** — background on this settlement.
- The card shows grid coordinates and the biome the city sits in.

### Map Pins Tab
Every tile that has a note attached is listed here. For each pin you can:
- Edit the **title** — shown as a label above the pin marker on the map at zoom ≥ 1.5×
- Edit the **note body** — the full text
- Click **✕ Remove** to delete the pin entirely

All changes in the Codex save automatically to your browser's localStorage, keyed to the world seed. The same seed always loads the same notes.

---

## Save & Load

The **Save & Load** panel stores up to 12 worlds persistently in your browser.

1. After generating, optionally type a name in the text field (auto-filled with the world name).
2. Click **Save** to store it.
3. Previously saved worlds appear as cards below. Click **Load** to restore them exactly.
4. **Double-click** a saved world's name to rename it inline.
5. Click **✕** on a card to delete that save.

Saves store the seed and all slider values, so the world is reproduced exactly — including custom names and notes (which are stored separately by seed in localStorage).

---

## World Lore

After generation the **World Lore** panel is populated automatically with:

- A generated world name and epithet
- Historical era and world age
- A timeline of events: founding wars, calamities, discoveries, alliances, prophecies
- Per-kingdom detail: founder, capital, population estimate, primary resource, and foreign relations with each other kingdom

Lore is generated deterministically from the seed and the world's actual terrain and kingdom configuration, so a world with more mountains will generate different events than a coastal world.

---

## Statistics Panel

The **Statistics** panel shows at a glance:
- Grid size and total tile count
- Land and water percentages
- Average elevation and number of active biomes
- River count and total river tiles
- City, kingdom, and road counts

---

## Tips

- **Seeds are everything.** If you find a world you like, note its seed — it's shown in the Seed panel and in the footer after generation. You can share seeds with others.
- **Word seeds work.** Type `dragon`, `northsea`, or your campaign name as a seed for memorable, repeatable worlds.
- **Notes are per-seed.** Custom names, tile notes, and Codex writing are stored against the seed in your browser. Loading the same seed restores all your customisation.
- **Combine views.** Generate a world in Terrain mode, then switch to Wind or Rainfall to understand why the deserts and forests ended up where they did.
- **Roads follow terrain.** Look at major roads to understand where the natural passes and valleys are — they're the paths of least resistance through mountains.
- **Zoom in on the minimap.** At high zoom the minimap becomes a useful reference for where you are on the world. Purple dots are your map pins.
- **The Codex is non-destructive.** Renaming a kingdom or city in the Codex doesn't change the underlying generated data — if you leave the name blank, the original generated name comes back.

---

## Technical Notes

- Runs entirely in the browser. No data is ever sent anywhere.
- All data (saves, notes) is stored in `localStorage` in your browser. Clearing browser data will erase saves and notes.
- Best experienced in a desktop browser at full screen. Mobile is functional but the sidebar is narrow.
- Generation time scales with map size. A Huge (240×240) world with many cities may take 5–10 seconds on slower machines, mostly due to road pathfinding.

---

*Procedural World Generator — v9.0 · Made by Aaron Sermon*
