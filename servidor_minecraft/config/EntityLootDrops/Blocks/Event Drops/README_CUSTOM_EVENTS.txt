Custom Block Events Guide
======================

You can create your own custom block events by following these steps:

1. Create a new folder inside the 'Event Drops' directory
   Example: config/EntityLootDrops/Blocks/Event Drops/MyCustomEvent/

2. Inside your custom event folder, create:
   - A Global_Block_Drops.json file for drops that apply to all blocks
   - A Block Types/ folder with block-specific drop files

3. Use the command to activate your event:
   /blockdrops event MyCustomEvent true

4. You can toggle your event on and off at any time:
   /blockdrops event MyCustomEvent false

5. Check active events with:
   /blockdrops active_events

6. See all available events with:
   /blockdrops listall

Note: Event names are case-insensitive in commands, but the folder name will be displayed as created.
