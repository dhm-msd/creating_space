# Life Support

Outside the Overworld, the Nether and the End, there is **no air**. This page lists exactly where that applies, what it does to you, and the three ways to stay alive.

## Where is there no air?

A place is airless when its **biome** is in the mod's `no_oxygen` biome tag. By default that is:

| World | Airless biomes |
|---|---|
| [The Moon](The-Moon.md) | Moon Plains, Moon Cave |
| [Mars](Mars.md) | Mars Plains, Mars Cave |
| [Venus](Venus.md) | Venus, Venus Hellground |
| [Orbits](Orbits-and-Space-Stations.md) (Earth, Moon, Mars) | Space |

Everywhere else (the Overworld, the Nether, the End, and other mods' biomes) is treated as breathable.

## What happens without air?

Once per second, every living thing standing in an airless place is checked.

### Players

| Situation | Result |
|---|---|
| Creative mode or spectator | Nothing happens. |
| Wearing a **full spacesuit** whose backtank still has oxygen | The backtank loses **1 unit of oxygen** and you take no damage. |
| Anything else | You take **2 damage** (one heart) that **ignores armour** and does not knock you back. The death message is "*player* didn't find oxygen in space". |
| Anything else, **on Venus** | An additional **0.5 damage** per second ("overheating"). This extra damage is not applied if you are in a working suit. |

A "full spacesuit" means: a chest piece from the *oxygen sources* tag (the Copper or Netherite Oxygen Backtank) **with oxygen left**, **and** a helmet, leggings and boots from the *spacesuit* tag. Basic and Advanced pieces may be mixed freely. See [Spacesuit and Oxygen Backtank](Spacesuit-and-Oxygen-Backtank.md).

### Who is affected?

- **Other living creatures** (animals, villagers, zombies and so on) take the same 2 damage plus 0.5 "overheating" damage every second in any airless place, unless they are in a pressurised room.
- **Skeletons are exempt.** They are the only creature in the mod's `space_creatures` list, which is why they roam the Moon.
- Armour does not help, because the damage bypasses it.

## Three ways to breathe

1. **A spacesuit.** Mobile, but your backtank has a limited amount of oxygen (15 minutes by default; see below). Refill it from a liquid-oxygen line.
2. **A pressurised room.** An [Oxygen Sealer](Oxygen-Sealer.md) fills a sealed room with oxygen. Anyone in the room breathes freely without a suit, and also isn't hurt by Venus's heat.
3. **A world with air.** The Overworld, the Nether and the End.

## Oxygen numbers at a glance

| Thing | Default |
|---|---|
| Backtank capacity | 900 units, +300 per level of Create's *Capacity* enchantment (read from Create's own backtank config) |
| Suit oxygen use | 1 unit per second, so 15 minutes on the default tank |
| Oxygen from 1 mB of Liquid Oxygen | 1 backtank unit |
| Room: oxygen from 1 mB of Liquid Oxygen | 10 room units |
| Room: oxygen a creature breathes | 10 room units per tick (200 per second) |
| Room: oxygen a leaf block makes | 2 room units per tick |
| Room breathable when | closed, and at least 10 units of oxygen per block of volume |
| Room: biggest size per sealer | 1 000 blocks |

The room numbers can be changed in the [server config](Configuration.md#server-config).

## Create's own backtanks

Create's regular air backtank (when placed as a block, it refills from rotation) **stops refilling in airless biomes**: the mod suspends that behaviour where there is no air. Use the oxygen backtanks for space.

## Tips

- **Pack a spare tank.** Every backtank tracks its own oxygen, and the gauge on your HUD shows the one you are wearing.
- **Don't build wooden farms outside a room on Venus**: see [Venus](Venus.md#fire).
- If you are about to run out, the game shows a warning in the middle of the screen at **10 %** and again when the backtank is **empty**.
