## ADDED Requirements

### Requirement: Spell slot system
Clerics and Wizards SHALL have spell slots that determine how many spells they can cast before resting. Spell slots scale with level. Slots are consumed when a spell is cast and restored on long rest. Wizards regain one slot on short rest via Arcane Recovery.

#### Scenario: Spell slot consumption
- **WHEN** a level 3 Wizard (2 level-1 slots, 1 level-2 slot) casts Magic Missile (level 1)
- **THEN** one level-1 slot is consumed, leaving 1 level-1 slot and 1 level-2 slot

#### Scenario: Spell slot recovery on long rest
- **WHEN** the player takes a long rest at a stairwell
- **THEN** all spell slots are restored to maximum

### Requirement: Wizard spell list
The Wizard SHALL have access to the following spells: Magic Missile (auto-hit, 3×d4+1 force damage), Shield (reaction: +5 AC for one attack), Sleep (2d8 HP of creatures fall asleep), Detect Magic (reveal magical items/traps in FOV), Knock (open one locked door/chest), Lightning Bolt (8d6 damage in a line, DEX save for half), Fireball (8d6 fire damage in area, DEX save for half).

#### Scenario: Magic Missile cast
- **WHEN** the Wizard casts Magic Missile at a Goblin
- **THEN** 3 darts hit automatically, each dealing d4+1 force damage (no attack roll)

#### Scenario: Fireball cast
- **WHEN** the Wizard casts Fireball targeting a room with 3 Orcs
- **THEN** each Orc makes a DEX saving throw (DC = 8 + INT mod + proficiency); on failure takes 8d6 fire damage, on success takes half

### Requirement: Cleric spell list
The Cleric SHALL have access to the following spells: Cure Wounds (heal d8 + WIS mod HP), Bless (+d4 to attack rolls for 10 turns), Protection from Evil (undead/demons have disadvantage attacking you for 10 turns), Turn Undead (all undead in FOV make WIS save or flee for 3 turns), Heal (heal 4d8 + WIS mod HP), Flame Strike (4d6 fire + 4d6 radiant damage, DEX save for half).

#### Scenario: Cure Wounds cast
- **WHEN** the Cleric casts Cure Wounds with WIS mod +3
- **THEN** the player heals d8+3 HP, not exceeding max HP

#### Scenario: Turn Undead
- **WHEN** the Cleric uses Turn Undead and 2 Skeletons are in FOV
- **THEN** each Skeleton makes a WIS save (DC = 8 + WIS mod + proficiency); on failure it flees for 3 turns

### Requirement: Spell targeting
Spells that target enemies SHALL require the target to be visible (within FOV). Area spells (Fireball, Flame Strike) affect all creatures in the targeted area. Self-targeting spells (Shield, Bless) affect only the caster.

#### Scenario: Blocked line of sight
- **WHEN** the Wizard attempts to cast Lightning Bolt at a monster behind a closed door
- **THEN** the spell cannot be cast and the action is rejected

### Requirement: Spell level requirements
Each spell SHALL have a minimum spell slot level required to cast it. Level 1 spells: Magic Missile, Shield, Sleep, Cure Wounds, Bless, Protection from Evil. Level 2 spells: Detect Magic, Knock, Turn Undead. Level 3 spells: Lightning Bolt, Fireball, Heal, Flame Strike.

#### Scenario: Insufficient spell level
- **WHEN** a level 1 Wizard (only level-1 slots) attempts to cast Fireball (level 3)
- **THEN** the action is rejected — no level-3 slot available
