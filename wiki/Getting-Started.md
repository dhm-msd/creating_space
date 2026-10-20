# Getting Started

A walkthrough from a fresh Create world to your first trip into orbit. You do not have to follow it strictly; it just shows the order in which the pieces depend on each other. Every step links to the page with the details.

> [!NOTE]
> Creating Space builds on Create's own progression. You should already have brass, the Mechanical Press, Mechanical Mixer, Blaze Burners, Fluid Tanks and Pipes, Sturdy Sheets and the train-control components. The Rocket Controls block is crafted from Create's electron tubes, redstone link, controls block and sturdy sheets.

## The big picture

```
 NICKEL ─────────► nickel plates ─► backtank, oxygen sealer, cryogenic tank
 BRASS/COPPER/IRON ► engine parts ─► ROCKET ENGINE ─┐
 WATER ► electrolysis ► hydrogen + oxygen            │
 AIR ► air liquefier ► liquid oxygen + CO₂ ─► methane ┴► ROCKET ──► ORBIT ──► MOON / MARS / VENUS
```

## Step 1: Find nickel

Nickel is the first new metal you need. **Nickel Ore** generates in the Overworld, in stone and in deepslate, anywhere between Y −64 and 120 (most often around the middle). You need an iron pickaxe.

Smelt it, or crush it and wash it (see [Resources and Materials](Resources-and-Materials.md)). Press nickel ingots into **nickel plates** in the Mechanical Press. You will use them for the oxygen backtank, the oxygen sealer and the cryogenic tank.

## Step 2: Build a Rocket Engineer Table and design your first engine

Craft a [Rocket Engineer Table](Machines.md#rocket-engineer-table) (six wooden slabs and a smooth stone) and open it. You start with the **Open Cycle** power pack and the **Bell Nozzle**, burning **Metha/LOX**.

A good first design is the one in [Engine Crafting](Engine-Crafting.md#step-by-step-example-your-first-engine-brass-open-cycle-bell-nozzle): 100 kN thrust, 1 000 mB chamber, expansion ratio 50, **Brass**. Press the check mark to get an **Engine Blueprint**. See [Rocket Engines](Rocket-Engines.md).

> [!TIP]
> Cheaper metals are possible with a bigger chamber, but a bigger chamber is a heavier engine, and heavy engines need more thrust. The design pages explain the trade-off.

## Step 3: Make the engine

Copy the blueprint with paper, then run the sequenced-assembly chain of walls, ribs, turbine and injectors to produce a **Rocket Engine**. The full bill of materials is on [Engine Crafting](Engine-Crafting.md): for an Open Cycle + Bell engine that is about 34 ingots' worth of the material, plus 4 Create Sturdy Sheets.

## Step 4: Make propellant

Metha/LOX needs equal volumes of Liquid Oxygen and Liquid Methane.

- **Liquid Oxygen:** an [Air Liquefier](Machines.md#air-liquefier) facing open air in the Overworld, powered by a rotating shaft. (Or an electrolyzer: it makes oxygen too.)
- **Liquid Methane:** needs Liquid CO₂ and Liquid Hydrogen.
  - CO₂: an Air Liquefier facing a **campfire**.
  - Hydrogen: a [Mechanical Electrolyzer](Machines.md#mechanical-electrolyzer) on water.
  - Combine in a [Catalyst Carrier](Machines.md#catalyst-carrier) over a **heated** basin with the catalyst slot empty.

Store them in separate **Create Fluid Tanks**. See [Fluids and Propellants](Fluids-and-Propellants.md).

## Step 5: Make a spacesuit

Space has no air. Make the **Basic Spacesuit** (fabric from copper sheets, gold nuggets and red wool; helmet, leggings, boots; and an oxygen backtank). Fill the backtank with Liquid Oxygen. See [Spacesuit and Oxygen Backtank](Spacesuit-and-Oxygen-Backtank.md) and [Life Support](Life-Support.md).

## Step 6: Build the rocket

Controls, engine, two fluid tanks (one per propellant), a seat, all glued together, with clear sky above. Check the [weight and thrust](Rocket-Science-Reference.md#worked-example): your thrust must beat the weight, and your Δv must beat the trip. See [Building a Rocket](Building-a-Rocket.md).

## Step 7: Fly

Right-click the Rocket Controls, press **Create New Rocket**, board, right-click the Controls again, add a **Destination: Earth Orbit** entry (1 500 m/s), click the **pause** button off, and close the screen. See [Launching and Flight](Launching-and-Flight.md).

## Step 8: Build a station, then go further

In Earth Orbit, press **Disassemble**, and build outward with an [Oxygen Sealer](Oxygen-Sealer.md) so you can work without a suit. From orbit:

| Next goal | Cost from Earth Orbit | Why go |
|---|---|---|
| The Moon (via Moon Orbit) | 900 m/s | Aluminium, cobalt and a lot of nickel; crashed rockets with better engine designs |
| Mars | 1 300 m/s | Nickel sulfate geodes for the catalyst; a buried outpost |
| Venus | 2 200 m/s | The hardest world: heat, fire, lava |

The Moon's wrecks hold the designs for the **Full Flow**, **Ox/Fuel Rich** power packs and the **Aerospike** nozzle. See [Blueprints and Designs](Blueprints-and-Designs.md), [Structures and Loot](Structures-and-Loot.md) and [Planets and Travel](Planets-and-Travel.md).

## Where to go next

- Read about all five alloys and the material ladder: [Resources and Materials](Resources-and-Materials.md).
- Work out better engines: [Engine Design Reference](Engine-Design-Reference.md).
- Stuck? [Troubleshooting and FAQ](Troubleshooting-and-FAQ.md).
