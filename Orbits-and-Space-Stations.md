# Orbits and Space Stations

There are three orbit worlds: **Earth Orbit**, **Moon Orbit** and **Mars Orbit**. They are the cheap hubs of the travel network (see the [Δv map](Planets-and-Travel.md#delta-v-map)), and they are where you build space stations.

| | Earth Orbit | Moon Orbit | Mars Orbit |
|---|---|---|---|
| Orbits | The Earth | The Moon | Mars |
| Arrival height | Y 64 | Y 64 | Y 64 |
| Gravity | 0 | 0 | 0 |
| Cost to reach from the Earth's surface | 1 500 | 2 100 | 2 500 |

## What an orbit world is like

- It is a **completely empty void**: no terrain, no structures, no mobs. There is no ground to stand on, so you bring your own.
- Its only biome is **Space**, and it is **airless**. You need a [spacesuit](Spacesuit-and-Oxygen-Backtank.md) or a [pressurised room](Oxygen-Sealer.md).
- **Gravity is zero.** If you are in the air, holding **jump** accelerates you up and **sneaking** accelerates you down. Items, boats and falling blocks do not fall.
- Beds work here.

## Arriving

When a rocket arrives in an orbit it stops at Y 64, above the X/Z you chose in the schedule (or the same X/Z it left from). Nothing is under it, but with zero gravity it simply hangs there. Open the rocket screen and press **Disassemble** to turn the rocket back into blocks at that spot.

## Building a space station

1. Fly a rocket to the orbit and **Disassemble** it. The blocks are placed in a floating cluster.
2. Build outwards from those blocks. Blocks can float in the void, so you can attach new ones to any existing face.
3. Seal the hull with full solid blocks, put an [Oxygen Sealer](Oxygen-Sealer.md) inside and feed it **Liquid Oxygen** (bring it by rocket, or make it with an [electrolyzer](Machines.md#mechanical-electrolyzer) running on water you brought). Now you can walk around without a suit.
4. Use it as a fuelling and cargo hub: [schedule conditions](Launching-and-Flight.md#wait-conditions) like *Idle Inventory* and *Fluid Threshold* let a rocket wait for cargo.

> [!TIP]
> Station-keeping is free: nothing in an orbit world moves on its own. Once a block is placed, it stays.

## Falling out of orbit

If a **player** drops below the bottom of an orbit world (below Y −54), the game catches them and sends them down to the planet the orbit belongs to:

| From | You land on | Arrival height |
|---|---|---|
| Earth Orbit | The Earth | Y 200 |
| Moon Orbit | The Moon | Y 300 |
| Mars Orbit | Mars | Y 300 |

You keep your X/Z position, and if you are riding something it comes with you. You then fall from that height under the planet's gravity, so a drop onto the Earth from Y 200 is dangerous unless you land in water; on the Moon the fall damage is scaled down to about a sixth.

Only players are rescued this way: items, mobs and loose blocks that fall out of the bottom just keep falling.
