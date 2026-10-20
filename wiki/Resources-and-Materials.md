# Resources and Materials

Creating Space adds three new ore metals (nickel, aluminium, cobalt) and five alloys. The alloys exist for one reason: they are the tougher metals you need to build high-pressure, high-temperature [rocket engines](Rocket-Engines.md).

## Ores and where to find them

| Ore | Where | How often | Height (Y) | Tool needed |
|---|---|---|---|---|
| **Nickel Ore** / **Deepslate Nickel Ore** | Overworld, any biome | 5 veins of up to 9 blocks per chunk | −64 to 120, most common near the middle | Iron pickaxe |
| **Moon Nickel Ore** | [The Moon](The-Moon.md), plains and cave biomes | 20 veins of up to 9 per chunk | −64 to 120, most common near the middle | Iron pickaxe |
| **Moon Aluminum Ore** | The Moon | 10 veins of up to 9 per chunk | −64 to 60, most common near the middle | Iron pickaxe |
| **Moon Cobalt Ore** | The Moon | 5 veins of up to 9 per chunk | −64 to 60, most common near the middle | **Diamond** pickaxe |
| **Nickel Sulfate geodes** | [Mars](Mars.md), cave biome | About 1 attempt in 24 chunks | From 6 blocks above the world bottom (Y −58) up to Y 30 | Pickaxe (needs the correct tool to drop) |

Notes:

- "Most common near the middle" is Minecraft's *trapezoid* height distribution: the ore peaks halfway between the minimum and maximum height and thins out towards both ends.
- Moon ores only replace **Moon Stone**.
- Cobalt is the gatekeeper metal. Besides Moon Cobalt Ore, you can also get small amounts of cobalt by washing Mars or Moon regolith (see below).
- Ores follow Minecraft's normal Fortune rules (they drop *Raw Nickel*, *Raw Aluminum* or *Raw Cobalt*); Silk Touch gives you the ore block.

### Nickel Sulfate geodes (Mars)

Mars geodes are built from, outside to inside: Create's **Crimsite**, Create's **Veridium**, then **Nickel Sulfate Block** and **Budding Nickel Sulfate**, with small, medium and large **Nickel Sulfate Buds** and **Nickel Sulfate Clusters** growing inside.

- A *Budding Nickel Sulfate* block slowly grows crystals on random sides (on each random tick there is a 1-in-5 chance it tries, and it can only grow into air or a full water source block). The growth order is Small Bud → Medium Bud → Large Bud → Cluster, just like Minecraft's amethyst.
- Breaking a **Nickel Sulfate Cluster** drops **Nickel Sulfate Shards** (Fortune increases the number; Silk Touch keeps the cluster).
- Shards are the key ingredient of the **Nickel Sulfate Catalyst**, see [Machines](Machines.md#catalyst-carrier).

## Processing metals

All three ore metals have the usual Create-style family: raw item, ingot, nugget, sheet (plate) and storage blocks. Nuggets and sheets carry the common `c:` tags so they work with other mods' recipes.

| Step | Recipe |
|---|---|
| Smelting / blasting | Ore, raw ore or *crushed* ore → 1 ingot (nickel, aluminium, cobalt). |
| Crushing (Create Crushing Wheels) | Nickel Ore → 1 crushed nickel + 75 % chance of a second one + 75 % chance of an experience nugget + 12.5 % chance of cobblestone. Deepslate Nickel Ore → 2 crushed nickel + 25 % chance of a third + the same bonuses (with cobbled deepslate). Moon Aluminum and Moon Cobalt Ore → 1 crushed ore + 75 % chance of a second + bonuses. Raw metal items and raw blocks can be crushed too. |
| Washing (Create Encased Fan splashing) | Crushed nickel / aluminium / cobalt → **9 nuggets** (one ingot's worth). |
| Pressing (Create Mechanical Press) | Ingot → sheet. Available for aluminium, cobalt, nickel and all five alloys. |

### Regolith washing

Moon and Mars stone can be crushed into regolith, and regolith can be washed for a *chance* at metal nuggets:

| Block | Crushing | Washing results (each independent chance) |
|---|---|---|
| Moon Stone | → Moon Regolith | 12.5 % for 2 gold nuggets · 8 % for 2 nickel nuggets · 4 % for 1 aluminium nugget · 4 % for 1 cobalt nugget |
| Mars Stone | → Mars Regolith | 12.5 % for 3 cobalt nuggets · 8 % for 3 nickel nuggets · 4 % for 3 aluminium nuggets |

Moon Stone can also be cut with a stonecutter into **Moon Stone Brick** or **Polished Moon Stone**.

## Alloys

Alloys are mixed in a Create **Basin** with a **Mechanical Mixer** over a Blaze Burner.

| Alloy | Ingredients | Heat |
|---|---|---|
| **Reinforced Copper** | 1 copper ingot + 3 iron nuggets | Heated |
| **Copronickel** (Copper–Nickel) | 1 copper ingot + 3 nickel nuggets | Heated |
| **Monel** | 1 nickel ingot + 3 copper nuggets | Superheated |
| **Inconel** | 1 nickel ingot + 3 iron nuggets | Superheated |
| **Hastelloy** | 1 copper ingot + 1 iron ingot + 2 nickel ingots + 2 cobalt ingots | Superheated |

Each recipe produces 1 ingot. "Heated" means a lit Blaze Burner under the basin; "Superheated" means a Blaze Burner fuelled with a Blaze Cake (Create's rules). Alloy ingots, nuggets, sheets and storage blocks all exist.

> [!NOTE]
> Some older guides list different alloy ratios (for example "2 copper + 1 iron"). The recipes above are the ones in the current mod data.

## The engine material ladder

When you design an [engine](Rocket-Engines.md), you choose a material. The mod has nine, ordered from weakest to strongest. A material's level (0–8) is just its position in this list.

| Level | Material | Max pressure (bar, at 0 °C) | Temperature where it fails (°C) | Where it comes from |
|---|---|---|---|---|
| 0 | Andesite | 3 | 900 | Create Andesite Alloy |
| 1 | Iron | 50 | 1 200 | Vanilla iron / Create iron sheet |
| 2 | Copper | 80 | 2 200 | Vanilla copper / Create copper sheet |
| 3 | Brass | 150 | 2 500 | Create brass |
| 4 | Reinforced Copper | 250 | 2 800 | Alloy |
| 5 | Copronickel | 400 | 3 200 | Alloy |
| 6 | Monel | 650 | 3 800 | Alloy |
| 7 | Inconel | 900 | 4 500 | Alloy |
| 8 | Hastelloy | 1 200 | 5 500 | Alloy |

How strong a material is *at a given temperature* is explained in [Engine Design Reference](Engine-Design-Reference.md#materials): the allowed pressure falls in a straight line from the "max pressure" at 0 °C down to zero at the failure temperature.

## Which metals do I need for which engine part?

Every engine part is made from **one** material (the one you picked on the table). The pieces are:

| Part | Made from |
|---|---|
| Engine wall | Cut from one sheet of the material |
| Rib | Nuggets + ingot of the material (crafting table) |
| Turbine shaft | 3 ingots of the material (crafting table, diagonal) |
| Blisk | Nuggets + sheets + ingot of the material (crafting table) |
| Injector | A Create Sturdy Sheet + one sheet and one nugget of the material (sequenced assembly) |

The Andesite tier is the exception: it uses Create Andesite Alloy (and vanilla iron nuggets) in place of the "ingot/nugget/sheet" of the material. Details and exact patterns are on [Engine Crafting](Engine-Crafting.md).
