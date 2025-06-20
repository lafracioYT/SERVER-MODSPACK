Block Drops Configuration Guide
============================

This system allows you to configure custom drops when blocks are broken.

Directory Structure:
-------------------
config/EntityLootDrops/Blocks/
  ??? Normal Drops/           # Always active drops
  ?   ??? Global_Block_Drops.json  # Drops for all blocks
  ?   ??? Block Types/        # Block-specific drops
  ??? Event Drops/            # Event-specific drops
      ??? Winter/             # Winter event drops
      ??? Summer/             # Summer event drops
      ??? Easter/             # Easter event drops
      ??? Halloween/          # Halloween event drops
      ??? [Custom Event]/     # Your custom events

For detailed configuration instructions, see the README files in each directory.

Commands:
--------
/blockdrops event <eventName> <true|false> - Toggle a block event
/blockdrops event dropchance <true|false> - Toggle double drop chance
/blockdrops event doubledrops <true|false> - Toggle double drops
/blockdrops active_events - List active block events
/blockdrops listall - List all available block events
/blockdrops reload - Reload block configuration
