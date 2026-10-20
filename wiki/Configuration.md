# Configuration

Creating Space registers three config files with NeoForge. The mod has no in-game config screen of its own: edit the `.toml` files (or use a config-editing mod), and restart to be sure the change is picked up.

| File | Where | Applies to |
|---|---|---|
| `creatingspace-client.toml` | `config/` | Your own game: HUD and camera options |
| `creatingspace-common.toml` | `config/` | Both sides |
| `creatingspace-server.toml` | the world's `serverconfig/` folder | Gameplay rules. On a server these decide the rules for everyone |

All values below are the defaults.

## Server config

### Rocket engines (`[rocketEngine]`)

| Key | Default | Meaning |
|---|---|---|
| `ISPModifier` | 1.5 (minimum 0.1) | "Reduction coefficient on the consumption." Every engine burns this many times less propellant than its ISP would suggest. 1.0 makes the table's ISP exact. See [Rocket Science Reference](Rocket-Science-Reference.md#2-exhaust-velocity-and-the-isp-modifier). |
| `smallRocketEngineThrust` | 98 100 | Thrust in newtons of the legacy **Small Rocket Engine**. |
| `bigRocketEngineThrust` | 4 905 000 | Thrust in newtons of the legacy **Big Rocket Engine**. |

These do not affect engines made on the Engineer Table; they carry their own thrust.

### Oxygen rooms (`[oxygenRoom]`)

| Key | Default | Meaning |
|---|---|---|
| `leaf02Prod` | 2 | Oxygen units a registered leaf block adds per tick. (The key contains a zero, "02", not the letter O.) |
| `living02Consumption` | 10 | Oxygen units a living creature uses per tick. |
| `maxSizePerSealer` | 1 000 | The biggest room (in blocks of volume) one sealer can hold. Each extra sealer touching the room adds another. Large values make scans slower. |
| `maxBlockPerTick` | 1 000 | How many blocks of a room the scan may cover each tick. High values can cause lag. |
| `smarterSearch` | false | Experimental. When on, a block change re-scans only around the changed spot instead of discarding and rebuilding the whole room. |

See [Oxygen Sealer and Pressurised Rooms](Oxygen-Sealer.md).

### Stress values

Under `[kinetics.stressValues.v3]`, with sub-sections `impact` and `capacity`. Values are **per RPM**, the same convention as Create.

| Machine | Key (under `impact`) | Default |
|---|---|---|
| Mechanical Electrolyzer | `mechanical_electrolyzer` | 1 024 |
| Air Liquefier | `air_liquefier` | 128 |
| Oxygen Sealer | `oxygen_sealer` | 8 |
| Catalyst Carrier | `catalyst_carrier` | 8 |

The `capacity` section has no entries, because the mod adds no stress sources.

## Common config

| Key | Default | Meaning |
|---|---|---|
| `additionalLogInfo` | false | Writes the rocket's trajectory calculation to the log on each launch. **Spams the console.** Useful when diagnosing a refused launch. |
| `recorder_measurement` | `VOLUMETRIC` | How the Flight Recorder and engine tooltips show propellant amounts: `VOLUMETRIC` (buckets/millibuckets) or `MASS` (tonnes). |

## Client config

### Oxygen backtank HUD (`[oxygenBacktank]`)

| Key | Default | Meaning |
|---|---|---|
| `place` | `BOTTOM_LEFT` | Which screen corner the gauge is measured from: `BOTTOM_RIGHT`, `BOTTOM_LEFT`, `TOP_RIGHT` or `TOP_LEFT`. |
| `color` | `WHITE` | Gauge colour: `WHITE`, `BLACK`, `RED`, `ORANGE`, `GREEN` or `BLUE`. |
| `xOffset`, `yOffset` | 0 | Pixels to move the gauge from its default spot. |

### Rooms (`[oxygenRoom]`)

| Key | Default | Meaning |
|---|---|---|
| `oxygenRoomDebugMode` | false | Draws the shape of oxygen rooms in the world. Handy for finding leaks. |

### Rocket (`[rocket]`)

| Key | Default | Meaning |
|---|---|---|
| `zoomOut` | 0.5 (range 0.1 to 20) | Multiplier for how far the third-person camera pulls back while you ride a rocket. |

## Settings that live in Create

Some things this mod relies on are Create's settings, not Creating Space's:

- Backtank capacity: Create's `airInBacktank` (900) and `enchantedBacktankCapacity` (300 per level).
- Fluid tank size: Create's `fluidTankCapacity` (8 buckets per block).
- Contraption size limit: Create's `maxBlocksMoved` (2 048).
