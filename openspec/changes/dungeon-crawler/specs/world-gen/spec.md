## ADDED Requirements

### Requirement: Dungeon structure
The dungeon SHALL consist of 12 floors organized into 4 themed tiers: Catacombs (1-3), Mines (4-6), Sanctum (7-9), and Abyss+Throne (10-12). Each floor SHALL be a 30x30 tile grid.

#### Scenario: Floor generation
- **WHEN** a new floor is generated for depth N
- **THEN** the floor is a 30x30 grid with the theme corresponding to its tier, containing rooms, corridors, walls, and at least one staircase down (except floor 12)

### Requirement: BSP room generation
Floors 1-11 SHALL be generated using binary space partitioning (BSP) to create rooms of varying sizes. Rooms SHALL be connected by L-shaped corridors. Each floor SHALL have a minimum of 6 rooms and a maximum of 12 rooms.

#### Scenario: Room connectivity
- **WHEN** a floor is generated
- **THEN** every room is reachable from every other room via corridors (fully connected graph)

### Requirement: Vault injection
Each generated floor (1-11) SHALL have 1-2 rooms replaced with hand-crafted vault rooms. Vaults are pre-designed room layouts containing specific encounters, puzzles, or rewards. Vault selection SHALL be appropriate to the floor's tier and SHALL not repeat within a single run.

#### Scenario: Vault placement
- **WHEN** floor 3 is generated
- **THEN** 1-2 rooms in the BSP layout are replaced with tier-1 vault templates, preserving corridor connections to the rest of the floor

### Requirement: Boss floor
Floor 12 (The Throne) SHALL be entirely hand-crafted, not procedurally generated. It SHALL contain a fixed layout with the final boss encounter.

#### Scenario: Floor 12 layout
- **WHEN** the player descends to floor 12
- **THEN** the floor is the hand-crafted Throne layout with the Dracolich boss and no random elements

### Requirement: Tile types
The world SHALL support the following tile types: wall, floor, door (open/closed/locked), secret wall (appears as wall until discovered), stairs down, stairs up, pit trap (hidden/revealed), pressure plate, chest (open/closed/locked/trapped), fountain, and shrine.

#### Scenario: Door interaction
- **WHEN** the player faces a closed door and performs the interact action
- **THEN** the door opens if unlocked, or prompts for a key/lockpick if locked

#### Scenario: Secret wall discovery
- **WHEN** the player performs a search action adjacent to a secret wall
- **THEN** the secret wall is revealed as a passable doorway (WIS check to detect, DC based on floor depth)

### Requirement: Dungeon features
Each floor SHALL contain: doors (3-8 per floor), at least 1 secret wall, traps appropriate to the tier, treasure chests, and environmental features (fountains on early floors, shrines on later floors). Stairs down SHALL be placed in the room furthest from the stairs up / entrance.

#### Scenario: Trap placement
- **WHEN** floor 5 (Mines tier) is generated
- **THEN** the floor contains 2-4 pit traps placed in corridors, hidden until triggered or detected

### Requirement: Monster spawning
Each room (excluding the entry room of floor 1) SHALL be populated with 0-3 monsters from the tier-appropriate pool. Monster count and type SHALL scale with floor depth. Corridors have a 10% chance of containing a wandering monster.

#### Scenario: Tier-appropriate monsters
- **WHEN** a room on floor 5 is populated
- **THEN** monsters are drawn from the Tier 2 pool (Orc Warrior, Skeleton Knight, Ghoul, etc.) with occasional Tier 1 stragglers

### Requirement: Item placement
Treasure chests, monster drops, and floor loot SHALL be generated from loot tables tied to floor depth. Deeper floors yield better items. Quest-critical items (keys for locked doors) SHALL always be placed on the same floor as the lock they open.

#### Scenario: Loot scaling
- **WHEN** a chest on floor 8 is opened
- **THEN** the loot is drawn from the Tier 3 loot table, which includes magical weapons, better potions, and higher-value scrolls
