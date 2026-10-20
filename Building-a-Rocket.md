# Building a Rocket

A Creating Space rocket is a **Create contraption**. You build it out of ordinary blocks, press one button, and the whole structure turns into a flying rocket entity. This page covers what a rocket needs and how to assemble it. Flying it is covered in [Launching and Flight](Launching-and-Flight.md).

## The minimum rocket

| Part | Why you need it |
|---|---|
| **Rocket Controls** | The brain. Assembly starts from this block, and you use it to set the destination. A rocket without it cannot be assembled. |
| **At least one [Rocket Engine](Rocket-Engines.md)** | Provides thrust. Your thrust must beat the rocket's weight. |
| **Propellant in Create Fluid Tanks** | Engines burn fluids stored in the rocket. See [Fuel tanks](#fuel-tanks). |
| **A seat** (Create Seat) | Riders sit on it; without one they can fall out. |
| **Everything glued together** | Blocks join the contraption through Create's normal attachment rules, such as Super Glue; see [How the structure is gathered](#how-the-structure-is-gathered). |

Everything else is up to you: casings for the hull ([Rocket Casing](Machines.md#rocket-casing) is a decorative option), extra seats, cargo (vaults, chests, barrels), Flight Recorders, pipes and so on.

## Step by step

1. **Pick a clear launch site.** The rocket travels straight up. Anything above it in its path will stop it (it counts as a collision). Do not build a roof over it.
2. **Build the hull** with the Rocket Controls and the engine(s). Place each [Rocket Engine](Rocket-Engines.md#the-finished-engine) with a free 1×2 vertical space for its nozzle.
3. **Add the fuel tanks** and fill them. You can fill tanks by piping fluids into them as usual before assembly.
4. **Add seats** for the crew, and a [Flight Recorder](Machines.md#flight-recorder) if you want diagnostics.
5. **Connect everything** with Create Super Glue, or other Create attachments.
6. **Right-click the Rocket Controls.** A small window opens with one button, **Create New Rocket**. Press it.
7. Next tick, all the blocks connected to the controls disappear and a **rocket entity** takes their place, with a contraption-assembly sound. If something is wrong, nothing happens and an assembly error is stored. Put on **Engineer's Goggles** and look at the Rocket Controls to read it (this is Create's standard assembly-error display).

After that, right-click the Rocket Controls *on the assembled rocket* to open its flight screen.

## How the structure is gathered

The mod uses Create's standard contraption assembly, started from the Rocket Controls block. In practice:

- Blocks stay together via **Super Glue**, **chassis** blocks and other sticky blocks, or Create's built-in attachment rules.
- **Engines and their nozzle structure** blocks are automatically treated as one piece.
- **Clamps** and other blocks tagged non-movable are never picked up. This keeps a launch pad in place.
- Create's block limit applies (default 2 048 blocks per contraption; server owners can change it).

> [!TIP]
> If assembly fails or your rocket is missing blocks, use Create's usual debugging steps: check the glue, and use the goggles' assembly message.

## Fuel tanks

Engines draw propellant straight from the rocket's mounted fluid storage. You do not need pipes between tanks and engines.

- **Use Create Fluid Tanks.** These are the only fluid containers Create can carry on a contraption (Create supports its own Fluid Tank and Creative Fluid Tank here). The mod's **Cryogenic Tank** does not register as mounted storage, so it does not count as propellant storage.
- A Create fluid tank holds one kind of fluid at a time, so you need a tank for each propellant. A Metha/LOX rocket needs a methane tank and an oxygen tank.
- Each Create fluid tank block holds 8 buckets (8 000 mB) by default, and tanks of several blocks merge into one larger container.
- The fluids must be the mod's propellant fluids (they are recognised by fluid tag; see [Fluids and Propellants](Fluids-and-Propellants.md)).
- Any other fluid in the tanks (for example water) is carried as dead weight.

### How much of each propellant?

Engines burn their propellants in a fixed **mass** ratio. For Metha/LOX the volumes are equal (1 : 1 millibuckets); for LH2/LOX you need about 2.4 times as many millibuckets of hydrogen as oxygen. See [Fluids and Propellants](Fluids-and-Propellants.md#propellant-types). If you load too much of one fluid, the extra is dead weight, and the flight screen's Δv figure already accounts for it.

## Mass: what your rocket weighs

The rocket's weight decides whether your engines can lift it. The mod adds up masses as follows:

- **Every block** weighs **1 000 kg by default.**
- Engines weigh what the Engineer Table said (the *Mass* readout).
- A short list of blocks weighs something else (below).
- Everything in the fluid tanks counts: propellant at its density (for example 1 kg per mB of oxygen), other fluids as dead weight.

The default mass table (it is a datapack file, so it can be changed; see [Datapack and Modpack Guide](Datapack-and-Modpack-Guide.md#block-masses)):

| Block | Mass |
|---|---|
| Create Fluid Tank | 40 kg |
| Create Fluid Pipe | 300 kg |
| Small Rocket Engine (legacy) | 1 000 kg |
| Big Rocket Engine (legacy) | 3 000 kg |
| Small and Big engine structure blocks (the nozzle halves of the legacy engines) | 0 |
| Iron Block | 7 800 kg |
| Copper Block | 8 600 kg |
| Raw Copper Block | 8 000 kg |
| Gold Block | 19 000 kg |
| Raw Gold Block | 18 000 kg |
| Diamond Block | 2 500 kg |
| Raw Aluminum Block | 2 300 kg |
| Raw Cobalt Block | 5 000 kg |

The list also names a `super_engine_structure` block with mass 0, but the nozzle block of the designed Rocket Engine is actually called `engine_structure`, so it is **not** covered: in the default data **each designed Rocket Engine adds the engine's own mass *plus* 1 000 kg for its nozzle block.** Budget an extra tonne per engine.

The list also has entries written as `#forge:stone` (3 000 kg) and `#forge:ores` (4 000 kg). These use the old Forge tag namespace, so they may not match anything on NeoForge 1.21; every block that is not listed or tagged weighs the 1 000 kg default.

> [!NOTE]
> A solid rule of thumb: **a block is a tonne**. A rocket of 30 ordinary blocks weighs 30 tonnes before any fuel. Keep your hull lean, and use the cheap-by-mass blocks (tanks, pipes) where you can.

## Getting the height right

The rocket changes dimension when the **Rocket Controls reach Y = 300**, but the world ceiling is Y = 320 and the rocket cannot pass it. From the flight code this means:

- Launch from a position **below Y 300**. A rocket that begins at or above 300 gets a "propulsion" failure.
- Keep the part of the rocket **above the Rocket Controls shorter than about 20 blocks**, or the top of the hull reaches the ceiling before the controls reach 300 and the rocket stops. The simplest way is to put the Controls near the top of the rocket.

## Checklist before pressing "Create New Rocket"

- [ ] Rocket Controls is part of the build, with a clear column of air above the rocket.
- [ ] Engine thrust is greater than the loaded weight (see [Rocket Science Reference](Rocket-Science-Reference.md)).
- [ ] Each propellant is in a Create Fluid Tank, in the right proportion.
- [ ] The Δv you will have is at least the cost of your trip ([Planets and Travel](Planets-and-Travel.md)).
- [ ] Seats for everyone who is coming.
- [ ] Everything glued together.
- [ ] Spacesuits for the crew, if you are leaving Earth ([Life Support](Life-Support.md)).
