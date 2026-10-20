# Blueprints and Designs

Two different things are called "blueprint" in Creating Space. Do not mix them up:

| Item | What it is | Where it comes from |
|---|---|---|
| **Design Blueprint** (a sheet of paper) | Teaches you a **power pack or exhaust pack design**, so it shows up on the Rocket Engineer Table. | Loot in [structures](Structures-and-Loot.md), or the `/creatingspace addAllDesigns` command. |
| **Engine Blueprint** | The finished plan for **one specific engine**, produced by the table and used as the starting item of [engine assembly](Engine-Crafting.md). | The Rocket Engineer Table. |

## Unlocking designs

A **Design Blueprint** carries one design (for example "Aerospike, exhaust pack"). **Right-click it** to learn that design. A message above your hotbar confirms what you unlocked. The paper is **not used up**, so you can keep it, or give it to a friend.

- Unlocks are **per player**. Each player in a world has their own list, stored with the world's save data.
- Every player starts with the **Open Cycle** power pack and the **Bell Nozzle** exhaust pack. If a player's list is ever empty (for example, a brand-new player), those two are added when they log in.
- Propellants are not unlocked; they are available as soon as a power pack supports them.

### What can be unlocked

| Design | Type | How |
|---|---|---|
| Open Cycle | Power pack | Known from the start |
| Bell Nozzle | Exhaust pack | Known from the start |
| Ox Rich Flow | Power pack | Design Blueprint in the **Crashed Rocket** structure on the Moon (random pick of four) |
| Fuel Rich Flow | Power pack | same |
| Full Flow | Power pack | same |
| Aerospike | Exhaust pack | same |
| Catalyse Cycle | Power pack | Design Blueprint in the underground outpost on **Mars** (always this one) |

See [Structures and Loot](Structures-and-Loot.md) for where those structures generate.

> [!NOTE]
> The Catalyse Cycle can be unlocked, and chosen on the table, but the data currently has no assembly recipe for its power pack. See [Known Issues](Known-Issues-and-Unfinished-Features.md).

### Designs for server owners and creative players

Operators (permission level 2) can unlock or reset all designs for themselves:

- `/creatingspace addAllDesigns` unlocks every power pack and exhaust pack that exists in the data.
- `/creatingspace clearAllDesigns` resets your list back to the two starting designs.

See [Commands](Commands.md).

## Engine Blueprints

An **Engine Blueprint** is created by pressing the confirm button on the [Rocket Engineer Table](Rocket-Engines.md). It stores:

- the nozzle, power pack and propellant,
- the chamber size, expansion ratio and material level,
- the engine's ISP, mass and thrust.

You can **copy** it with paper (see [Engine Crafting](Engine-Crafting.md#copying-blueprints)). Its tooltip describes it as the plan used to craft rocket engines and their components.
