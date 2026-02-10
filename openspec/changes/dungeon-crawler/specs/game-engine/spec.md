## ADDED Requirements

### Requirement: Turn-based game loop
The engine SHALL process the game as a sequence of discrete turns. Each turn, the player submits one action, the engine resolves it, then all monsters take their actions. The turn counter SHALL increment after all actions resolve.

#### Scenario: Player takes a turn
- **WHEN** the player submits a valid action (move, attack, cast, use item, interact, search)
- **THEN** the engine resolves the player action, resolves all monster actions, increments the turn counter, and returns the updated game state

#### Scenario: Invalid action
- **WHEN** the player submits an action that cannot be performed (e.g., move into a wall, attack with no target)
- **THEN** the engine rejects the action with an error message and does not advance the turn

### Requirement: Game state encapsulation
The engine SHALL expose game state through a `Game` struct with a `Do(action Action) Result` method. All game logic SHALL be contained within the engine and its sub-packages. Neither TUI nor API code SHALL modify game state directly.

#### Scenario: Action dispatch
- **WHEN** any consumer (TUI or API) calls `Game.Do(action)`
- **THEN** the engine processes the action and returns a `Result` containing the new observable state, log entries, and any error

### Requirement: Seeded random number generation
The engine SHALL accept an optional seed at game creation. All random decisions (map generation, combat rolls, loot drops, monster behavior) SHALL use this seed. The same seed and same action sequence SHALL produce identical game states.

#### Scenario: Reproducible run
- **WHEN** two games are created with the same seed, class, and action sequence
- **THEN** both games produce identical state at every turn

#### Scenario: Random seed
- **WHEN** no seed is provided at game creation
- **THEN** the engine generates a random seed and includes it in the game state for later reproduction

### Requirement: Game lifecycle
The engine SHALL support creating a new game with a character name, class selection, and optional seed. The game ends when the player character dies or defeats the final boss on floor 12.

#### Scenario: New game creation
- **WHEN** a new game is created with name "Kael", class "fighter", seed 42
- **THEN** the engine initializes a level 1 fighter on floor 1 with generated dungeon and returns the initial state

#### Scenario: Character death
- **WHEN** the player's HP reaches 0
- **THEN** the game enters a "game over" state and no further actions are accepted

#### Scenario: Victory
- **WHEN** the player defeats the boss on floor 12
- **THEN** the game enters a "victory" state with final stats summary

### Requirement: Observable state
The engine SHALL provide the current observable state after each action. Observable state includes only what the player character can perceive: visible tiles (based on field of vision), known map (previously explored tiles), current stats, inventory, and recent log entries. The engine SHALL NOT expose hidden map data, unexplored rooms, or monster stats beyond what the character can observe.

#### Scenario: Fog of war in state
- **WHEN** the player requests game state
- **THEN** the state includes visible tiles (current FOV), explored tiles (previously seen, may be stale), and omits unexplored areas entirely
