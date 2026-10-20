# Commands

Creating Space adds one command, `/creatingspace`. Every sub-command needs **operator permission level 2** (the same level as `/give`). `addAllDesigns` and `clearAllDesigns` act on the player who runs them, so they cannot be run from the server console.

| Command | What it does |
|---|---|
| `/creatingspace addAllDesigns` | Unlocks every power pack and exhaust pack design for you, as if you had read all the [Design Blueprints](Blueprints-and-Designs.md). Shows "All designs added!". |
| `/creatingspace clearAllDesigns` | Wipes your unlocked designs and puts you back to the two starting ones (Open Cycle and Bell Nozzle). Shows "All designs cleared!". |
| `/creatingspace dumpGravityList` | Prints every world in the travel network with the gravity the server is using for it, for example `The Moon : 1.6 m/s²`. Useful for checking that a datapack change took effect. |

Notes:

- `addAllDesigns` unlocks everything that exists in the data, including the **Catalyse Cycle** power pack, which currently has no assembly recipe (see [Known Issues](Known-Issues-and-Unfinished-Features.md)).
- Designs are per player. Running these commands only changes your own list.
- There is no command to teleport to other worlds. To travel, build a rocket, or use Minecraft's `/execute in <dimension> run tp ...`; the dimension ids are in [Datapack and Modpack Guide](Datapack-and-Modpack-Guide.md#dimension-ids).
