## 1. Project Scaffolding

- [ ] 1.1 Initialize Go module (`go mod init`), create package directory structure per design (cmd/dungeon, engine, world, combat, entity/player, entity/monster, magic, item, fov, tui, api, data)
- [ ] 1.2 Add dependencies: bubbletea, lipgloss, gorilla/websocket
- [ ] 1.3 Create `cmd/dungeon/main.go` with CLI flag parsing: `--api` (bool), `--port` (int), `--seed` (int64)

## 2. Core Data Types

- [ ] 2.1 Define tile types (wall, floor, door, secret wall, stairs, pit trap, pressure plate, chest, fountain, shrine) and the map grid struct in `world/`
- [ ] 2.2 Define ability scores, modifiers, and the character stat block in `entity/player/`
- [ ] 2.3 Define the 4 class definitions (Fighter, Rogue, Cleric, Wizard) with hit dice, proficiencies, starting equipment, and level-up tables
- [ ] 2.4 Define item types (weapons, armor, shields, potions, scrolls, keys, gold) with all weapon/armor stat tables in `item/`
- [ ] 2.5 Define spell definitions (7 Wizard, 6 Cleric) with slot levels, effects, and targeting rules in `magic/`
- [ ] 2.6 Define monster stat blocks for all 36 monsters with behavior tags, stats, and tier assignments in `data/`
- [ ] 2.7 Define the Action and Result types used by `Game.Do()` — all action variants (move, attack, cast, use_item, interact, search, equip, turn)

## 3. Dice and Combat Engine

- [ ] 3.1 Implement seeded RNG wrapper with dice rolling functions (d4, d6, d8, d10, d12, d20, NdX) in `combat/`
- [ ] 3.2 Implement initiative calculation (d20 + DEX mod, ties favor player)
- [ ] 3.3 Implement attack roll resolution (d20 + mod + proficiency vs AC, natural 1/20 handling, critical hit double dice)
- [ ] 3.4 Implement damage calculation (weapon die + ability mod, critical damage)
- [ ] 3.5 Implement saving throw system (d20 + ability mod vs DC)
- [ ] 3.6 Implement AC calculation (base armor + DEX mod cap + shield + magic bonus)
- [ ] 3.7 Implement condition system (poisoned, stunned, paralyzed, frightened, slowed, blinded) with duration tracking and per-turn resolution
- [ ] 3.8 Implement XP award and level-up logic (proficiency scaling, HP gain, class feature unlocks)

## 4. Entity Systems

- [ ] 4.1 Implement character creation: 4d6-drop-lowest ability generation, class selection, starting equipment assignment
- [ ] 4.2 Implement inventory system: backpack (20 slots), equipment slots (weapon, armor, shield, ring, amulet), equip/unequip actions
- [ ] 4.3 Implement class features: Fighter extra attack + action surge, Rogue sneak attack + evasion, Cleric turn/destroy undead, Wizard arcane recovery
- [ ] 4.4 Implement spell slot management: slot tracking per level, consumption on cast, recovery on rest
- [ ] 4.5 Implement spell effects: Magic Missile (auto-hit multi-dart), Shield (+5 AC), Sleep (HP-based), Fireball/Lightning Bolt (area/line + DEX save), Cure Wounds/Heal, Bless, Protection from Evil, Turn Undead, Detect Magic, Knock, Flame Strike
- [ ] 4.6 Implement monster AI behavior loop: evaluate behavior tags in priority order, select action (attack, cast, flee, charge, summon, special)
- [ ] 4.7 Implement specific monster behaviors: Pack (+1 per ally), Ambusher (surprise round), Berserker (damage boost when hurt), Regenerator (heal per turn, fire vulnerability), Engulfer, Phaser, Charger, Fleeing, Corroder (equipment damage + DEX save)
- [ ] 4.8 Implement equipment durability for Rust Monster interaction (normal → worn → broken → destroyed)

## 5. World Generation

- [ ] 5.1 Implement BSP room partitioning for 30x30 grid (min 6, max 12 rooms per floor)
- [ ] 5.2 Implement L-shaped corridor carving connecting all BSP rooms (ensure full connectivity)
- [ ] 5.3 Implement door placement on corridor-room boundaries (3-8 per floor, some locked with keys placed on same floor)
- [ ] 5.4 Implement stair placement (stairs down in room furthest from entry, stairs up at entry)
- [ ] 5.5 Implement vault system: define 3-4 vault templates per tier, replace random rooms with vaults preserving corridor connections
- [ ] 5.6 Implement trap placement: pit traps in corridors (hidden until triggered/detected), pressure plates, scaling with floor depth
- [ ] 5.7 Implement secret wall placement (at least 1 per floor, WIS check to detect)
- [ ] 5.8 Implement monster spawning per room (0-3 from tier pool, scaling with depth, 10% corridor wanderers)
- [ ] 5.9 Implement loot/chest placement using tier-appropriate loot tables
- [ ] 5.10 Implement floor 12 (The Throne) as a fixed hand-crafted boss layout with Dracolich encounter
- [ ] 5.11 Implement tier theming: Catacombs (1-3), Mines (4-6), Sanctum (7-9), Abyss+Throne (10-12) with appropriate feature distribution

## 6. Field of Vision

- [ ] 6.1 Implement FOV calculation: 5-tile cone in facing direction, 1 tile to each side, corridor line-of-sight to first wall/corner
- [ ] 6.2 Implement room reveal: entering a room reveals all tiles in that room regardless of facing
- [ ] 6.3 Implement fog-of-war state tracking: tiles are unexplored, explored (dimmed), or visible (current FOV)

## 7. Game Engine Integration

- [ ] 7.1 Implement the `Game` struct and `Game.Do(action) Result` method as the single entry point for all game logic
- [ ] 7.2 Implement turn processing loop: validate action → resolve player action → resolve all monster actions → update FOV → increment turn → return state
- [ ] 7.3 Implement game lifecycle: new game creation (name, class, seed), game over on death, victory on floor 12 boss defeat
- [ ] 7.4 Implement observable state generation: filter game state to only player-perceivable information (FOV, explored map, known entities)
- [ ] 7.5 Implement rest mechanics: short rest at safe rooms (spend hit dice to heal, Wizard arcane recovery), long rest at stairwells (full HP/slot restore)
- [ ] 7.6 Implement game log system: combat rolls, damage, item pickups, room descriptions, trap activations — stored as structured entries

## 8. First-Person ASCII Renderer

- [ ] 8.1 Design and implement wall templates for all configurations (corridor, left/right turn, T-junction, crossroads, dead end) at 3 depths using box-drawing characters
- [ ] 8.2 Implement depth-layer compositing: render far layer first, overlay mid, overlay near
- [ ] 8.3 Implement door overlay rendering at each depth (open/closed door frames)
- [ ] 8.4 Create ASCII art sprites for all 36 monsters at 3 sizes (near: 5-7 lines, mid: 3-4 lines, far: 1-2 lines) — start with Tier 1 (9 monsters)
- [ ] 8.5 Create ASCII art sprites for Tier 2 monsters (9 monsters, 3 sizes each)
- [ ] 8.6 Create ASCII art sprites for Tier 3 monsters (9 monsters, 3 sizes each)
- [ ] 8.7 Create ASCII art sprites for Tier 4 monsters (9 monsters, 3 sizes each)
- [ ] 8.8 Implement item rendering at depth (chest symbols, loot symbols on floor)
- [ ] 8.9 Implement entity compositing into the viewport (monsters/items rendered at correct depth position)

## 9. Terminal UI (Bubbletea)

- [ ] 9.1 Implement root model with four-panel layout using lipgloss (viewport top-left, stats top-right, minimap bottom-left, log bottom-right)
- [ ] 9.2 Implement first-person viewport panel (wraps the ASCII renderer from section 8)
- [ ] 9.3 Implement character stats panel: name/class/level, HP bar, spell slots, ability scores, AC, XP, equipped gear, conditions
- [ ] 9.4 Implement minimap panel: fog-of-war automap with symbols (@, ., #, +, /, >, <, ^, !, *), player facing indicator, scroll on large maps
- [ ] 9.5 Implement game log panel: scrollable text area, color-coded entries (red damage, green healing, blue magic, yellow loot)
- [ ] 9.6 Implement keyboard input routing: movement (WASD), actions (E, X, space), UI (I, C, ?, ESC), spells (1-7), potions (Q)
- [ ] 9.7 Implement inventory overlay: item list with equip/use/drop actions, closes with ESC
- [ ] 9.8 Implement character sheet overlay: detailed stats view
- [ ] 9.9 Implement game over and victory screens with final stats (floor, kills, turns, gold)
- [ ] 9.10 Implement terminal size detection and minimum size enforcement (100×30 minimum, 120×40 target)
- [ ] 9.11 Implement ANSI color styling: damage red, healing green, magic blue, loot yellow, dim gray for fog-of-war

## 10. REST + WebSocket API

- [ ] 10.1 Implement HTTP server setup with routing (stdlib net/http or gorilla/mux)
- [ ] 10.2 Implement POST /api/v1/game/new — create game with name, class, optional seed; return initial state
- [ ] 10.3 Implement GET /api/v1/state — return current observable game state as JSON
- [ ] 10.4 Implement POST /api/v1/action — submit action, return result + new state + log entries
- [ ] 10.5 Implement GET /api/v1/log — return recent log entries with limit parameter
- [ ] 10.6 Implement GET /api/v1/game/info — return game metadata, status, and available actions
- [ ] 10.7 Implement GET /api/v1/ws/watch — WebSocket upgrade, stream state after each turn
- [ ] 10.8 Implement API error handling: JSON error format with error/code fields, proper HTTP status codes
- [ ] 10.9 Implement JSON serialization for all game state types (player, map, entities, log entries)

## 11. Integration and Polish

- [ ] 11.1 Wire TUI mode: main.go → bubbletea app → engine, keyboard → actions → re-render
- [ ] 11.2 Wire API mode: main.go → HTTP server → engine, REST/WS → actions → JSON responses
- [ ] 11.3 Implement character creation screen in TUI (name input, class selection, ability score display)
- [ ] 11.4 Add room description generation (short atmospheric text for each room type/theme)
- [ ] 11.5 Balance pass: playtest all 4 classes through floors 1-3, adjust monster HP/damage/XP curves
- [ ] 11.6 Add help screen (? key) showing all keybindings and game commands
