# Creating Space wiki sources

This folder holds a complete player and modpack-maker wiki for Creating Space, written as plain Markdown so it can be reviewed in a pull request, read directly on GitHub, or copied into the repository's GitHub Wiki.

**Start at [Home.md](Home.md).**

## What it covers

Getting started, every machine and item, the rocket-engine designer and its formulas, building and flying rockets, every world and travel cost, life support and oxygen rooms, configuration, commands, the datapack formats, a glossary, troubleshooting, and a candid list of known issues. Page list: see [Home.md](Home.md) or [_Sidebar.md](_Sidebar.md).

## How it was checked

Everything was written from the **source code and data files**, not from memory or from older wikis:

- Based on the `1.21.1-release` branch, **mod version 1.7.23**, commit `211ffbbb`.
- Gameplay rules come from `src/main/java`, with numbers from `src/main/resources/data` and the generated data in `src/generated/resources/data` (recipes, planets, dimensions, loot tables, language file).
- Where the mod depends on Create's behaviour or defaults (backtank capacity, tank size, mounted fluid storage, mixer timings, contraption size limit), the values were read from the Create 6.0.9-216 jar the mod is compiled against.
- Engine-table numbers on [Engine Design Reference](Engine-Design-Reference.md) and [Rocket Engines](Rocket-Engines.md) were computed by re-implementing the mod's formulas, and the Δv matrix on [Planets and Travel](Planets-and-Travel.md) by running the same shortest-path search on the planet data.
- No page repeats the older Fandom wiki; where the older documentation disagreed with the code, the code won.

> [!IMPORTANT]
> The pages were **not play-tested in a running game.** Behaviour that is derived from reading code rather than observed is the most likely to be slightly off. Things worth a quick in-game check before publishing:
>
> 1. How blocks get collected into a rocket (the pages describe Create's standard glue/attachment rules) and the "keep the part above the Controls shorter than ~20 blocks" rule ([Building a Rocket](Building-a-Rocket.md#getting-the-height-right)).
> 2. A rocket whose pre-flight check fails staying "in transit" until the schedule is re-sent.
> 3. The Cryogenic Tank not counting as rocket propellant storage.
> 4. How well leaves contribute to room oxygen, and which non-full blocks leak.
> 5. Air Liquefier / Electrolyzer cycle times (they follow Create's mixer formula).
> 6. The two advancement files not loading because of their folder name.

## Conventions

- File names use hyphens (`Engine-Crafting.md`), the way GitHub Wiki expects.
- Links between pages are relative Markdown links with the `.md` extension, so they work in this folder.
- Callouts use GitHub's `> [!NOTE]` / `[!TIP]` / `[!IMPORTANT]` / `[!WARNING]` syntax (rendered nicely on GitHub, readable as plain quotes elsewhere).
- One diagram uses a ```` ```mermaid ```` block (GitHub renders it).
- There are no images, so nothing depends on files outside this folder, apart from one link to [`../CREDITS.md`](../CREDITS.md) on the Home page.

## Publishing to the GitHub Wiki

The files can be copied into the `.wiki.git` repository unchanged, except that wiki links normally omit the `.md` extension. Convert them on copy:

```bash
mkdir -p /tmp/wiki-out
for f in wiki/*.md; do
  sed -E 's/\]\(([A-Za-z0-9_-]+)\.md(#[^)]*)?\)/](\1\2)/g' "$f" > "/tmp/wiki-out/$(basename "$f")"
done
```

(`README.md` is not needed in the wiki itself, and the `../CREDITS.md` link on the Home page should be pointed at the repository URL there.)

## Source map: where each page's facts come from

When the mod changes, these are the files to re-check.

| Page(s) | Main sources |
|---|---|
| Rocket flight, Δv, speed | `content/rocket/RocketContraptionEntity.java`, `content/rocket/contraption/RocketContraption.java`, `…/entity/RocketStorageManager.java`, `legacy/utilities/data/FlightDataHelper.java`, `content/rocket/CSMassUtil.java`, `data/creatingspace/creatingspace_utilities/blocks_mass.json` |
| Schedule screen and conditions | `content/rocket/ScheduleMakingScreen.java`, `content/rocket/squedule/**` |
| Planets and travel | `content/planets/CSDimensionUtil.java`, `api/planets/RocketAccessibleDimension.java`, `data/minecraft/creatingspace/rocket_accessible_dimension/overworld.json`, `src/generated/…/rocket_accessible_dimension/*.json` (from `content/datagen/worldgen/CSRocketAccessibleDimensionGen.java`) |
| Engine designer | `content/rocket/engine/design/*`, `content/rocket/engine/table/*`, `init/EngineMaterialInit.java`, `data/creatingspace/creatingspace/{power_pack_type,exhaust_pack_type,propellant_type}/` |
| Engine crafting | `data/creatingspace/recipe/engine_recipe/**`, `data/creatingspace/recipe/engine_ingredients/**`, `init/ingameobject/ItemInit.java` |
| Life support | `content/event/CSEventHandler.java`, `content/life_support/**`, `data/creatingspace/tags/**` |
| Machines and chemistry | `content/recipes/**`, `content/fluids/**`, `init/ingameobject/BlockInit.java`, `init/ingameobject/FluidInit.java`, generated recipes |
| Gravity | `mixin/entity/gravity/*`, `mixin/entity/PlayerMixin.java` |
| Worldgen and structures | `data/creatingspace/worldgen/**`, `data/creatingspace/structure/**`, generated loot tables |
| Configuration and commands | `configs/*.java`, `init/CommandsInit.java` |

## Contributing changes

Improvements and corrections are welcome. Please keep claims checkable against the code, and cite the source file in the PR description when you change a number.
