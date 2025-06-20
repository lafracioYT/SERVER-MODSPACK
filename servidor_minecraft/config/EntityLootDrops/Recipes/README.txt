Custom Recipes Configuration Guide
===============================

This system allows you to create custom crafting recipes with NBT data support.

Directory Structure:
-------------------
config/EntityLootDrops/Recipes/
  ??? Shaped/               # Shaped crafting recipes
  ??? Shapeless/            # Shapeless crafting recipes

Recipe Format:
------------
Recipes use JSON format with these properties:

Common Properties:
- name: Unique name for the recipe (used for recipe ID)
- type: Either "shaped" or "shapeless"
- outputItem: The Minecraft item ID for the output (e.g., "minecraft:diamond_sword")
- outputCount: Number of items to output (default: 1)
- outputNbt: Optional NBT data for the output item
- group: Optional recipe group for the recipe book

Shaped Recipe Properties:
- pattern: Array of strings representing the crafting grid pattern
- key: Mapping of pattern characters to item IDs

Shapeless Recipe Properties:
- ingredients: Array of item IDs for the ingredients

Example Shaped Recipe:
```json
{
  "name": "diamond_helmet_with_enchants",
  "type": "shaped",
  "outputItem": "minecraft:diamond_helmet",
  "outputCount": 1,
  "outputNbt": "{display:{Name:'{\"text\":\"Enchanted Helmet\",\"color\":\"aqua\"}'},Enchantments:[{id:\"minecraft:protection\",lvl:4},{id:\"minecraft:unbreaking\",lvl:3}]}",
  "pattern": [
    "XXX",
    "X X"
  ],
  "key": {
    "X": "minecraft:diamond"
  },
  "group": "helmets"
}
```

Example Shapeless Recipe:
```json
{
  "name": "golden_apple_from_gold_blocks",
  "type": "shapeless",
  "outputItem": "minecraft:golden_apple",
  "outputCount": 1,
  "ingredients": [
    "minecraft:gold_block",
    "minecraft:gold_block",
    "minecraft:apple"
  ]
}
```

Commands:
--------
/recipes reload - Reload recipe configuration
