# Requirements and Installation

## What you need

| Component | Version | Notes |
|---|---|---|
| Minecraft | 1.21.1 | The mod's `minecraft_version` is 1.21.1 (accepted range 1.21.1 up to, but not including, 1.22). |
| NeoForge | 21.1.x | The mod is built against NeoForge 21.1.219 and accepts any NeoForge 21.1.0 or newer. |
| Create | 6.0.9 or newer | **Required.** Creating Space declares Create as a mandatory dependency, and almost every system (contraptions, fluid tanks, sequenced assembly, basins, kinetic stress) is built on it. The mod is compiled against `6.0.9-216`. |
| JEI | optional | If JEI is installed, Creating Space adds JEI categories for Air Liquefying, Chemical (synthesis) and Electrolysis recipes. |

Create 6 brings its own required libraries (Flywheel and Ponder); install whichever versions your Create build asks for.

> [!IMPORTANT]
> Creating Space 1.7.x for 1.21.1 is a different codebase from the 1.20.1 and 1.19.2 releases. Older guides (including parts of the Fandom wiki) may describe mechanics that no longer exist, for example the old Chemical Synthesizer block, which is now marked deprecated in the mod's own tooltip text. Always check that a guide matches your Minecraft version.

## Installing

1. Install NeoForge for Minecraft 1.21.1.
2. Put the Create jar (and the libraries it requires) in your `mods` folder.
3. Put the Creating Space jar in the same folder.
4. Optionally add JEI so you can look up the mod's custom recipe types.

On a **dedicated server** every player must have the mod too, because Creating Space adds blocks, items, entities and dimensions. The mod also synchronises several data-driven registries (planets and propellant types) from the server to clients.

## Where the mod keeps its settings

The mod registers three config files: client, common and server. See [Configuration](Configuration.md) for every option and its default.

## Worlds and dimensions

You do **not** need a special world type. The mod's dimensions (Earth Orbit, The Moon, Moon Orbit, Mars, Mars Orbit and Venus) are defined by the mod's own data, so they exist in every world. You reach them by rocket. See [Planets and Travel](Planets-and-Travel.md).

## Getting help

- Check [Troubleshooting and FAQ](Troubleshooting-and-FAQ.md).
- Ask in the community [Discord](https://discord.gg/Dn9DhTqarH).
- Report bugs on the [issue tracker](https://github.com/RealAntEngineer/creating_space/issues).
