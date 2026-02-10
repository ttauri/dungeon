## ADDED Requirements

### Requirement: Depth-layered rendering
The first-person viewport SHALL render the dungeon as 3 depth layers (near, mid, far) using pre-drawn ASCII templates. Each layer shows walls, openings, doors, and entities at the correct visual depth with perspective narrowing.

#### Scenario: Empty corridor view
- **WHEN** the player faces north in a straight corridor 3+ tiles long with no entities
- **THEN** the viewport renders 3 nested rectangular frames showing walls converging to a vanishing point

#### Scenario: Dead end view
- **WHEN** the player faces a wall 1 tile ahead
- **THEN** the viewport renders a near-depth wall filling the view

### Requirement: Wall configuration templates
The renderer SHALL support wall templates for each combination of left-wall/right-wall/front-wall presence at each depth. Templates cover: corridor (walls on both sides), left turn (opening on left), right turn (opening on right), T-junction, crossroads, and dead end.

#### Scenario: Left turn visible
- **WHEN** the player faces north and there is an opening to the left at depth 1
- **THEN** the mid-depth layer shows a left wall opening (no wall on the left side at that depth)

### Requirement: Door rendering
Doors SHALL be rendered at the depth where they appear. Closed doors show a door frame with a visible door. Open doors show a door frame with passage visible beyond. Locked doors look identical to closed doors (player must try to interact to discover the lock).

#### Scenario: Closed door at depth 2
- **WHEN** a closed door exists 2 tiles ahead
- **THEN** the far-depth layer renders a door frame with a solid door surface using box-drawing characters

### Requirement: Monster rendering
Monsters SHALL be rendered as ASCII art sprites at their depth in the viewport. Near monsters (depth 0, adjacent) display full-size ASCII art (5-7 lines). Mid-depth monsters (depth 1) display medium art (3-4 lines). Far monsters (depth 2) display a small silhouette (1-2 lines).

#### Scenario: Adjacent monster
- **WHEN** an Orc is 1 tile ahead (depth 0)
- **THEN** the viewport renders the full-size Orc ASCII art prominently in the center of the view

#### Scenario: Distant monster
- **WHEN** a Skeleton is 3 tiles ahead (depth 2)
- **THEN** the viewport renders a small skeleton silhouette at far depth

### Requirement: Item rendering
Items on the floor (dropped loot, chests) SHALL be rendered at their depth as small ASCII symbols. Chests use a recognizable box character. Items on the ground use category-specific symbols.

#### Scenario: Chest visible at mid depth
- **WHEN** a closed chest is 2 tiles ahead on the floor
- **THEN** the viewport shows a small chest symbol at mid-depth on the floor area

### Requirement: Viewport dimensions
The first-person viewport SHALL render within a fixed area of approximately 40 columns × 18 rows, designed to fit alongside the stats panel and above the minimap in an 120×40 terminal layout.

#### Scenario: Terminal sizing
- **WHEN** the game runs in a 120×40 terminal
- **THEN** the viewport, stats panel, minimap, and game log all fit without overlap or truncation
