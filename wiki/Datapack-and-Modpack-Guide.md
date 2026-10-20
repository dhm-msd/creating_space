# Datapack and Modpack Guide

Most of Creating Space's content is **data-driven**, so modpack makers and datapack authors can add planets, propellants and engine designs, and change rules, without writing code. This page documents the formats, as read from the mod's codecs.

> [!NOTE]
> The data shipped inside the mod lives in `data/creatingspace/…`. Some folders in the source tree end in `-x` (for example `rocket_accessible_dimension-x`, `dimension-x`). Those are old copies that Minecraft does **not** load; do not use them as a reference. The live planet data is generated into `data/creatingspace/creatingspace/rocket_accessible_dimension/`.

Contents: [Planets](#planets-and-travel-costs) · [Propellants](#propellant-types) · [Power packs](#power-packs) · [Exhaust packs](#exhaust-packs) · [Block masses](#block-masses) · [Tags](#tags) · [Recipe types](#recipe-types) · [Dimension ids](#dimension-ids)

## Planets and travel costs

**Path:** `data/<namespace>/creatingspace/rocket_accessible_dimension/<name>.json`, where `<namespace>:<name>` is the **id of the dimension** you are describing. The Overworld is `data/minecraft/creatingspace/rocket_accessible_dimension/overworld.json`. The registry is synchronised to clients.

```json
{
  "gravity": 3.71,
  "arrivalHeight": 300,
  "orbitedBody": "creatingspace:sun",
  "distanceToOrbitingBody": 2000,
  "adjacentDimensions": {
    "creatingspace:mars_orbit": { "deltaV": 400 }
  }
}
```

| Field | Type | Meaning |
|---|---|---|
| `gravity` | number (m/s²) | Surface gravity. **`0` makes the world an orbit** (rockets stop there instead of landing; players below the bottom fall to the world in `orbitedBody`). |
| `arrivalHeight` | integer (Y) | Where rockets and fallen players arrive in this world. |
| `orbitedBody` | dimension id, optional (default `sun`) | The world below an orbit. Used for the "falling out of orbit" rule. |
| `distanceToOrbitingBody` | integer | Stored with the data, not used by the current game logic. |
| `adjacentDimensions` | map | Direct connections **from this world**: key is the destination dimension id; `deltaV` is the cost in m/s. |
| `adjacentDimensions.*.arrivalHeight` | integer, optional (default 64) | Accepted for compatibility; the game uses the destination world's own `arrivalHeight` instead. |

Rules:

- Connections are **one-way**: write both directions if you want both.
- The game computes the cheapest route between any two worlds (Dijkstra) from these edges. A rocket can choose as destination any world that has at least one connection leaving it.
- Gravity and arrival height are looked up per world, and missing worlds default to 9.81 m/s² and Y 64.
- You must also define the dimension and its dimension type yourself (standard Minecraft datapack files). The mod's own examples are in `data/creatingspace/dimension/` and `dimension_type/`.
- The mod's gravity scaling on entities does not apply to dimensions in the `ad_astra` or `ad_extendra` namespaces.

## Propellant types

**Path:** `data/<namespace>/creatingspace/propellant_type/<name>.json`

```json
{
  "propellantRatio": {
    "creatingspace:liquid_oxygen": 2,
    "creatingspace:liquid_methane": 1
  },
  "maxIsp": 460,
  "Cp": 4500,
  "gamma": 1.1,
  "M": 18
}
```

| Field | Meaning |
|---|---|
| `propellantRatio` | Map from a **fluid tag id** to a weight. The weights are normalised into a **mass** fraction. The engine looks for fluids in the rocket tagged with each id (for example `creatingspace:liquid_oxygen` is a fluid tag). |
| `maxIsp` | The ISP, in seconds, of a perfect engine with this propellant. |
| `Cp` | Specific heat. Higher means a cooler flame (see [Engine Design Reference](Engine-Design-Reference.md#formulas)). |
| `gamma` | Heat-capacity ratio (about 1.1 to 1.3). |
| `M` | Mean molar mass of the exhaust, in g/mol. |

The registry is synchronised to clients. Single-fluid propellants (like Premixed methalox) are supported as well as two-fluid ones.

## Power packs

**Path:** `data/<namespace>/creatingspace/power_pack_type/<name>.json`

```json
{ "combustionEfficiency": 0.9, "numberOfPumps": 2,
  "allowedPropellants": ["creatingspace:methalox", "creatingspace:lh2lox"] }
```

`combustionEfficiency` scales the flame temperature (and with it ISP). `numberOfPumps` is read but not used by any code. `allowedPropellants` lists propellant ids; a pack with an empty list is hidden from the table.

## Exhaust packs

**Path:** `data/<namespace>/creatingspace/exhaust_pack_type/<name>.json`

```json
{ "minExpansionRatio": 2, "maxExpansionRatio": 100,
  "allowedPropellants": ["creatingspace:methalox"] }
```

The expansion-ratio slider on the table spans `minExpansionRatio` to `maxExpansionRatio`. These also feed the engine mass formula. The shipped files contain a `slots` field that the loader ignores.

### Making a new design usable

A new power or exhaust pack also needs:

1. A **translation** key `power_pack_type.<namespace>.<name>` or `exhaust_pack_type.<namespace>.<name>`.
2. A **picture** for the table screen at `assets/creatingspace/textures/gui/rocket_engineer_table/<name>.png` (the screen always looks in the `creatingspace` namespace).
3. **Assembly recipes** that produce the power pack or exhaust pack item from an Engine Blueprint carrying `engineRecipeData` with the matching `powerPackType` / `exhaustPackType` (copy an existing file under `data/creatingspace/recipe/engine_recipe/`).
4. A way for players to **unlock** it: a *Design Blueprint* item with custom data `{"design": "<namespace>:<name>", "design_type": "creatingspace:power_pack_type"}` (or `creatingspace:exhaust_pack_type`), for example inside a loot table with `minecraft:set_components`. The shipped chests do exactly this.

## Block masses

**Path:** `data/creatingspace/creatingspace_utilities/blocks_mass.json`

```json
{ "values": { "minecraft:iron_block": 7800, "#minecraft:logs": 600 } }
```

Keys are block ids or `#`-prefixed block tags; values are kilograms. Unlisted blocks weigh **1 000 kg**. A datapack that supplies this file **replaces** the whole file (the highest-priority pack wins), so copy the default list and edit it. Block entities that report their own mass (the Rocket Engine) ignore the table.

## Tags

| Tag | Used for |
|---|---|
| Biome tag `creatingspace:no_oxygen` | Which biomes are airless. Includes the other biome tags `is_moon`, `is_mars`, `is_venus`. |
| Entity tag `creatingspace:space_creatures` | Entities immune to vacuum damage (skeleton by default). |
| Item tag `creatingspace:oxygen_sources` | Chest items that count as oxygen backtanks. |
| Item tag `creatingspace:spacesuit` | Items that count toward a "full suit". |
| Fluid tags `creatingspace:liquid_oxygen`, `liquid_hydrogen`, `liquid_methane`, `liquid_co2`, `monopropellant` | The propellant and oxygen fluids. Add other mods' fluids to these tags to make them usable as propellant. |

## Recipe types

| Type | Machine | Key fields |
|---|---|---|
| `creatingspace:air_liquefying` | Air Liquefier | `blockInFront` (block id), `dimension` (optional dimension id), `processing_time`, fluid `results` |
| `creatingspace:mechanical_electrolysis` | Mechanical Electrolyzer | fluid `ingredients`, fluid `results`, `processing_time` |
| `creatingspace:chemical_synthesis` | Catalyst Carrier | fluid `ingredients`, optional `catalyst` (an item ingredient; leave it out for no catalyst), `heat_requirement`, fluid `results`, `processing_time` |

The shipped examples are under `data/creatingspace/recipe/`.

## Dimension ids

`creatingspace:earth_orbit`, `creatingspace:moon_orbit`, `creatingspace:the_moon`, `creatingspace:mars_orbit`, `creatingspace:mars`, `creatingspace:venus`, plus `minecraft:overworld`.
