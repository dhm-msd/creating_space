# Rocket Engines

Creating Space does not give you a fixed list of engines. You **design** each one at the **Rocket Engineer Table**, the table produces an **Engine Blueprint**, and you then manufacture the engine with Create's sequenced assembly. This page explains the design step. The recipes are on [Engine Crafting](Engine-Crafting.md), and all formulas, ranges and data are on [Engine Design Reference](Engine-Design-Reference.md).

## The big picture

```
Rocket Engineer Table ──► Engine Blueprint ──► (copy it with paper)
                                   │
                                   ▼
                     Create sequenced assembly
                     (power pack + exhaust pack + parts)
                                   │
                                   ▼
                              Rocket Engine ──► placed on your rocket
```

An engine is described by seven choices:

| Choice | What it controls |
|---|---|
| **Power pack** | How the propellants are pumped and burned. Decides combustion efficiency (and so chamber temperature and ISP) and which propellants you may use. |
| **Exhaust pack** | The nozzle type: **Bell Nozzle** or **Aerospike**. Decides the expansion-ratio range and the engine's mass. |
| **Propellant** | Which fluids the engine burns, and their maximum ISP. |
| **Size** | Combustion chamber volume, in millibuckets. Bigger chambers are heavier but run at lower pressure. |
| **Thrust** | Force in newtons. More thrust means higher chamber pressure. |
| **Expansion ratio** | How much the nozzle widens. Higher ratios give better ISP and a heavier engine. |
| **Material** | What the engine is built from. It must be strong enough for the chamber pressure at the chamber temperature. |

## Using the Rocket Engineer Table

Right-click the table to open its screen. The table remembers its settings.

**Selectors**

- **Power pack** (top left) and **Exhaust pack** (top right): scroll with the mouse wheel over the box. Only designs you have *unlocked* appear. New players start with the **Open Cycle** power pack and the **Bell Nozzle**; see [Blueprints and Designs](Blueprints-and-Designs.md) for how to unlock more.
- **Propellant** (bottom left): scroll to choose. Changing the power pack refreshes this list to the propellants that pack supports (for example the Open Cycle only offers Metha/LOX).
- **Size**: chamber volume in millibuckets (minimum 1). Hover text: "Heavier but decrease material requirement".
- **Thrust**: newtons, adjusted in steps of 1 000 (hold Shift for steps of 100 000). Hover text: "More thrust but increase material requirement".
- **Material**: nine levels, from Andesite (level 0) up to Hastelloy (level 8); the order is listed on [Resources and Materials](Resources-and-Materials.md#the-engine-material-ladder). In the current build the selector may show the raw names `creatingspace.material.andesite`, `creatingspace.material.iron`, and so on, because the language file has no entries for them. Hover text: "The material set the pressure limit at a given temperature".
- **Expansion ratio** slider: the range depends on the nozzle (Bell Nozzle 2–100, Aerospike 2–500).

**Readouts** (right-hand panel)

| Readout | Meaning |
|---|---|
| `ISP : n s` | Specific impulse of the finished engine, in seconds. Higher is more efficient. |
| `n / m bar` | **n** = the chamber pressure of your design; **m** = the highest pressure your chosen material can survive at your chamber temperature. You need n ≤ m. |
| `Mass : x t` | Engine mass in tonnes. This counts towards your rocket's weight. |
| Tooltip | The combustion temperature (°C) and pressure (bar) appear in a tooltip over the readout area. The mod places this tooltip using fixed screen coordinates, so it may not line up at every window size; the temperature of every design is also listed on [Engine Design Reference](Engine-Design-Reference.md#isp-by-expansion-ratio). |

**The confirm button** (check mark) only does anything when the design is valid, meaning the pressure is within the material's limit. It places an **Engine Blueprint** in the output slot on the right. Take it out, then you can design the next engine. If the slot still holds a blueprint, new ones cannot be made.

> [!TIP]
> If the pressure readout is above the limit, you have three levers: increase **Size** (lower pressure, heavier engine), reduce **Thrust**, or pick a stronger **Material**. Changing the power pack or propellant also changes the temperature, which changes the limit.

## How the choices push on each other

| If you… | Pressure | Temperature | ISP | Engine mass |
|---|---|---|---|---|
| raise **Size** | goes down | no change | no change | goes up (in proportion) |
| raise **Thrust** | goes up (in proportion) | no change | no change | no change |
| raise **Expansion ratio** | goes down slightly | no change | goes up | goes up |
| use a more **efficient power pack** | no change | goes up | goes up | no change |
| switch to **LH2/LOX** | similar | goes way up | goes way up | no change |

The engine's chamber pressure is independent of the power pack's efficiency (efficiency affects temperature and ISP instead).

## Example designs

Computed with the mod's formulas (the game rounds down, and tiny floating-point differences can move a value by one), using 100 kN of thrust and an expansion ratio of 50, Metha/LOX on the Open Cycle power pack (ISP 289 s, chamber at 1 883 °C):

| Size | Chamber pressure | Cheapest material that works | Bell nozzle mass |
|---|---|---|---|
| 100 mB | 307 bar | Monel (level 6) | 0.30 t |
| 250 mB | 122 bar | Copronickel (5) | 0.76 t |
| 500 mB | 61 bar | Reinforced Copper (4) | 1.5 t |
| 1 000 mB | 30 bar | Brass (3) | 3.0 t |
| 5 000 mB | 6 bar | Copper (2) | 15 t |

More examples, including LH₂/LOX, are in [Engine Design Reference](Engine-Design-Reference.md#worked-examples).

## The finished engine

The **Rocket Engine** item remembers its design. Its tooltip lists ISP, mass and thrust, and the **ratio of fluids it consumes** (shown by volume or by mass; this is a [common-config](Configuration.md#common-config) option).

**Placing an engine.** An engine is two blocks tall: the engine on top and a non-solid "engine structure" block directly below it for the nozzle. Both spaces must be empty when you place it. When the rocket launches, the exhaust plume renders from the nozzle.

An engine can only be used on a rocket. Its thrust and mass are read when the rocket is assembled; see [Building a Rocket](Building-a-Rocket.md).

### Legacy fixed engines

The mod also contains a **Small Rocket Engine** and a **Big Rocket Engine** with fixed stats (Metha/LOX, efficiency 0.79). Their thrust comes from the [server config](Configuration.md#server-config) (default 98 100 N and 4 905 000 N). They have no crafting recipe in the mod's data, so normal progression uses the designed Rocket Engine.
