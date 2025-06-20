Entity Loot Drops - Configuration Guide
=====================================

This mod allows you to customize what items drop from mobs, with powerful features like conditional drops, commands, and special effects.

Quick Start:
-----------
1. All configuration is done through JSON files
2. Files are organized in folders for normal drops and event drops
3. Use /lootdrops commands to control events in-game

1. Directory Structure
----------------------
config/entitylootdrops/
|-- Normal Drops/            # Regular drops (always active)
|   |-- Global_Hostile_Drops.json   # Drops for all hostile mobs
|   `-- Mobs/                # Entity-specific drops
|       |-- zombie_drops.json
|       |-- skeleton_drops.json
|-- Event Drops/             # Event-specific drops
    |-- Winter/              # Winter event drops
    |   |-- Global_Hostile_Drops.json
    |   `-- Mobs/
    |-- Summer/              # Summer event drops
    |-- Easter/              # Easter event drops
    |-- Halloween/           # Halloween event drops
    `-- [custom event]/      # Custom event drops

2. Drop Configuration Format
-------------------------
All drop configurations use JSON format with these properties:

Basic Properties:
- "_comment": Comment for documentation
- itemId: The Minecraft item ID (e.g., "minecraft:diamond")
- dropChance: Percentage chance to drop (0-100)
- minAmount: Minimum number of items to drop
- maxAmount: Maximum number of items to drop
- requirePlayerKill: If true, only drops when killed by a player
- allowDefaultDrops: If false, disables vanilla drops
- allowModIDs: List of mod IDs allowed to drop items when allowDefaultDrops is false

Advanced Properties:
- nbtData: Custom NBT data for the item (enchantments, names, etc.)
- command: Command to execute when the mob dies
- commandChance: Percentage chance for the command to execute
- requiredAdvancement: Player must have this advancement
- requiredEffect: Player must have this potion effect
- requiredEquipment: Player must have this item equipped
- requiredDimension: Player must be in this dimension

3. Comprehensive Examples
----------------------

A. Basic Hostile Drop:
```json
{
  "_comment": "Simple diamond drop with 5% chance",
  "itemId": "minecraft:diamond",
  "dropChance": 5.0,
  "minAmount": 1,
  "maxAmount": 2,
  "requirePlayerKill": true
}
```

B. Advanced Item Drop with NBT:
```json
{
  "_comment": "Named sword with enchantments",
  "itemId": "minecraft:diamond_sword",
  "dropChance": 10.0,
  "minAmount": 1,
  "maxAmount": 1,
  "nbtData": "{display:{Name:'{\"text\":\"Legendary Blade\",\"color\":\"gold\"}',Lore:['{\"text\":\"Ancient power flows through this weapon\",\"color\":\"purple\"}']},Enchantments:[{id:\"minecraft:sharpness\",lvl:5},{id:\"minecraft:looting\",lvl:3}]}"
}
```

C. Conditional Drop with Command:
```json
{
  "_comment": "Special drop for advanced players",
  "itemId": "minecraft:netherite_ingot",
  "dropChance": 15.0,
  "minAmount": 1,
  "maxAmount": 1,
  "requiredAdvancement": "minecraft:story/enter_the_nether",
  "requiredEquipment": "minecraft:diamond_sword",
  "command": "title {player} title {\"text\":\"Legendary Find!\",\"color\":\"gold\"}",
  "commandChance": 100.0
}
```

D. Entity-Specific Drop (for Mobs folder):
```json
{
  "_comment": "Special zombie drop",
  "entityId": "minecraft:zombie",
  "itemId": "minecraft:rotten_flesh",
  "dropChance": 50.0,
  "minAmount": 2,
  "maxAmount": 5,
  "nbtData": "{display:{Name:'{\"text\":\"Purified Flesh\",\"color\":\"green\"}'}}"
}
```

E. Disabling Vanilla Drops:
```json
{
  "_comment": "Replace vanilla drops with custom ones",
  "itemId": "minecraft:emerald",
  "dropChance": 100.0,
  "minAmount": 1,
  "maxAmount": 3,
  "requirePlayerKill": true,
  "allowDefaultDrops": false,
  "allowModIDs": ["examplemod", "anothermod"]
}
```

F. Complete Example with All Options:
```json
{
  "_comment": "Example showing all available options",
  "entityId": "minecraft:zombie",
  "itemId": "minecraft:diamond_sword",
  "dropChance": 10.0,
  "minAmount": 1,
  "maxAmount": 3,
  "nbtData": "{display:{Name:'{\"text\":\"Ultimate Sword\",\"color\":\"gold\"}',Lore:['{\"text\":\"A powerful weapon\",\"color\":\"purple\"}']},Enchantments:[{id:\"minecraft:sharpness\",lvl:5},{id:\"minecraft:looting\",lvl:3}]}",
  "requiredAdvancement": "minecraft:story/enter_the_nether",
  "requiredEffect": "minecraft:strength",
  "requiredEquipment": "minecraft:diamond_pickaxe",
  "requiredDimension": "minecraft:overworld",
  "command": "title {player} title {\"text\":\"Epic Kill!\",\"color\":\"gold\"}\nparticle minecraft:heart {entity_x} {entity_y} {entity_z} 1 1 1 0.1 20",
  "commandChance": 100.0,
  "requirePlayerKill": true,
  "allowDefaultDrops": true,
  "allowModIDs": ["examplemod"]
}
```

4. Command Placeholders
--------------------
Use these in your commands to reference specific values:

Player Related:
- {player}    : Player's name
- {player_x}  : Player's X coordinate
- {player_y}  : Player's Y coordinate
- {player_z}  : Player's Z coordinate

Entity Related:
- {entity}    : Killed entity's name
- {entity_id} : Entity's Minecraft ID
- {entity_x}  : Entity's X coordinate
- {entity_y}  : Entity's Y coordinate
- {entity_z}  : Entity's Z coordinate

5. Command Examples
----------------
- Effect: "effect give {player} minecraft:regeneration 10 1"
- Sound: "playsound minecraft:entity.experience_orb.pickup master {player}"
- Particles: "particle minecraft:heart {entity_x} {entity_y} {entity_z} 1 1 1 0.1 20"
- Message: "title {player} actionbar {\"text\":\"Epic kill!\",\"color\":\"gold\"}"
- Lightning: "summon minecraft:lightning_bolt {entity_x} {entity_y} {entity_z}"
- Multiple commands: Use \n to separate commands

6. Player Commands
----------------
Event Management:
- /lootdrops event <eventName> true|false - Enable/disable an event
- /lootdrops event dropchance true|false - Enable/disable 2x drop chance
- /lootdrops event doubledrops true|false - Enable/disable 2x drop amounts

Information Commands:
- /lootdrops active_events - List all active events
- /lootdrops listall - List all available events
- /lootdrops openconfig - Opens custom JSON editor menu
- /lootdrops reload - Reload all configuration files
- /lootdrops debug true|false - Enable/disable debug logging

7. Events System
-------------
- Events are special drop configurations that can be toggled on/off
- Multiple events can be active simultaneously
- Event drops stack with normal drops
- Custom events can be created by adding new folders in the events directory
- The drop chance event doubles all drop chances when active
- The double drops event doubles all item drops when active

8. Tips and Best Practices
-----------------------
1. Start with small drop chances (1-5%) for valuable items
2. Use commands sparingly to avoid spam
3. Test configurations on a test server first
4. Back up your config files before making major changes
5. Use meaningful comments in your JSON files
6. Keep drop chances balanced for game progression
7. You can delete most of the default example generated files, but keep the Global_Hostile_Drops.json file

9. Common Issues
-------------
1. Invalid JSON: Check your syntax, especially with NBT data
2. Missing Quotes: All strings need double quotes
3. Wrong IDs: Verify Minecraft IDs are correct (include "minecraft:" prefix)
4. Command Errors: Test commands in-game first
5. Case Sensitivity: IDs and commands are case-sensitive
6. Custom Events: Inside your custom event folder, you MUST have at least one of these:
   - A Global_Hostile_Drops.json file for drops that apply to all hostile mobs
   - A Mobs folder with entity-specific drop files

