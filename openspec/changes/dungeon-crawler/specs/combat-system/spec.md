## ADDED Requirements

### Requirement: Initiative
At the start of combat, each combatant SHALL roll d20 + DEX modifier for initiative. Higher initiative acts first. Ties are resolved in favor of the player.

#### Scenario: Initiative order
- **WHEN** the player (DEX 14, mod +2) enters combat with a Goblin (DEX 14, mod +2)
- **THEN** both roll d20+2, and the higher roll acts first; on a tie the player acts first

### Requirement: Attack rolls
An attack SHALL be resolved by rolling d20 + ability modifier + proficiency bonus. If the total equals or exceeds the target's AC, the attack hits. A natural 20 always hits (critical). A natural 1 always misses.

#### Scenario: Melee attack hit
- **WHEN** a Fighter (STR mod +3, proficiency +2) attacks an Orc (AC 13) and rolls d20 → 9
- **THEN** total is 9+3+2=14 ≥ 13, the attack hits

#### Scenario: Critical hit
- **WHEN** the player rolls a natural 20 on an attack roll
- **THEN** the attack hits regardless of AC, and damage dice are doubled (roll weapon die twice + modifier)

#### Scenario: Critical miss
- **WHEN** the player rolls a natural 1 on an attack roll
- **THEN** the attack misses regardless of target AC

### Requirement: Damage calculation
On a hit, damage SHALL be calculated as weapon damage die + ability modifier. Melee weapons use STR modifier, finesse weapons use the higher of STR or DEX, ranged uses DEX.

#### Scenario: Longsword damage
- **WHEN** a hit is scored with a longsword (d8) by a character with STR mod +3
- **THEN** damage is d8 roll + 3

### Requirement: Saving throws
When a creature must resist an effect (spell, trap, monster ability), it SHALL roll d20 + relevant ability modifier. If the total equals or exceeds the DC, the save succeeds and the effect is reduced or negated.

#### Scenario: Poison save
- **WHEN** a Giant Spider hits and the player must make a CON save (DC 12) with CON mod +2
- **THEN** player rolls d20+2; on 10+ (total 12+) the poison is resisted, otherwise the player is poisoned

### Requirement: Conditions
The combat system SHALL support conditions: poisoned (-2 to attacks), stunned (skip turn), paralyzed (auto-crit on hit, skip turn), frightened (-2 to attacks, cannot move toward source), slowed (no movement action), blinded (-4 to attacks, enemies have advantage). Each condition SHALL have a duration in turns and be removable by rest or specific spells.

#### Scenario: Stunned condition
- **WHEN** a creature is stunned for 1 turn
- **THEN** it skips its next action, and the condition is removed at the end of that turn

### Requirement: Death
When a creature's HP reaches 0, it dies and is removed from the combat. The player character dies when HP reaches 0 (no death saves — this is a dungeon crawler, death is death).

#### Scenario: Monster death
- **WHEN** a Goblin's HP is reduced to 0 or below
- **THEN** the Goblin is removed from the floor, drops its loot, and combat ends if no enemies remain

### Requirement: Armor Class calculation
AC SHALL be calculated as base armor AC + DEX modifier (up to armor's max DEX) + shield bonus. Unarmored AC is 10 + DEX modifier.

#### Scenario: Chain mail and shield
- **WHEN** a character wears chain mail (AC 16, max DEX +0) and carries a shield (+2)
- **THEN** the character's AC is 18

### Requirement: Leveling and proficiency
Proficiency bonus SHALL scale with level: +2 at levels 1-4, +3 at levels 5-8, +4 at levels 9-10. XP thresholds for leveling SHALL follow a simplified progression. On level up, the player gains HP (class hit die + CON mod) and may gain new class abilities.

#### Scenario: Level up
- **WHEN** a Fighter with 300 XP gains 100 XP (threshold for level 2 is 300)
- **THEN** the character advances to level 2, gains d10 + CON mod HP, and proficiency remains +2
