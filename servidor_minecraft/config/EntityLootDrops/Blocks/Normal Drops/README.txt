Normal Drops Configuration
========================

Configuration Format:
-------------------
Block drops use JSON format with these properties:

Basic Properties:
- blockId: The Minecraft block ID (e.g., "minecraft:stone") - only for block-specific drops
- itemId: The item to drop (e.g., "minecraft:diamond")
- dropChance: Percentage chance to drop (0-100)
- minAmount: Minimum amount to drop
- maxAmount: Maximum amount to drop
- requirePlayerBreak: If true, only drops when broken by a player
- allowDefaultDrops: If true, keeps vanilla drops

Tool Requirements:
- requiredTool: Specific tool required (e.g., "minecraft:diamond_pickaxe")
- requiredToolTier: Required tool tier (e.g., "diamond")
- requiredToolLevel: Required tool level (e.g., 3 for diamond)
- requiredEnchantment: Required enchantment (e.g., "minecraft:fortune")
- requiredEnchantLevel: Required enchantment level

Advanced Features:
- nbtData: Custom NBT data for the dropped item
- command: Command to execute when the block breaks
- commandChance: Percentage chance to execute the command
- allowModIDs: List of mod IDs allowed to drop items when allowDefaultDrops is false
