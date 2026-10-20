# Known Issues and Unfinished Features

Creating Space is under active development. This page lists things in **version 1.7.23** that look unfinished or inconsistent, so you don't waste time hunting for them. If a later version fixes any of these, this page will be out of date; see [the folder README](README.md) for how to check.

## Content that exists but cannot be obtained or used yet

| What | Details |
|---|---|
| **Catalyse Cycle power pack** | You can unlock the design from the Mars outpost and pick it on the Engineer Table, but the data has **no assembly recipe** for its power pack. So there is no way to craft an engine that burns *Premixed methalox* (monopropellant) yet. |
| **Metallic hydrogen** | A propellant type is defined (6 000 s ISP) but no power pack or nozzle lists it as allowed. A "magnetic cycle" power pack sits in an unused data folder. |
| **Ox Rich Flow and Fuel Rich Flow** | They currently have identical numbers. They differ in name only. |
| **Redstone Link wait condition** | The schedule has a "Redstone Link" condition name in its code and language file, but it is switched off and cannot be selected. |
| **Sturdy Propeller, Space Food** | Both items exist (the propeller is craftable, the food is not), but nothing in the mod uses them. |
| **Small / Big Rocket Engine** | Legacy fixed-stat engines with no recipe. |

## Rough edges

- **Material names on the Engineer Table** may show as raw keys (`creatingspace.material.copper`) because the language file has no entries for them. The order is Andesite, Iron, Copper, Brass, Reinforced Copper, Copronickel, Monel, Inconel, Hastelloy.
- **The nozzle block of a designed Rocket Engine weighs 1 000 kg** by default, because the mass table lists it under a different name (`super_engine_structure`) from the block's real id (`engine_structure`). Every designed engine therefore weighs its listed mass **plus a tonne**. See [Building a Rocket](Building-a-Rocket.md#mass-what-your-rocket-weighs). You can fix this with a datapack that edits `blocks_mass.json`.
- **Two mass-table entries use legacy tags** (`#forge:stone`, `#forge:ores`) that may not match anything in NeoForge 1.21.
- **A rocket that fails its pre-flight check may stay "in transit"** until you re-send the schedule. Open the rocket screen and close it again after you have fixed the cause.
- **Sealed rooms and non-full blocks**: partial blocks (stairs especially) may not seal reliably; see [Oxygen Sealer](Oxygen-Sealer.md#how-the-room-is-worked-out).
- **Leaf oxygen** is only registered for leaves that the room scan runs into at the edges of its boxes, so the number of oxygen-producing leaves is not simply the number of leaf blocks.
- **Air liquefying** works only in the Overworld.
- **The two mod advancements** ("Not enough… space down there" for reaching Earth orbit, and "Where is the cheese?" for reaching the Moon) are stored in a data folder called `advancements`. Minecraft 1.21 reads `advancement` (singular), so they may not be loading.
- **Structure loot**: the Crashed Ship has no loot, and the Abandoned Outpost's loot table does not appear to be attached to a container. See [Structures and Loot](Structures-and-Loot.md).
- **Ponder scenes** exist only for the rocket (controls, engines, flight recorder). Machines such as the electrolyzer and Catalyst Carrier have no Ponder yet. Ponder text for the old Chemical Synthesizer (coal dust, 320 kg every 4 seconds) is obsolete.
- **Few creatures.** Only skeletons spawn naturally (on the Moon). Mars and Venus have no native mobs.

## Roadmap (from the developer's notes)

The repository's technical document (`documentation/main.tex`, dated May 2026) lists plans and ideas. **None of these are in the game now.** They may change or be dropped.

- A better rocket menu with a rocket analysis panel (mass, Δv, thrust-to-weight, fuel, reentry heating) and a manual destination picker.
- Orbital manoeuvring, docking beacons, relative-velocity matching and a spaceflight HUD.
- A node-based engine designer instead of the table, pre-made engine blueprints as loot, engine models that change with the design, and recycling of engine parts.
- Spacesuit upgrades: armour upgrade slot, a jetpack slot, magnetic boots, easier refilling.
- More detailed air: several gases (oxygen, CO₂), air recycling, visible leaks.
- Planet atmospheres that affect fog and visibility; orbit-based day/night.
- More terrain, structures and mobs on Mars, Venus and the Moon; an Asteroid Belt and Europa (neither exists as a destination in this version's data); lore.
