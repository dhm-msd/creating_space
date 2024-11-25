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


