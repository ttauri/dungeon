## ADDED Requirements

### Requirement: Four-panel layout
The TUI SHALL display four panels simultaneously: first-person viewport (top-left), character stats (top-right), minimap (bottom-left), and game log (bottom-right). All panels SHALL update after each turn.

#### Scenario: Layout rendering
- **WHEN** the game is running in TUI mode
- **THEN** all four panels are visible and correctly positioned with border separators

### Requirement: Bubbletea architecture
The TUI SHALL be built using the bubbletea framework with each panel as an independent sub-model. The root model SHALL compose panels and route keyboard input to the appropriate handler.

#### Scenario: Panel composition
- **WHEN** the game state updates after a turn
- **THEN** the root model dispatches the new state to all four sub-models and re-renders the full screen

### Requirement: Keyboard input
The TUI SHALL accept the following default key bindings: W (move forward), S (move backward), A (turn left), D (turn right), E (interact with facing tile), I (open inventory), C (character sheet), X (search for secrets), space (attack facing enemy), 1-7 (cast spell by slot), Q (quaff potion), ESC (quit/close overlay), ? (help screen).

#### Scenario: Movement input
- **WHEN** the player presses W
- **THEN** the TUI sends a "move forward" action to the engine and re-renders with updated state

#### Scenario: Inventory overlay
- **WHEN** the player presses I
- **THEN** an inventory overlay appears showing all carried items with equip/use/drop options, and gameplay input is paused until ESC closes it

### Requirement: Character stats panel
The stats panel SHALL display: character name, class, and level; HP bar (visual bar + numeric); MP/spell slots remaining; all 6 ability scores with modifiers; AC; XP and progress to next level; equipped weapon, armor, and shield; active conditions with remaining duration.

#### Scenario: Stats display
- **WHEN** a level 3 Fighter has 28/35 HP, AC 17, and is poisoned (2 turns remaining)
- **THEN** the stats panel shows a green HP bar at 80%, "AC: 17", "POISONED (2)" in a highlighted color, and all equipped gear

### Requirement: Game log panel
The game log SHALL display the most recent game events as scrollable text. New events appear at the bottom. The log SHALL show combat rolls, damage, item pickups, environmental descriptions, and trap activations. The player can scroll up to review previous entries.

#### Scenario: Combat log entries
- **WHEN** the player attacks a Goblin, rolls 17, hits for 9 damage
- **THEN** the log shows: "You swing your longsword at the Goblin. Roll: 17 + 5 = 22 vs AC 13. Hit! 9 damage."

#### Scenario: Environmental description
- **WHEN** the player enters a new room
- **THEN** the log shows a brief room description: "You enter a damp chamber. Moss clings to the crumbling walls. A chest sits in the far corner."

### Requirement: Color and styling
The TUI SHALL use ANSI colors for visual clarity: red for damage/danger, green for healing/HP, blue for magic/MP, yellow for gold/loot, white for normal text, dim gray for explored-but-not-visible areas. Box-drawing characters (─│┌┐└┘├┤┬┴┼) SHALL be used for borders and panel separation.

#### Scenario: Damage highlighting
- **WHEN** the player takes damage
- **THEN** the damage number appears in red in the log and the HP bar updates with the lost portion shown in red

### Requirement: Minimum terminal size
The TUI SHALL require a minimum terminal size of 100×30 characters. If the terminal is smaller, a message SHALL be displayed asking the user to resize. Target layout is optimized for 120×40.

#### Scenario: Terminal too small
- **WHEN** the game starts in an 80×24 terminal
- **THEN** a centered message reads "Terminal too small. Minimum: 100×30. Current: 80×24. Please resize."

### Requirement: Game over and victory screens
On character death, the TUI SHALL display a game over screen with final stats (floor reached, monsters killed, turns taken, gold collected). On victory, a victory screen with the same stats plus a congratulatory message.

#### Scenario: Game over screen
- **WHEN** the player dies on floor 7
- **THEN** a full-screen overlay shows "YOU HAVE PERISHED" with stats: Floor 7, 89 monsters slain, 342 turns, 1240 gold
