# Machines

This page covers every functional block the mod adds, except rocket engines (see [Rocket Engines](Rocket-Engines.md)) and oxygen-related gear (see [Life Support](Life-Support.md)).

Stress numbers below are the mod's defaults and follow Create's convention: the listed value is the **impact per RPM**, so a machine with impact 128 turning at 64 RPM loads the network with 128 × 64 = 8 192 SU. You can change them in the [server config](Configuration.md#stress-values).

Contents: [Air Liquefier](#air-liquefier) · [Mechanical Electrolyzer](#mechanical-electrolyzer) · [Catalyst Carrier](#catalyst-carrier) · [Oxygen Sealer](#oxygen-sealer) · [Cryogenic Tank](#cryogenic-tank) · [Flow Meter](#flow-meter) · [Rocket Engineer Table](#rocket-engineer-table) · [Rocket Controls](#rocket-controls) · [Flight Recorder](#flight-recorder) · [Clamps](#clamps) · [Rocket Casing](#rocket-casing)

---

## Air Liquefier

*Pulls a gas out of the air in front of it and liquefies it. Needs rotation.*

**Crafting** (shaped):

```
 .  S  .      S = brass plate (c:plates/brass)
 C  P  C      C = Create brass casing
 .  T  .      P = Create encased fan, T = Create fluid tank
```

| Property | Value |
|---|---|
| Stress impact | 128 SU per RPM |
| Output buffer | Two internal output tanks of 1 000 mB each. Nothing can be pumped *in*. |
| Pipe connections | Any face except the face it points at and the two faces on its shaft axis. |

**What it makes** depends on the block directly in front of its open face (the face it is pointing at):

| Block in front | Dimension | Result per cycle |
|---|---|---|
| Air | Overworld only | 100 mB Liquid Oxygen |
| Campfire | Overworld only | 100 mB Liquid CO₂ |

It stops when the output tanks are full. Other dimensions have no recipe by default.

**Cycle time.** Like Create's Mechanical Mixer, faster rotation shortens a cycle, in steps. With the default recipe time of 200 the cycle takes `30 × floor(log₂(floor(512 ÷ RPM))) + 1` ticks (never less than 1 or more than 512):

| RPM | 8 | 16 | 32 | 64 | 128 | 256 |
|---|---|---|---|---|---|---|
| Ticks per cycle | 181 | 151 | 121 | 91 | 61 | 31 |
| 100 mB every | 9 s | 7.5 s | 6 s | 4.5 s | 3 s | 1.5 s |

Speeds between the powers of two use the next lower row (for example 100 RPM behaves like 64).

---

## Mechanical Electrolyzer

*Splits water into hydrogen and oxygen. Works like a Mechanical Mixer over a Basin.*

**Crafting** (shaped):

```
 X  S  X      X = Create copper casing, S = Create shaft
 C  C  C      C = Copper Coil
 G  T  G      G = gold plate (c:plates/gold), T = Create fluid tank
```

The **Copper Coil** is crafted from 8 copper ingots in a ring (`CCC / C C / CCC`).

| Property | Value |
|---|---|
| Stress impact | 1 024 SU per RPM |
| Placement | Sideways shaft (like the Mechanical Mixer) with **one empty block** between it and the Basin below; it cannot be placed directly on top of a Basin. |
| Recipe | 100 mB water → 160 mB Liquid Hydrogen + 80 mB Liquid Oxygen |

Feed water into the basin through pipes (or a spout/drain) and pipe the products away from the basin's outputs, exactly as with other Create basin machines. Processing time is `30 × floor(log₂(floor(512 ÷ RPM))) + 1` ticks, the same formula as the Air Liquefier, plus about 2 seconds for the head to dip and rise.

---

## Catalyst Carrier

*A mixer-like head for chemistry that sometimes needs a catalyst. Works over a Basin.*

**Crafting** (shaped):

```
 .  G  .      G = gold plate
 N  P  N      N = nickel ingot, P = Create mechanical press
 .  G  .
```

| Property | Value |
|---|---|
| Stress impact | 8 SU per RPM |
| Placement | Same as the Mechanical Mixer: sideways shaft, one empty block above the Basin. |
| Heat | Both mod recipes need a **heated** Basin (a lit Blaze Burner underneath). |

**Catalyst slot.** Right-click the carrier with a *Nickel Sulfate Catalyst* to load it. Right-click again with an empty hand to take it back, or with another catalyst to swap. Other items are ignored (they use the block normally). Each time a recipe completes, the catalyst loses 1 durability (it has 100).

**Recipes:**

| Recipe | Catalyst slot | Inputs | Outputs |
|---|---|---|---|
| Methane synthesis | **Must be empty** | 100 mB Liquid CO₂ + 286 mB Liquid Hydrogen | 80 mB Liquid Methane + 90 mB water |
| Monopropellant synthesis | **Nickel Sulfate Catalyst** | 100 mB Liquid Methane + 286 mB Liquid Oxygen | 80 mB Monopropellant |

Both take the same 200-tick base time as the other basin machines.

> [!NOTE]
> The methane recipe lists no catalyst, and a recipe without a catalyst only matches an *empty* carrier. If your methane line stalls, check that you did not leave a catalyst in the carrier.

**Nickel Sulfate Catalyst** is crafted by stacking one Nickel Sulfate Shard above one iron plate (`" S " / " I "` in the middle column). Shards come from Mars geodes, see [Resources and Materials](Resources-and-Materials.md#nickel-sulfate-geodes-mars).

> [!WARNING]
> The old **Chemical Synthesizer** block no longer exists in 1.21.1. Its tooltip text is still in the language file marked "DEPRECATED"; the Catalyst Carrier replaces it.

---

## Oxygen Sealer

Pressurises a sealed room with oxygen. It has its own page: [Oxygen Sealer and Pressurised Rooms](Oxygen-Sealer.md).

---

## Cryogenic Tank

*A 4 000 mB portable tank for cold liquids.*

**Crafting:** a Create fluid tank in the centre, red wool above/below/left/right, nickel plates in the four corners (`NWN / WTW / NWN`).

- Accepts any fluid with a temperature under 200 K (every mod fluid; not water or lava).
- Keeps its contents when broken, and the carried item shows the fluid. In item form it exposes a standard fluid-handler, so it can be filled and emptied by item-fluid tools.
- Pipes and pumps connect to it from any side.
- It is **not** counted as propellant storage when a rocket is assembled. See [Building a Rocket](Building-a-Rocket.md#fuel-tanks).

---

## Flow Meter

*A gauge that sits in a pipe and shows how fast fluid is moving.*

**Crafting:** a compass above a Create copper casing.

Place it **inline** in a pipe run, with the dial facing you and the pipe running left-to-right across it (it connects to the two sides next to its dial face). The dial moves with the flow and the number, labelled `mB/t`, appears in the Engineer's Goggles tooltip.

---

## Rocket Engineer Table

*Where you design engines.* Full guide: [Rocket Engines](Rocket-Engines.md).

**Crafting:** two rows of 3 wooden slabs on top of a smooth stone (`WWW / WWW / .S.`).

---

## Rocket Controls

*The brain of every rocket.* Full guide: [Building a Rocket](Building-a-Rocket.md).

**Crafting:**

```
 E  R  E      E = Create electron tube, R = Create redstone link
 E  T  E      T = Create train controls (the "Controls" block)
 S  S  S      S = Create sturdy sheet
```

Crafting a Rocket Controls on its own in the crafting grid gives you a fresh one back (it resets the stored custom name).

---

## Flight Recorder

*A black box that explains why a rocket would not launch.*

**Crafting:** two Create brass casings above and below, a Create shaft on each side, and a dried kelp block in the middle (`.B. / AKA / .B.`).

Right-click it on an assembled rocket to read the result of the last launch attempt, or **sneak + right-click** for a live readout of the rocket's mass, Isp, propellant mass and computed Δv. The last-flight information is stored in the block, so after the rocket is disassembled you read it with Engineer's Goggles. What the messages mean is covered in [Troubleshooting and FAQ](Troubleshooting-and-FAQ.md#reading-the-flight-recorder).

You can choose whether propellant amounts are shown by volume or by mass in the [common config](Configuration.md#common-config).

---

## Clamps

*An immovable block.*

**Crafting (makes 4):** iron blocks and Create copper casings in a checkerboard (`ICI / CIC / ICI`).

Clamps carry Create's "non-movable" block tag, so a contraption can never pick them up. Use them for launch pads and anything you want to stay put beside a rocket. The in-game tooltip describes them as preventing a contraption from moving.

---

## Rocket Casing

*A decorative Create-style casing for hull panels.*

**Crafting:** a checkerboard of cobalt ingots and aluminium plates (`CSC / SCS / CSC`). It has no special mechanics; it exists so rockets can have their own look and connect with Create's casing textures.
