# Fluids and Propellants

Creating Space adds five fluids. All of them are **virtual fluids**: they live in tanks, pipes, basins and machines, but they have no bucket and cannot be poured into the world as a block.

| Fluid | Temperature | Density | Made by | Used for |
|---|---|---|---|---|
| **Liquid Oxygen** (LOX) | 90 K | 1 000 kg/m³ | [Air Liquefier](Machines.md#air-liquefier), [Mechanical Electrolyzer](Machines.md#mechanical-electrolyzer) | Rocket oxidiser, [oxygen backtanks](Spacesuit-and-Oxygen-Backtank.md), [Oxygen Sealers](Oxygen-Sealer.md), methane/monopropellant chemistry |
| **Liquid Hydrogen** (LH₂) | 10 K | 70 kg/m³ | [Mechanical Electrolyzer](Machines.md#mechanical-electrolyzer) | Rocket fuel, methane synthesis |
| **Liquid Methane** | 90 K | 500 kg/m³ | [Catalyst Carrier](Machines.md#catalyst-carrier) | Rocket fuel |
| **Liquid CO₂** | 180 K | 1 100 kg/m³ | [Air Liquefier](Machines.md#air-liquefier) facing a campfire | Methane synthesis |
| **Monopropellant** | 80 K | 350 kg/m³ | [Catalyst Carrier](Machines.md#catalyst-carrier) with a Nickel Sulfate Catalyst | Rocket propellant (needs the *Catalyse Cycle* power pack) |

Because a millibucket (mB) is a thousandth of a cubic metre, **1 mB weighs density ÷ 1000 kilograms**:

| Fluid | Mass of 1 mB |
|---|---|
| Liquid Oxygen | 1 kg |
| Liquid CO₂ | 1.1 kg |
| Liquid Methane | 0.5 kg |
| Monopropellant | 0.35 kg |
| Liquid Hydrogen | 0.07 kg |

> [!NOTE]
> Fluid mass matters a lot: everything in the tanks counts towards the rocket's weight and towards how much Δv it has. Hydrogen is very light per millibucket, which is why LH₂/LOX rockets need a lot of tank volume. See [Rocket Science Reference](Rocket-Science-Reference.md).

## Propellant types

A *propellant type* is a recipe for a burn: which fluids, in what **mass** ratio, and how energetic it is. The table at the engineer's desk shows these as "Metha/LOX", "LH2/LOX" and so on.

| Propellant | Fluids | Mass ratio | Volume ratio (what you actually pipe in) | Max ISP | Notes |
|---|---|---|---|---|---|
| **Metha/LOX** (`methalox`) | Liquid Oxygen + Liquid Methane | 2 : 1 | **1 : 1** (equal millibuckets) | 460 s | Available to every power pack except the Catalyse Cycle. |
| **LH2/LOX** (`lh2lox`) | Liquid Hydrogen + Liquid Oxygen | 1 : 6 hydrogen : oxygen | about **2.4 : 1** hydrogen : oxygen | 540 s | Hottest and most efficient. Only the staged-cycle power packs support it. Needs very strong materials unless the chamber is large. |
| **Premixed methalox** (`monoprop`) | Monopropellant (one fluid) | n/a | n/a | 600 s | Only the Catalyse Cycle power pack supports it. |
| Metallic hydrogen (`metalic_hydrogen`) | Liquid Hydrogen | n/a | n/a | 6 000 s | Defined in the data, but **no power pack or nozzle allows it**, so it cannot be used. |

A rocket only burns what its engines call for. If you mix engines with different propellants on the same rocket, each fluid is consumed in proportion. If one fluid runs out before the others, the rest is dead weight at the end of the burn; the Δv shown by the game already accounts for that. See [Rocket Science Reference](Rocket-Science-Reference.md#mixture-ratio).

> [!TIP]
> A Metha/LOX rocket wants the **same number of millibuckets** of methane and oxygen. If you use Create fluid tanks, giving both propellants the same total tank volume works out about right.

## How to make each fluid

| Goal | Machine | Inputs | Output |
|---|---|---|---|
| Liquid Oxygen from air | Air Liquefier facing open air, in the **Overworld** | rotation only | 100 mB per cycle |
| Liquid CO₂ | Air Liquefier facing a **campfire**, in the **Overworld** | rotation only | 100 mB per cycle |
| Liquid Hydrogen + Liquid Oxygen | Mechanical Electrolyzer over a basin | 100 mB water | 160 mB LH₂ **and** 80 mB LOX |
| Liquid Methane | Catalyst Carrier over a **heated** basin, with the catalyst slot **empty** | 100 mB Liquid CO₂ + 286 mB LH₂ | 80 mB methane **and** 90 mB water |
| Monopropellant | Catalyst Carrier over a **heated** basin holding a Nickel Sulfate Catalyst | 100 mB methane + 286 mB LOX | 80 mB monopropellant |

Machine details, stress, and speed behaviour are on the [Machines](Machines.md) page.

> [!IMPORTANT]
> The Air Liquefier recipes in the current data only work in the **Overworld**. You cannot liquefy air on the Moon, Mars or Venus with the default recipes. Datapacks can add more (see [Datapack and Modpack Guide](Datapack-and-Modpack-Guide.md)).

## Cryogenic Tank (carrying fluids)

The **Cryogenic Tank** holds up to 4 000 mB of any fluid colder than 200 K (all five mod fluids qualify; water does not). It keeps its contents when you break it and carry it as an item. It is a convenient bucket for cold liquids, but it is **not** part of a rocket's propellant storage; use Create fluid tanks for that. See [Building a Rocket](Building-a-Rocket.md#fuel-tanks).
