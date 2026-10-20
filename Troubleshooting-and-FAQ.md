# Troubleshooting and FAQ

## My rocket won't assemble

Press **Create New Rocket** and nothing happens? Assembly failed, and the reason is stored on the Rocket Controls. Wear **Engineer's Goggles** and look at the controls: Create shows the assembly error as a tooltip.

Common causes:

- **The structure is too big.** Create limits contraptions (default 2 048 blocks).
- **The Rocket Controls is not connected to the rest of the build.** Assembly starts from the controls and only collects what is attached to it (glue, chassis or other Create attachments).
- Any other reason Create gives for refusing a contraption.

## My rocket assembled but won't launch

Work down this list:

1. **Is it paused?** A new schedule starts paused. Click the pause button so its indicator goes out, then close the screen. See [Launching and Flight](Launching-and-Flight.md).
2. **Is there a destination entry?** And is it a *different* world from the one you are in?
3. **Is the screen's ΔV box green?** Red means the propellant on board is not enough for that trip.
4. **Is thrust at least the weight?** Use a [Flight Recorder](Machines.md#flight-recorder) or the numbers on [Rocket Science Reference](Rocket-Science-Reference.md). Remember every block weighs a tonne by default, and each engine adds a tonne for its nozzle block.
5. **Is the rocket below Y 300?** A rocket at or above Y 300 can't take off.
6. **Is the sky clear?** Any block directly above the rocket stops it (collision).

If it still does nothing, read the Flight Recorder (below). After you fix the problem, open the rocket screen and close it again to send the schedule once more.

## Reading the Flight Recorder

Right-click the Flight Recorder on the assembled rocket (or look at it through Engineer's Goggles once the rocket has been disassembled). It tells you about the **last launch attempt**:

| Message | Meaning | Fix |
|---|---|---|
| *No past flight* | The rocket hasn't tried to launch since it was assembled. | Start the schedule. |
| *No failure* | The last attempt passed all checks. | n/a |
| *Not enough propellant* | There is less propellant in total than the trip needs. It also lists each fluid as `loaded / needed`. | Add more propellant, or carry less dry mass. |
| *Wrong ratio of propellant* | There is enough in total, but at least one fluid is short of what the burn needs (or missing). It lists each fluid as `loaded / needed`. Green means enough, red means short. | Top up the short fluid. |
| *Not enough thrust* | Shows "Thrust" and "Weight" in newtons; thrust is lower than weight. | Add engines, use bigger engines, or lighten the rocket. |

**Sneak + right-click** gives a live readout: the empty mass (with the dry-mass and inert-fluid parts), the **mean Isp** (this already includes the ISP modifier, so it reads 1.5× the table's ISP by default), the propellant mass and the computed **Δv**. Compare that Δv with the trip's cost.

You can switch the fluid amounts between volume and mass in the [common config](Configuration.md#common-config).

## The rocket stopped in mid-air

It hit something. Possible causes:

- A block above it (a roof, a mountain, another builder's tower).
- The **world ceiling**. The world is 320 blocks tall and the rocket switches world when the Controls pass Y 300, so if a lot of the rocket extends above the Controls, its top reaches the ceiling first. Keep the part above the Controls short. See [Building a Rocket](Building-a-Rocket.md#getting-the-height-right).

Open the rocket screen and press **Disassemble** to recover your blocks.

## I'm taking damage in space

The check is once per second, and it is purely about your **gear** and **biome**:

- Do you wear **all four pieces** (helmet, backtank in the chest slot, leggings, boots) from the spacesuit set? Missing one means no protection.
- Does the **backtank still have oxygen**? An empty backtank protects nothing.
- On Venus, the extra "overheating" damage is also stopped by a working suit. See [Life Support](Life-Support.md).

## My oxygen room doesn't work

- Look at the sealer with Engineer's Goggles. **Open** means there is a leak or the room is too big.
- Turn on `oxygenRoomDebugMode` in the client config to see the room's outline; the leak is where the outline pokes through.
- Remember that **iron bars, fences, leaves, copper grates, campfires and non-full blocks** let air through. See [Oxygen Sealer](Oxygen-Sealer.md#how-the-room-is-worked-out).
- Is the sealer **spinning** and does it have **Liquid Oxygen**? It needs both.
- Is the room within the **1 000-block** limit?

## The backtank won't fill

- Place the backtank as a block first (use the item on the ground); you can't fill it while wearing it.
- Connect the pipe to the **bottom face**.
- Only **Liquid Oxygen** is accepted.

## The Engineer Table's check mark does nothing

- The pressure readout (`n / m bar`) must have `n ≤ m`. Raise the material, enlarge the chamber, or lower the thrust.
- The output slot must be empty. Take the previous blueprint out.

## Machines

**Air Liquefier makes nothing.** It only works in the **Overworld** with **air** (oxygen) or a **campfire** (CO₂) directly in front of it, its output tanks must have room, and it needs rotation.

**Methane synthesis doesn't start.** It needs a **heated** basin (lit Blaze Burner), Liquid CO₂ and Liquid Hydrogen in the basin, the Catalyst Carrier with **one empty block of air between it and the basin**, rotation, and an **empty catalyst slot**.

**Mechanical Electrolyzer or Catalyst Carrier can't be placed.** They cannot sit directly on top of a Basin; leave one block of space, as with the Mechanical Mixer.

## FAQ

**How long is a flight?** The rocket climbs at between 6.7 and 20 blocks per second, so most launches from the surface take roughly 10 to 40 seconds. See [Launching and Flight](Launching-and-Flight.md#speed).

**Do I need fuel to land?** No. Descent uses no propellant, but you can't steer and it won't brake. The rocket stops when it touches something.

**Can I refuel a rocket mid-trip?** Break the trip into entries. After each arrival the schedule runs the entry's wait conditions, which can include *Fluid Threshold*, *Item Threshold* and *Idle Inventory*, so you can have the rocket wait while something loads or refuels it.

**Why does everything weigh so much?** Every block is 1 000 kg unless the mass table says otherwise. See [Building a Rocket](Building-a-Rocket.md#mass-what-your-rocket-weighs).

**Can I move my designs to another world or player?** Designs are stored per player in each world. Give a Design Blueprint to another player to teach them. Operators can use `/creatingspace addAllDesigns`.

**Is there a Ponder?** Yes. Hold **W** over a Rocket Controls, a Rocket Engine, or a Flight Recorder to see the "Rockets building" and "Rockets debugging" scenes. They are simplified.

**Does it work with Ad Astra?** The mod includes language entries for Ad Astra dimension names and leaves gravity alone in the `ad_astra` and `ad_extendra` namespaces. It does not add Ad Astra planets to its travel network by itself.

**Where do I report problems?** [GitHub issues](https://github.com/RealAntEngineer/creating_space/issues), or the community [Discord](https://discord.gg/Dn9DhTqarH).
