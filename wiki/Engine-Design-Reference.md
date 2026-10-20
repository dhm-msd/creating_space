# Engine Design Reference

Everything on the [Rocket Engineer Table](Rocket-Engines.md), with the exact data and formulas the mod uses. If you only want to design an engine, the table's own readouts are enough; this page is for planning ahead and for people who like the maths.

## Power packs

A power pack decides how efficiently propellant is burned.

| Power pack | Combustion efficiency | Propellants it supports | How you get it |
|---|---|---|---|
| **Open Cycle** | 0.70 | Metha/LOX | Unlocked from the start |
| **Ox Rich Flow** (oxidiser-rich staged cycle) | 0.90 | Metha/LOX, LH2/LOX | Design blueprint, found on [the Moon](Structures-and-Loot.md) |
| **Fuel Rich Flow** (fuel-rich staged cycle) | 0.90 | Metha/LOX, LH2/LOX | Design blueprint, found on the Moon |
| **Full Flow** (full-flow staged cycle) | 0.98 | Metha/LOX, LH2/LOX | Design blueprint, found on the Moon |
| **Catalyse Cycle** | 0.70 | Premixed methalox (monopropellant) | Design blueprint, found on [Mars](Structures-and-Loot.md) |

- Ox Rich and Fuel Rich currently have identical numbers. They differ in name only.
- **The Catalyse Cycle has no assembly recipe** in the current mod data, so you can unlock the design but cannot yet manufacture a power pack for it. See [Known Issues](Known-Issues-and-Unfinished-Features.md).
- The data also contains a "number of pumps" field for each pack, but nothing in the code uses it. How many turbines a pack needs is set by its assembly recipe: the Open Cycle needs one, the three staged cycles need two.

## Exhaust packs (nozzles)

| Exhaust pack | Expansion ratio range | Propellants | How you get it | Notes |
|---|---|---|---|---|
| **Bell Nozzle** | 2 – 100 | all three | Unlocked from the start | The classic nozzle. |
| **Aerospike** | 2 – 500 | all three | Design blueprint, found on the Moon | A much wider ratio range, and lighter at the same ratio (see the mass formula). |

## Propellant types

| Propellant | Mass ratio | Max ISP | Cp (J/kg·K) | γ (gamma) | Molar mass |
|---|---|---|---|---|---|
| Metha/LOX | 2 LOX : 1 methane | 460 s | 4 500 | 1.1 | 18 g/mol |
| LH2/LOX | 6 LOX : 1 hydrogen | 540 s | 3 000 | 1.2 | 10 g/mol |
| Premixed methalox | single fluid | 600 s | 4 500 | 1.1 | 18 g/mol |
| Metallic hydrogen | single fluid | 6 000 s | 18 280 | 1.3 | 2 g/mol (unusable, no pack allows it) |

More about the fluids is on [Fluids and Propellants](Fluids-and-Propellants.md).

## Materials

| Level | Material | Max pressure at 0 °C (bar) | Fails at (°C) |
|---|---|---|---|
| 0 | Andesite | 3 | 900 |
| 1 | Iron | 50 | 1 200 |
| 2 | Copper | 80 | 2 200 |
| 3 | Brass | 150 | 2 500 |
| 4 | Reinforced Copper | 250 | 2 800 |
| 5 | Copronickel | 400 | 3 200 |
| 6 | Monel | 650 | 3 800 |
| 7 | Inconel | 900 | 4 500 |
| 8 | Hastelloy | 1 200 | 5 500 |

**The rule:** at a combustion temperature *T* (in °C), a material can hold up to

> `P_max(T) = P_max(0 °C) × (1 − T ÷ T_fail)`

bar, and nothing at all once *T* reaches *T_fail*. Your design is valid when its chamber pressure is **less than or equal to** `P_max(T)`.

Allowed pressure (bar) for common temperatures:

| Material | 1 000 °C | 1 900 °C | 2 500 °C | 3 000 °C | 4 500 °C | 5 000 °C |
|---|---|---|---|---|---|---|
| Andesite | 0 | 0 | 0 | 0 | 0 | 0 |
| Iron | 8 | 0 | 0 | 0 | 0 | 0 |
| Copper | 43 | 10 | 0 | 0 | 0 | 0 |
| Brass | 90 | 36 | 0 | 0 | 0 | 0 |
| Reinforced Copper | 160 | 80 | 26 | 0 | 0 | 0 |
| Copronickel | 275 | 162 | 87 | 25 | 0 | 0 |
| Monel | 478 | 325 | 222 | 136 | 0 | 0 |
| Inconel | 700 | 520 | 400 | 300 | 0 | 0 |
| Hastelloy | 981 | 785 | 654 | 545 | 218 | 109 |

(Values rounded down to whole bar, so a value that works out to exactly a whole number may be off by one in-game.)

> [!NOTE]
> This differs from older descriptions that give a fixed "material level" from separate pressure and temperature steps. In this version the material limit is the sliding scale above.

## Formulas

All of these run live in the Engineer Table screen. Symbols: *η* is the power pack efficiency, *Isp_max* the propellant's max ISP, *Cp*, *γ* and molar mass *M* come from the propellant table, *V* is the chamber volume in cubic metres (**size in mB ÷ 1000**), *F* is the thrust in newtons, and *ε* is the expansion ratio.

1. **Combustion temperature** (°C as displayed):
   `T_c = 300 + 0.5 × (Isp_max × 9.81)² × η ÷ Cp`
2. **Gas constant:** `R_s = 8.314 ÷ (M ÷ 1000)`
3. **Exit Mach number** from the area ratio: solve numerically, for Mach from 1 to 1 000, for
   `ε = (1 ÷ Ma) × [ (2 ÷ (γ+1)) × (1 + (γ−1)/2 × Ma²) ] ^ ((γ+1) ÷ (2(γ−1)))`
4. **Exhaust temperature:** `T_e = T_c ÷ (1 + (γ−1)/2 × Ma²)`
5. **Exhaust velocity and ISP:** `v_e = Ma × √(γ × R_s × T_e)`, then `ISP = v_e ÷ 9.81`.
6. **Throat area:** `A_t = V ÷ 6`. The mod's own code comment says this assumes a characteristic length of 2 m and a chamber area three times the throat area.
7. **Chamber pressure:** `P = (F ÷ ISP) × √(T_c × R_s ÷ γ) ÷ A_t × ((γ+1)/2) ^ ((γ+1) ÷ (2(γ−1)))` in pascals, shown in bar (÷ 100 000).
8. **Engine mass (kg):** `m = (ε ÷ (ε_max − ε_min) + 1) × V × 2000`, where *ε_min* and *ε_max* are the nozzle's ratio range (Bell 2/100, Aerospike 2/500).
9. The blueprint stores *efficiency = ISP ÷ Isp_max*; the built engine's ISP is the whole number below `Isp_max × efficiency`, i.e. the ISP shown on the table (rounded down).

> [!NOTE]
> In flight, the rocket treats each engine as if its ISP were multiplied by the server config **ISPModifier** (default **1.5**). With defaults, an engine listed at 200 s behaves like a 300 s engine when working out fuel use and Δv. See [Rocket Science Reference](Rocket-Science-Reference.md).

## ISP by expansion ratio

Computed from the formulas above:

| Design | Combustion T | ε = 5 | ε = 10 | ε = 25 | ε = 50 | ε = 100 | ε = 500 (aerospike only) |
|---|---|---|---|---|---|---|---|
| Metha/LOX, Open Cycle | 1 883 °C | 224 s | 248 s | 274 s | 289 s | 303 s | 329 s |
| Metha/LOX, Ox/Fuel Rich | 2 336 °C | 250 s | 277 s | 305 s | 322 s | 338 s | 367 s |
| Metha/LOX, Full Flow | 2 517 °C | 259 s | 287 s | 316 s | 335 s | 351 s | 381 s |
| LH2/LOX, Ox/Fuel Rich | 4 509 °C | 451 s | 492 s | 531 s | 555 s | 574 s | 607 s |
| LH2/LOX, Full Flow | 4 883 °C | 470 s | 512 s | 553 s | 577 s | 597 s | 631 s |
| Premixed, Catalyse | 2 994 °C | 283 s | 313 s | 345 s | 365 s | 382 s | 415 s |

(Rounded down as the game displays them; a value may differ by 1 s from what you see because of floating-point rounding.)

## Worked examples

Chamber pressure with the **expansion ratio at 50** (pressure barely depends on the power pack, but LH₂/LOX is slightly higher):

| Propellant & pack | Thrust | Size | Pressure | Lowest material that works | Engine mass (bell) |
|---|---|---|---|---|---|
| Metha/LOX, Open Cycle | 100 kN | 1 000 mB | 30 bar | Brass | 3.0 t |
| Metha/LOX, Open Cycle | 100 kN | 5 000 mB | 6 bar | Copper | 15 t |
| Metha/LOX, Open Cycle | 600 kN | 3 000 mB | 61 bar | Reinforced Copper | 9.1 t |
| Metha/LOX, Open Cycle | 600 kN | 6 000 mB | 30 bar | Brass | 18 t |
| Metha/LOX, Full Flow | 600 kN | 6 000 mB | 30 bar | Copronickel | 18 t |
| LH2/LOX, Full Flow | 600 kN | 3 000 mB | 64 bar | Hastelloy | 9.1 t |
| LH2/LOX, Full Flow | 100 kN | 100 mB | 322 bar | None (too hot and too tight) | n/a |

Notice the trade-off: a hotter, more efficient engine needs a stronger metal for the *same* pressure, and the only way to relax the pressure is a bigger, heavier chamber.

## Engine mass versus rocket weight

Engine mass is added to your rocket's dry mass, and your thrust must exceed the weight of the whole loaded rocket. A heavy low-pressure engine and a light high-pressure engine each have their place; see [Rocket Science Reference](Rocket-Science-Reference.md) for the full flight maths.
