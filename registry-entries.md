# Datapack registries

Creating Space adds 4 registries that can be extended with datapacks, each of them store there element in the `data/{element-namespace}/{registry-namespace}/{registry-path}/{element-path}.json` format.

## Rocket Accessible Dimensions (creatingspace:rocket_accessible_dimensions)

as the name sugest this is what controls what is a planet, the cost of travel and some gui stuff.
very important : the namespace:path correspond to the name of the dimension.

```
{
  "adjacentDimensions": {
    "random:planet": {
      "deltaV": 400 #the cost of travel
    } # you can add more if you want
  },
  "arrivalHeight": 200, #as the name suggest, the height the rocket spawn when arrivng
  "gravity": 3.71, #in comparaison to overworld which is 9.81. this is used when calculating the weight of the rocket and the gravity effect on entities
  "orbitedBody": "sun", # for client rendering
  "distanceToOrbitingBody": 2000 # for client rendering
}
```
The adjacentDimensions is derived from graph theory. See the [adjacency matrix](https://en.wikipedia.org/wiki/Adjacency_matrix) and [adjacency list](https://en.wikipedia.org/wiki/Adjacency_list) wikipedia page.



## Exhaust Pack Type (creatingspace:exhaust_pack_type)
it's used in the crafting of rocket engines

exemple : 
```
{
  "minExpansionRatio": 2,
  "maxExpansionRatio": 100,
  "allowedPropellants": [
    "creatingspace:methalox",#fluid tags
    "creatingspace:lh2lox"
  ]
}

the min and max of Expansion ratio are the one used in the rocket engineer table. Don't use values inferior or equal to 1 for the minimum. It would cause division per 0.
```

## Power Pack Type (creatingspace:power_pack_type)
it's used in the crafting of rocket engines

exemple : 
```
{
  "combustionEfficiency": 0.9,
  "numberOfPumps": 2, # don't do anything right now
  "allowedPropellants": [
    "creatingspace:methalox",#fluid tags
    "creatingspace:lh2lox"
  ]
}

the combustion efficiency is used to calculate the real ISP of the engine along with the expansion ratio.
```
## Propellant Type (creatingspace:propellant_type)

it's the property of a mix of fuels. Very important, it's the mix of liquids not the liquid in itself.

```
{
  "propellantRatio": {
    "creatingspace:liquid_oxygen": 2,
    "creatingspace:liquid_methane": 1
  },
  "maxIsp": 460,
  "Cp": 4500,
  "gamma": 1.1,
  "M": 18
}
```

The propellant ratio is used to caculate the ratio of consumption of fuels. The resource location point to a fluid tag, not a fluid. The number is normalised at reading time, so for this example it will be converted to 0.66 for liquid oxygen and 0.33 for liquid methane.

The max ISP is the maximum ISP atanable with this propellant, it's also used to calculate the temperature in the combustion chamber : it's equivalent to the enregy density of the mix.

The Cp is the thermal capacity of the burned mix, it' used to calculated the temperature in the combustion chamber.

The gamma is used .

The M is the mean molecular mass of the burned mix in g/mol.