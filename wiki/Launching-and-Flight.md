# Launching and Flight

You have an assembled rocket (see [Building a Rocket](Building-a-Rocket.md)). This page explains how to tell it where to go, what happens during the flight, and how to land.

## The flight screen

Right-click the **Rocket Controls** on the assembled rocket. The screen that opens looks and works like Create's train schedule editor, because it is built from the same pieces. It lets you write a **schedule**: a list of *entries*, each one a destination plus optional wait conditions.

**Buttons along the bottom of the schedule**

| Button | What it does |
|---|---|
| Loop (arrows icon) | Repeat the schedule from the top after the last entry. If off, the rocket stops when it has done the last entry. |
| Pause | **A new rocket starts paused.** While the pause indicator is lit the rocket will not start any new leg. Click it so the indicator goes out to allow launching. |
| Reset progress / Skip | Choose which entry the schedule begins at. |
| Confirm (check mark) | Closes the screen. Your schedule is sent to the rocket when the screen closes, by any route. |
| **Disassemble** (separate button) | Turns the rocket back into ordinary blocks where it is. See [Disassembling](#disassembling). |

> [!IMPORTANT]
> The most common "my rocket won't launch" cause is simply the **pause** toggle. A brand-new schedule is paused. Click the pause button until its indicator is off, then close the screen.

### Entries and destinations

Click the "+" card to add an entry. In the editor you choose an **instruction type** (the only one available is **Destination**) and then:

- **The destination**, picked with the mouse wheel from the list of reachable worlds: The Earth, Earth Orbit, The Moon, Moon Orbit, Mars, Mars Orbit, Venus.
- **X and Z entry coordinates** (optional). Where in the destination world the rocket should arrive. Leave them blank to arrive above the same X/Z the rocket left from.
- A **ΔV needed** box showing the cost of that trip, in m/s. Its border is **green** when your rocket's current Δv covers it and **red** when it does not.

Pick a destination that is not the world you are in. The costs between all worlds are in [Planets and Travel](Planets-and-Travel.md).

### Wait conditions

Under each entry you can add conditions. They are checked **after the rocket has arrived** at that entry's destination, and the schedule only moves on to the next entry once they are met. They are not conditions to *start* the first leg; use the pause button for that.

Conditions in the same row run one after the other (all must be met, in order). Add a condition in a second column as an **alternative** and the rocket moves on when *either* column finishes.

| Condition | Waits until… |
|---|---|
| **Delay** | A set time has passed (ticks, seconds or minutes; default 5 seconds). |
| **Time of Day** | The in-game clock of the current world reaches a chosen time. |
| **Fluid Threshold** | The fluid in the rocket's tanks is more than / less than / exactly a number of buckets. Drop a bucket or fluid container in the filter slot to pick the fluid, or leave it empty to count any fluid. Checked about once a second. |
| **Item Threshold** | Same, for items in the rocket's storage. It can count items or full stacks. |
| **Seated Player Count** | Exactly *N* players, or *N* or more, are seated on the rocket. |
| **Idle Inventory** | Nothing has been put into or taken out of the rocket's storage (items **or** fluids) for the chosen time. Handy for "wait until loading and refuelling is done". |

(The mod's data also has a "Redstone Link" condition name, but it is switched off and cannot be chosen in this version.)

## What happens during a flight

1. **Check.** When the schedule starts a leg, the rocket works out the route and the Δv that route needs (the sum of the legs along the cheapest path; see [Planets and Travel](Planets-and-Travel.md)). It checks that:
   - thrust is at least the weight of the fully loaded rocket,
   - there is enough propellant in the right proportions for that Δv,
   - the rocket is below Y 300.

   If any check fails, the rocket does not move. Use the [Flight Recorder](Machines.md#flight-recorder) to see which one; see [Troubleshooting and FAQ](Troubleshooting-and-FAQ.md).
2. **Burn.** The engines fire (you hear "Rocket Roar" and see the plumes) and the rocket climbs straight up. It burns **only as much propellant as the trip needs**, spread evenly over the climb, not everything in the tanks. A multi-world trip is still **one burn**: the whole route's Δv is spent on this first climb, so you need enough propellant for the entire route at launch (there is no refuelling halfway unless the route is split into separate entries).
3. **Switch world.** When the rocket's Controls pass **Y 300**, the rocket, everyone aboard, and anyone standing on it are moved to the destination world at that world's arrival height (see below).
4. **Arrival.**
   - If the destination is an **orbit** (zero gravity): the rocket stops where it arrives and counts as having reached its destination.
   - If the destination is a **planet surface**: the rocket comes down **without using propellant** until it touches something, then stops. It cannot be steered on the way down, so choose your X/Z deliberately.
5. **Conditions, then the next entry**, or the end of the schedule.

Arrival heights: Earth Orbit, Moon Orbit and Mars Orbit at Y 64; The Earth at Y 200; The Moon, Mars and Venus at Y 300.

### Speed

The climb speed depends on how much your thrust exceeds your weight, not on how much you have already accelerated:

| Net acceleration (thrust ÷ mass − gravity) | Climb speed |
|---|---|
| a tiny bit more than 0 | about 0.34 blocks/tick (6.7 blocks/s) |
| 3.8 m/s² | about 0.46 blocks/tick (9.3 blocks/s) |
| 10 m/s² | about 0.64 blocks/tick (12.8 blocks/s) |
| 26.4 m/s² or more | 1 block/tick (20 blocks/s), the maximum |

So a rocket that only just beats its own weight still climbs at a steady pace; it is not slow-then-fast. The exact formulas are on [Rocket Science Reference](Rocket-Science-Reference.md#climb-speed).

The descent speed uses the same formula with gravity as the deceleration, so landing speeds are about 12.7 blocks/s on the Earth, 7.8 on the Moon, 9.2 on Mars and 12.2 on Venus.

## Disassembling

Press **Disassemble** in the flight screen to turn the rocket back into blocks at its current position. You usually do this after landing. In an **orbit** world there is no ground, so the blocks stay in mid-air: this is how you build a **space station** (see [Orbits and Space Stations](Orbits-and-Space-Stations.md)).

## Passengers

- Anyone **seated** on the rocket goes with it and stays seated through the world change.
- Anyone **standing on or inside** the rocket's bounds also gets teleported with it.
- Other entities in the rocket's space (animals, mobs, items) are carried too.
- Anyone who is *not* on the rocket stays behind.

## Example: a one-way trip to Earth orbit

1. Build and assemble a rocket as on [Building a Rocket](Building-a-Rocket.md).
2. Right-click the Rocket Controls and add one entry: **Earth Orbit**. The ΔV box should read 1 500 and be green.
3. Un-pause (click the pause button), then close the screen.
4. The rocket lifts off, switches to the Earth Orbit world at Y 64, and stops.
5. Open the screen again and press **Disassemble** to unpack your station.

To come home: build or keep a rocket in orbit, set **The Earth** as the destination (cost 200), launch, and it descends and lands at the X/Z you chose.
