# Spacesuit and Oxygen Backtank

A full suit is four pieces: **helmet, backtank (chest), leggings, boots**. The rules for what a suit does are on [Life Support](Life-Support.md). This page covers making, wearing and filling one.

There are two tiers:

| Tier | Armour material | Fabric made from | Backtank made from |
|---|---|---|---|
| **Basic Spacesuit** | Create's copper armour material | Copper sheet | Red wool and **nickel plates** |
| **Advanced Spacesuit** | Netherite armour material, **fire resistant** | Netherite ingot | White wool and **aluminium plates** |

You can mix pieces from both tiers; a "full suit" only needs one valid piece in each slot.

## Crafting

### 1. Spacesuit Fabric (Create sequenced assembly)

| | Basic Spacesuit Fabric | Advanced Spacesuit Fabric |
|---|---|---|
| Start with | A Create copper sheet | A netherite ingot |
| Step 1 | Deploy a gold nugget | Deploy a cobalt nugget |
| Step 2 | Deploy red wool | Deploy white wool |
| Step 3 | Press (Mechanical Press) | Press |
| Result | Basic Spacesuit Fabric (almost always) | Advanced Spacesuit Fabric (almost always) |
| Consolation | Occasionally a gold nugget instead | Occasionally a cobalt ingot instead |

The recipe runs once. The result is picked by weight: 120 for the fabric versus 8 for the consolation item, so roughly 94 % of the time you get fabric.

### 2. Armour pieces (crafting table, `F` = the matching fabric)

| Piece | Pattern |
|---|---|
| Helmet | `FFF / FGF` where **G** = a Create **golden sheet** |
| Leggings | `FFF / F.F / F.F` |
| Boots | `F.F / F.F` |

### 3. Oxygen Backtank (Create mechanical crafting)

A 5×3 mechanical-crafting recipe (use Create's Mechanical Crafter array):

```
 .  F  .  F  .      F = matching Spacesuit Fabric
 W  T  N  T  W      W = wool (red for Basic, white for Advanced)
 .  F  W  F  .      T = Create Fluid Tank
                    N = plate (nickel for Basic, aluminium for Advanced)
```

## Wearing it

- The **backtank is the chest piece**. The helmet, leggings and boots must be worn too, or the backtank does nothing.
- A small gauge on your HUD shows the remaining oxygen. You can move it to any corner and change its colour in the [client config](Configuration.md#client-config).
- The helmet has the **Aqua Affinity** effect built in, and **breathes underwater**: when you are drowning and carry a backtank with oxygen, it burns 1 unit per second to keep you breathing, like Create's diving helmet.
- The **Advanced** pieces are fire resistant, and a full Advanced kit (helmet, backtank with oxygen, leggings and boots) makes you **immune to fire**. It also lets you swim in lava (the same trick as Create's netherite diving gear).

## Filling the backtank

You fill a backtank with **Liquid Oxygen**. Backtanks cannot be filled while worn.

1. **Place** the backtank on the ground: with it in your hand, use it on a block. It becomes a block (a "placed backtank").
2. Connect a **pipe to the bottom face** of the placed tank (the oxygen can only enter from below). Pump **Liquid Oxygen** in. 1 mB gives 1 unit.
3. The comparator output reads how full it is.
4. To pick it up again, right-click it while **not sneaking**, with **nothing in your chest armour slot** and **no block in your hand**. It goes straight onto your chest, oxygen included.

A placed backtank stores up to its full capacity. The capacity comes from Create's own backtank settings: **900 units** by default, **+300 per level of Create's Capacity enchantment** (levels I to III), which can be put on the backtank item. Mending and Unbreaking cannot.

Where do you get Liquid Oxygen? See [Fluids and Propellants](Fluids-and-Propellants.md#how-to-make-each-fluid).

## Using it

- In an airless place, a full suit consumes **1 unit per second**. A default backtank therefore lasts 15 minutes.
- You get a title-screen warning at 10 % and when it hits empty.
- Inside a [pressurised room](Oxygen-Sealer.md) the suit uses no oxygen, since you are already breathing.
