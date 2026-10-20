# Engine Crafting

You have a valid design and an **Engine Blueprint** from the [Rocket Engineer Table](Rocket-Engines.md). This page shows how to turn it into a **Rocket Engine**.

The blueprint is the *starting item of every assembly recipe*. It carries your design (material, nozzle, power pack) inside it, and each recipe only accepts a blueprint whose design matches. Every intermediate part is therefore built **from a blueprint of the same design**, and the finished parts carry the design forward, so the final engine knows what it is.

> [!IMPORTANT]
> Each assembly recipe consumes the blueprint it starts from. Build a blueprint *copy* for every recipe in the tree. Copying costs only paper; see [Copying blueprints](#copying-blueprints).

## Assembly tree

Read this top to bottom; each line is a separate Create **Sequenced Assembly** recipe (you can look each one up in JEI or Create's recipe viewer).

```
Rocket Engine
  starts from: Engine Blueprint
  deploy: Power Pack
  deploy: Exhaust Pack

Power Pack            (one blueprint)
  Open Cycle:                 deploy 1 Turbine, then 1 Injector Grid
  Ox Rich / Fuel Rich / Full Flow:  deploy 2 Turbines, then 1 Injector Grid

Exhaust Pack          (one blueprint)
  deploy: Combustion Chamber
  deploy: Bell Nozzle      (or: Aerospike Plug, for the Aerospike)

Turbine               (one blueprint, the 2-step sequence runs twice)
  deploy: Turbine Shaft, deploy: Blisk,   then again: Turbine Shaft, Blisk

Injector Grid         (one blueprint, runs twice)
  deploy: Injector, deploy: Engine Wall, deploy: Injector,   then again

Combustion Chamber    (one blueprint)
  deploy: Engine Wall, Rib, Engine Wall, Rib

Bell Nozzle           (one blueprint)
  deploy: Rib, Engine Wall, Engine Wall, Engine Wall, Rib

Aerospike Plug        (one blueprint)
  deploy: Create Shaft, Engine Wall, Engine Wall, Engine Wall, Rib
```

All of these use *deployers*: set up the starting item on a belt or depot with a deployer in front of each item in the order above, exactly like any Create sequenced assembly. "Runs twice" means the recipe loops over its sequence twice.

### The raw parts

Every part is made from **one material** (the level you chose). `M` below stands for the material name; for Brass use brass items, for Hastelloy use Hastelloy items, and so on.

| Part | How it is made |
|---|---|
| **Engine Wall** | Cut one sheet of `M` in a Create Mechanical Saw. (Andesite: cut an Andesite Alloy.) |
| **Rib** | Crafting table: top row nugget, ingot, nugget; middle row a single nugget in the centre (`N I N / . N .`). That is 3 nuggets + 1 ingot of `M`. (Andesite: 3 Andesite Alloy + 1 iron nugget.) |
| **Turbine Shaft** | Crafting table: 3 ingots of `M` in a diagonal. (Andesite: 3 Andesite Alloy.) |
| **Blisk** | Crafting table: `N P N / P I P / N P N` with N = nugget, P = sheet, I = ingot of `M`. (Andesite: Andesite Alloy in the corners, iron nuggets on the edges, a Create Shaft in the middle.) |
| **Injector** | Sequenced assembly starting from a Create **Sturdy Sheet**; deploy one sheet of `M`, then one nugget of `M`. (Andesite: deploy Andesite Alloy then an iron nugget.) |

Where `M` is iron, copper or brass the sheets and nuggets are Create's own (`create:iron_sheet`, `create:copper_nugget`, `create:brass_sheet`, and so on, plus vanilla iron nuggets). For the nickel alloys and Hastelloy they are the mod's own sheets and nuggets; see [Resources and Materials](Resources-and-Materials.md).

## How much does one engine cost?

Totals for one complete engine, **in units of the material `M`**:

| Engine | Blueprints needed | Sheets | Ingots | Nuggets | Create Sturdy Sheets | Other |
|---|---|---|---|---|---|---|
| Open Cycle + Bell Nozzle | 7 | 19 | 12 | 24 | 4 | n/a |
| Open Cycle + Aerospike | 7 | 19 | 11 | 21 | 4 | 1 Create Shaft |
| Staged cycle + Bell Nozzle | 8 | 27 | 20 | 32 | 4 | n/a |
| Staged cycle + Aerospike | 8 | 27 | 19 | 29 | 4 | 1 Create Shaft |

(One sheet or ingot is 1 ingot's worth of metal; 9 nuggets are 1 ingot's worth. An Open Cycle + Bell engine is therefore about 34 ingots of metal.)

How the table adds up for the Open Cycle + Bell Nozzle engine (one turbine, one injector grid, a chamber and a nozzle):

- Engine Walls: 2 (injector grid) + 2 (chamber) + 3 (nozzle) = **7**
- Ribs: 2 (chamber) + 2 (nozzle) = **4**
- Turbine: 2 shafts and 2 blisks
- Injectors: 2 per loop × 2 loops = **4**
- Blueprints: engine + power pack + turbine + injector grid + exhaust pack + chamber + nozzle = **7**

## Copying blueprints

Blueprints are only produced by the Engineer Table, so copy them. This is a sequenced assembly recipe that starts from one Engine Blueprint, deploys **paper** twice and gives you **2 Engine Blueprints** with the design intact. Each run therefore nets +1 blueprint for 2 paper. For the 7 blueprints of an Open Cycle + Bell engine, run it 6 times (12 paper).

## Step-by-step example: your first engine (Brass, Open Cycle, Bell Nozzle)

1. At the Engineer Table pick Open Cycle, Bell Nozzle, Metha/LOX, **thrust 100 000 N, size 1 000 mB, expansion ratio 50, material Brass**. The readout shows about 30 bar against a limit of about 36 bar. Press confirm and take the blueprint.
2. Copy the blueprint until you hold 7.
3. Prepare the parts from brass: 7 walls (saw 7 brass sheets), 4 ribs, 2 turbine shafts, 2 blisks, 4 injectors (4 Sturdy Sheets + 4 brass sheets + 4 brass nuggets).
4. Assemble with a blueprint each: a Turbine (shaft, blisk, shaft, blisk), an Injector Grid (injector, wall, injector, ×2), a Power Pack (turbine, grid), a Combustion Chamber (wall, rib, wall, rib), a Bell Nozzle (rib, wall, wall, wall, rib), an Exhaust Pack (chamber, nozzle).
5. With the last blueprint: deploy the Power Pack and the Exhaust Pack to get the **Rocket Engine**. Its tooltip should show ISP 289 s, mass 3 020 kg and thrust 100 000 N.

That engine can lift about 10 tonnes in Earth gravity; see [Rocket Science Reference](Rocket-Science-Reference.md) for what that means for the rest of your rocket.

## Recycling

There is no recycling recipe for engine parts, the blueprint copying consumes paper only, and the parts cannot be disassembled again. Plan your first design carefully, but remember that designing and copying blueprints costs nothing but paper.
