## Why

Build a first-person dungeon crawler in the style of Eye of the Beholder — a grid-based, turn-based RPG with ASCII terminal graphics, light D&D 5e rules, and a single-character focus. The game serves dual purposes: a playable retro dungeon crawl for humans, and an API-driven testbed for AI agents to exercise and balance game mechanics through automated play.

## What Changes

- New standalone game application written in Go
- Terminal UI with first-person depth-layered ASCII view, minimap, character stats panel, and game log
- Procedurally generated dungeon (12 floors, 30x30 grids) with hand-crafted vault rooms dropped into the layout
- D&D-lite combat system: d20 attack rolls, ability scores, AC, saving throws, spell slots
- 4 playable classes: Fighter, Rogue, Cleric, Wizard — each with distinct dungeon survival strategies
- 36 monster types across 4 tiers, each with unique combat behaviors and mechanics
- Item system: weapons, armor, potions, scrolls, and dungeon interactables (doors, chests, traps, secrets)
- Character progression: levels 1-10 with class-specific abilities
- REST + WebSocket API enabling programmatic play by AI agents
- Seeded RNG for reproducible runs (critical for balance testing)

## Capabilities

### New Capabilities

- `game-engine`: Core game loop, turn processing, state management, and seeded RNG
- `world-gen`: Procedural dungeon generation with floors, rooms, corridors, vaults, and dungeon features (traps, secrets, doors, stairs)
- `combat-system`: D20-based combat — initiative, attack rolls, damage, saving throws, conditions, and death
- `entity-model`: Player character (classes, abilities, leveling, inventory) and monster definitions (36 types with distinct AI behaviors)
- `spell-system`: Spell slots, spell effects, class spell lists for Cleric and Wizard
- `item-system`: Weapons, armor, potions, scrolls, keys, and loot tables tied to dungeon depth
- `first-person-view`: Depth-layered ASCII renderer showing walls, doors, monsters, and items from first-person perspective
- `terminal-ui`: Full terminal interface — first-person view, minimap, stats panel, game log, input handling via bubbletea
- `game-api`: REST endpoints (GET /state, POST /action, GET /log) and WebSocket /watch for agent play and live observation
- `minimap`: Fog-of-war automap revealing explored tiles, showing player position and orientation

### Modified Capabilities

_(none — greenfield project)_

## Impact

- **New repository content**: Entire Go project scaffolded from scratch in the dungeon repo
- **Dependencies**: Go 1.22+, bubbletea (TUI), lipgloss (styling), standard library net/http (API), gorilla/websocket
- **No external services**: Fully self-contained, no database, no network dependencies beyond the optional API server
- **Build targets**: Single binary `dungeon` with CLI flags for TUI mode vs API-server mode
