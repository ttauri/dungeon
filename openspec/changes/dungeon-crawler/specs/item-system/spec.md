## ADDED Requirements

### Requirement: Item categories
The game SHALL support the following item categories: weapons (melee, ranged), armor (light, medium, heavy), shields, potions, scrolls, keys, gold, and quest items.

#### Scenario: Item identification
- **WHEN** the player picks up an item
- **THEN** the item is added to inventory with its category, name, and properties visible

### Requirement: Weapon types
The game SHALL include weapons: Dagger (d4, finesse), Short Sword (d6, finesse), Longsword (d8), Greataxe (d12, two-handed), Mace (d6), Staff (d6, two-handed), Shortbow (d6, ranged), and magical variants (+1, +2) for each. Magical weapons add their bonus to both attack and damage rolls.

#### Scenario: Magical weapon bonus
- **WHEN** a character attacks with a Longsword +1
- **THEN** the attack roll gains +1 and the damage roll gains +1 in addition to ability modifier and proficiency

### Requirement: Armor types
The game SHALL include armors: Leather (AC 11 + DEX), Studded Leather (AC 12 + DEX), Chain Shirt (AC 13 + DEX max 2), Chain Mail (AC 16, no DEX), Plate (AC 18, no DEX). Magical armor variants (+1, +2) add their bonus to the base AC.

#### Scenario: Armor class restriction
- **WHEN** a Wizard (no armor proficiency) equips Chain Mail
- **THEN** the armor provides AC but the character has disadvantage on all attack rolls (can't use armor they're not proficient with)

### Requirement: Potions
The game SHALL include: Healing Potion (heal 2d4+2), Greater Healing (heal 4d4+4), Antidote (cure poison), Potion of Strength (+2 STR for 20 turns), Potion of Speed (extra action for 3 turns), Potion of Invisibility (invisible for 10 turns or until attack). Using a potion costs one turn action.

#### Scenario: Healing potion use
- **WHEN** the player uses a Healing Potion at 20/40 HP
- **THEN** they heal 2d4+2 HP (up to max 40) and the potion is removed from inventory

### Requirement: Scrolls
The game SHALL include scrolls that allow any class to cast a spell once: Scroll of Fireball, Scroll of Lightning Bolt, Scroll of Heal, Scroll of Detect Magic, Scroll of Knock. Using a scroll costs one turn action and consumes the scroll.

#### Scenario: Non-caster using scroll
- **WHEN** a Fighter uses a Scroll of Fireball
- **THEN** the Fireball spell is cast using DC 13 (fixed scroll DC), and the scroll is consumed

### Requirement: Loot tables
Loot SHALL be determined by tier-specific loot tables. Each tier has weighted drop tables for chest contents and monster drops. Higher tiers include better base items and higher chance of magical items. Gold amounts scale with depth.

#### Scenario: Tier 1 chest loot
- **WHEN** a chest on floor 2 is opened
- **THEN** contents are drawn from Tier 1 table: common weapons, basic potions, 5-20 gold, low chance of magical item

#### Scenario: Tier 3 monster drop
- **WHEN** a Minotaur is killed on floor 8
- **THEN** it drops from Tier 3 table: chance of magical weapon/armor, greater potions, 30-80 gold

### Requirement: Equipment durability (Rust Monster interaction)
Metal equipment (weapons, heavy armor, shields) SHALL be destructible by Rust Monster attacks. When a Rust Monster hits, the player makes a DEX save; on failure, one random metal equipment piece loses a durability tier (normal → worn → broken → destroyed).

#### Scenario: Rust Monster destroys armor
- **WHEN** a Rust Monster hits and the player fails the DEX save, and their Chain Mail is already "worn"
- **THEN** Chain Mail degrades to "broken" (AC reduced by 2) and a log message warns the player
