# Oxygen Sealer and Pressurised Rooms

The **Oxygen Sealer** fills an enclosed room with breathable air. People inside the room can take their helmets off: no suit needed, no oxygen backtank use, and no extra Venus heat damage. This is how you build bases, greenhouses and space stations.

## The block

**Crafting:**

```
 N  P  N      N = nickel plate
 C  T  C      P = Create propeller, T = Create fluid tank
 C  C  C      C = Create copper casing
```

| Property | Value |
|---|---|
| Stress impact | 8 SU per RPM |
| Needs | **Rotation** and **Liquid Oxygen** |
| Internal tank | 1 000 mB, accepts only Liquid Oxygen |
| Pipe connections | Any face except the face it points at and the two faces on its shaft axis |

The sealer looks out of its **front face**; the room is whatever empty space is **directly in front of that face**. If nothing happens when you start it, check that the sealer is facing into the room (try placing it from the other side).

## Setting up a room

1. Build a room with solid walls, floor and ceiling.
2. Place the sealer so its front faces **into** the room.
3. Pipe **Liquid Oxygen** into one of its connection faces.
4. Spin it with a shaft.
5. The room is detected automatically. You can also **right-click the sealer with an empty hand** to make it (re)scan right away.
6. Look at the sealer with **Engineer's Goggles**: the tooltip shows **Sealed** or **Open**, and the oxygen concentration (labelled `mb/m3`; the room is breathable above 10).

When the room is sealed and filled, anyone inside is in "oxygen". When you remove the sealer, its room is removed too.

## How the room is worked out

The mod does a flood-fill from the block in front of the sealer. It follows the same "can air pass here?" test as Create's encased fans:

- A **full solid block** stops air.
- Anything with **gaps** in its collision shape can let air through. Blocks that Create's fans pass straight through always leak: **iron bars, fences, copper grates, campfires, blaze burners, copycat bases, mangrove roots, sail frames and leaves**. Non-full blocks like slabs may leak sideways, and the mod's own code comments say stairs are not handled well.
- **Unloaded chunks** count as solid, so the search will never force a chunk to load.

A room is **Sealed** only if the flood-fill finishes by running out of space, and **Open** if it leaks or if it is too big. If a room is open, its oxygen is reset to **zero** every tick, so a single hole means no air at all.

**Size limit:** 1 000 blocks of volume per sealer by default. Every extra sealer that touches the room adds another 1 000. Larger rooms are declared open. (Server config `maxSizePerSealer`.)

**Rescans:** if you place or break blocks next to the room's boundary, the room re-scans itself within a few ticks. Big rooms take a few ticks to finish (up to 1 000 blocks per tick; server config `maxBlockPerTick`), so a freshly changed room may flicker for a moment.

### Seeing the room

Turn on the client option `oxygenRoomDebugMode` (see [Configuration](Configuration.md#client-config)) to draw the shape the mod has found. It is a great way to find a leak: the room's outline will include the gap.

## How the oxygen works

Rooms track a number of **oxygen units**.

| Event | Effect |
|---|---|
| The sealer spins with fluid | Every half second (10 ticks) it takes **RPM** millibuckets of Liquid Oxygen from its tank and adds **10 units per mB** to the room. |
| A living creature is in the room | Takes **10 units per tick** (default). Checked every 5 ticks. |
| A leaf block that the room scan has registered | Adds **2 units per tick** each (default). See the note below. |
| Room volume V | Holds at most **100 × V** units. |
| Breathable? | Closed room and **more than 10 units per block of volume**. |

So a room needs only a little oxygen to become breathable: a 100-block room is breathable with 1 000+ units, which is just 100 mB of Liquid Oxygen.

### How much Liquid Oxygen does it cost?

- **Filling:** about 1 mB of Liquid Oxygen per block of volume to reach the breathable threshold, and 10 mB per block to fill the room completely.
- **Upkeep:** each creature breathes **200 units per second**, which is 20 mB of Liquid Oxygen per second per creature, with defaults. Five creatures use 100 mB/s.
- **Leaves** can offset some of that. Each registered leaf block makes 40 units per second. The scan registers leaves it runs into while outlining irregular spaces (for example the boundary of a tree canopy inside the room), not necessarily every leaf, so treat leaves as a bonus rather than a precisely countable supply.

> [!WARNING]
> The sealer takes **RPM** mB per half-second whenever it spins and has fluid, even if the room is already full, and the excess is lost. A sealer spun at 256 RPM burns through 512 mB of Liquid Oxygen every second. Run it **slowly**: a few RPM per creature is plenty. You can stop it once the room is full; the stored oxygen does not leak out of a sealed room.

Once the room is filled, you can stop the sealer. The oxygen stays in the room, and only falls as creatures breathe it. When it drops below the threshold, the room is no longer breathable.

## Common questions

**Do I need a sealer for every room?** Yes, a sealer is what creates a room (and a room can have several sealers to raise its size limit). Rooms with no sealer have no oxygen.

**Can mobs breathe in the room?** Yes. Everything alive inside uses oxygen and is protected.

**Does gravity change in a room?** No. A room in orbit is still weightless. See [Planets and Travel](Planets-and-Travel.md#gravity).

**What about Venus' fire rules?** They do not apply to a player standing in a working pressurised room; see [Venus](Venus.md#fire).
