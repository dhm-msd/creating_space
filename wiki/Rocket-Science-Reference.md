# Rocket Science Reference

This page explains what the game computes when your rocket launches, so you can plan a design on paper. For the buttons and procedure, see [Launching and Flight](Launching-and-Flight.md).

## The quantities

| Quantity | Symbol | Unit | Where it comes from |
|---|---|---|---|
| Thrust | F | N | Sum of every engine's thrust |
| Dry mass | m_dry | kg | All blocks (1 000 kg each unless listed; see [Building a Rocket](Building-a-Rocket.md#mass-what-your-rocket-weighs)), plus engine masses, plus non-propellant fluids in the tanks |
| Propellant mass | m_prop | kg | Fluid in the tanks that the engines burn, at its density |
| Wet mass | m₀ | kg | m_dry + m_prop |
| Gravity | g | m/s² | The world you launch from; see [Planets and Travel](Planets-and-Travel.md#gravity) |
| Specific impulse | ISP | s | Per engine; shown on the table and the engine tooltip |
| Exhaust velocity | v_e | m/s | See below |
| Δv | Δv | m/s | What the rocket can do, and what each trip costs |

## 1. Can it lift off? (thrust versus weight)

The weight of the loaded rocket is `W = m₀ × g`, using the gravity of the world you are launching from.

> The launch is refused if **F < W**. If F equals W exactly, it passes.

At Earth's gravity (9.81 m/s²) every 100 kN of thrust lifts about 10.2 tonnes. On the Moon (1.6 m/s²) the same engine lifts about 62 tonnes.

## 2. Exhaust velocity and the ISP modifier

For each engine the mod works out a propellant mass flow:

`ṁ = F_engine ÷ (ISP × ISPModifier × 9.81)` kg/s

`ISPModifier` is a **server config option, default 1.5**. Its description is "reduction coefficient on the consumption": it makes every engine burn 1.5 times *less* propellant than its listed ISP would suggest. For your rocket as a whole:

`v_e = F_total ÷ ṁ_total`

With one engine this is just `ISP × 1.5 × 9.81`; with several, it is the thrust-weighted blend. Set `ISPModifier` to 1.0 in the config to make the numbers match the table's ISP exactly.

## 3. Δv (the rocket equation)

The Δv a rocket has is Tsiolkovsky's equation:

`Δv = v_e × ln(m₀ ÷ m_burnout)`

where `m_burnout` is the mass left when the usable propellant is gone. The trip you want has a fixed cost (see the [Δv map](Planets-and-Travel.md#delta-v-map)); the rocket can go if its Δv is at least that cost. The flight screen shows both numbers (green or red).

To find how much propellant a trip burns, the game solves the same equation backwards:

`m_prop_left = m₀ ÷ e^(Δv_trip ÷ v_e) − m_dry`

and the amount burnt is `m_prop − m_prop_left`. If `m_prop_left` is negative, you do not have enough propellant for that trip.

## Mixture ratio

Each engine burns its propellants in a fixed *mass* ratio (Metha/LOX 2 : 1, LH2/LOX 6 : 1; see [Fluids and Propellants](Fluids-and-Propellants.md#propellant-types)). The game works out what share of the total burn each propellant makes up (across all your engines) and compares it with what is loaded:

- The **limiting propellant** (the one you have the least of relative to its share) decides how much of the burn is possible.
- Any propellant beyond what the limiting one allows is **dead weight at burnout**, so it reduces your Δv rather than adding to it.
- If any propellant is short of the mass the trip needs, the launch is refused with a "wrong ratio of propellant" message.

Aim to load each propellant in its correct ratio, and a little extra of both rather than a lot of one.

## Where the fuel goes

The game calculates, for the specific trip, how many kilograms of each propellant to burn, and divides that by the number of ticks the climb will take, so that the fuel runs down smoothly and ends at the exact amount left over. The rocket's weight used for acceleration is the **launch weight** and does not drop during the burn.

## Climb speed

```
a = F ÷ m₀ − g                         (m/s², the "net acceleration")
speed = sign(a) × ln(1.4 + |a| ÷ 20)   (blocks per tick, limited to ±1)
```

- Positive a: it climbs. Even a very small positive a gives about 0.34 blocks per tick (6.7 blocks/s), because `ln(1.4)` is about 0.34.
- The maximum is 1 block per tick (20 blocks/s), reached when a is about 26.4 m/s² or more.
- If `a` is exactly zero the rocket does not move.
- The climb takes roughly `(300 − Y_start) ÷ speed` ticks.

The speed is recalculated every tick from the formula above using the launch mass, so there is no gradual build-up of speed.

### Descent

When the rocket arrives on a planet it falls with `a = −g` of the *arrival* world (no thrust, no propellant), so the speed is `ln(1.4 + g ÷ 20)` blocks per tick: 0.64 on the Earth (12.7 blocks/s), 0.39 on the Moon (7.8), 0.46 on Mars (9.2) and 0.61 on Venus (12.2).

## Worked example

A small first rocket using the engine from [Engine Crafting](Engine-Crafting.md): Brass, Open Cycle, Bell Nozzle, 100 kN, ISP 289 s, mass 3 020 kg.

**Parts (dry mass):**

| Part | Mass |
|---|---|
| Rocket Engine | 3 020 kg |
| Its nozzle block (engine structure) | 1 000 kg (default data) |
| Rocket Controls | 1 000 kg |
| One Create Seat | 1 000 kg |
| Two Create fluid tank blocks | 2 × 40 = 80 kg |
| **Dry mass** | **6 100 kg** |

**Propellant:** 2 500 mB methane (1 250 kg) and 2 500 mB oxygen (2 500 kg) is a 1 : 2 mass ratio, as Metha/LOX wants. That gives 3 750 kg.

**Checks:**

- m₀ = 6 100 + 3 750 = 9 850 kg. Weight = 9 850 × 9.81 = 96.6 kN. Thrust 100 kN ≥ 96.6 kN ✓ (only just).
- v_e = 289 × 1.5 × 9.81 = 4 253 m/s.
- Δv = 4 253 × ln(9 850 ÷ 6 100) = **2 038 m/s**. The Earth → Earth Orbit trip costs 1 500 m/s, so ✓.
- Propellant burnt for 1 500 m/s: 9 850 ÷ e^(1500 ÷ 4253) − 6 100 = 822 kg are left over, so 2 928 kg are burnt (1 952 kg oxygen and 976 kg methane); both are below what is loaded ✓.
- Net acceleration = 100 000 ÷ 9 850 − 9.81 = 0.34 m/s², climb speed about 0.35 blocks/tick (7 blocks/s). From Y 64 to Y 300 takes about 34 seconds.

This works, but with no margin: one extra tonne would make the thrust smaller than the weight and the launch would be refused. To get more room, build a second engine, shed dry mass, or redesign the engine for more thrust (a bigger chamber costs extra tonnes, so the trade-off is real).
