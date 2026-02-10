## ADDED Requirements

### Requirement: Fog-of-war automap
The minimap SHALL display a top-down view of the current floor showing explored tiles, with unexplored areas hidden. Tiles currently in the player's field of vision are shown at full brightness. Previously explored but not currently visible tiles are shown dimmed.

#### Scenario: Exploration reveal
- **WHEN** the player enters a new room
- **THEN** all tiles within FOV are revealed on the minimap and remain visible (dimmed) even after the player leaves

#### Scenario: Unexplored areas
- **WHEN** the player has only explored the first 3 rooms of a floor
- **THEN** the minimap shows those 3 rooms and connecting corridors; all other areas are blank/hidden

### Requirement: Minimap symbols
The minimap SHALL use the following symbols: `@` for player position (with facing indicator), `.` for floor, `#` for wall, `+` for closed door, `/` for open door, `>` for stairs down, `<` for stairs up, `^` for revealed trap, `!` for visible monster (in current FOV only), `*` for visible item (in current FOV only).

#### Scenario: Player position with facing
- **WHEN** the player is at position (5,3) facing east
- **THEN** the minimap shows `@` at (5,3) with an east-facing indicator (e.g., `@>` or colored arrow)

### Requirement: Minimap dimensions
The minimap SHALL fit within approximately 32×16 characters. If the full 30×30 floor doesn't fit, the minimap SHALL be centered on the player's position and scroll as they move.

#### Scenario: Large floor scrolling
- **WHEN** the player is at position (25, 25) on a 30×30 floor
- **THEN** the minimap viewport centers on the player, showing the surrounding area within the 32×16 display

### Requirement: FOV calculation
The player's field of vision SHALL extend in a cone of 5 tiles in the facing direction and 1 tile to each side. In corridors, FOV extends to the first wall or corner. In rooms, FOV reveals the full room if the player is inside it.

#### Scenario: Corridor FOV
- **WHEN** the player faces north in a 7-tile straight corridor
- **THEN** FOV reveals the first 5 tiles ahead (or up to the first wall/turn, whichever is closer)

#### Scenario: Room FOV
- **WHEN** the player enters a 6×6 room
- **THEN** the entire room is revealed in FOV regardless of facing direction
