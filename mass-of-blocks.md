it's the od one here being in the data/creatingspace/creatingspace_utilities/block_mass.json file.

Given that this files isn't using the minecraft API, you overides completly the existing file when use it in your datapack so you CAN'T EXTEND THE EXISTING FILE, you replace it.

default values : 

```
{
  "values": {
    "#forge:stone": 3000,
    "#forge:ores": 4000,
    "minecraft:gold_block": 19000,
    "minecraft:diamond_block": 2500,
    "minecraft:raw_gold_block": 18000,
    "minecraft:raw_copper_block": 8000,
    "minecraft:copper_block": 8600,
    "creatingspace:raw_aluminum_block": 2300,
    "creatingspace:raw_cobalt_block": 5000,
    "minecraft:iron_block": 7800,
    "create:fluid_pipe": 300,
    "create:fluid_tank": 40,
    "creatingspace:small_engine_structure": 0,
    "creatingspace:big_engine_structure": 0
  }
}
```
the numbers are in Kg
you can use block tags with #.
when a block isn't referenced here it's mass is 1000 Kg

Right now copycats have the mass of their attached block, probably will change in the future.