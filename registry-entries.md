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

The gamma is what determine how much of an expansion ratio you need to attain the max isp.

The M is the mean molecular mass of the burned mix in g/mol.

Has those values are not trival to ballance I suggest you use this python script to generate these values for you : 

```
import matplotlib.pyplot as plt
import numpy as np

T_i = 0  # 300
R = 8.31446261815324


def dichotomie(f, a, b, epsilon):
    try:
        if f(a) * f(b) > 0:  # On vérifie l'encadrement de la fonction
            raise Exception("Mauvais choix de a ou b.")
        else:
            m = (a + b) / 2.
            while abs(a - b) > epsilon:
                if f(m) == 0.:
                    return m
                elif f(a) * f(m) > 0:
                    a = m
                else:
                    b = m
                m = (a + b) / 2
            return m
    except:
        print("Mauvais choix de l'encadrement")
        return 0


def get_a_throat(size):
    return size / 6  # L* of 2m and chamber area 3 time the throat


def get_chamber_temperature(max_isp, c_p):
    return T_i + (get_enthalpy(max_isp)) / c_p


def get_enthalpy(max_isp):
    return 0.5 * (max_isp * 9.81) ** 2


def er_mach(gamma, expansion_ratio, mach):
    """
    based on formula for the expansion ratio : https://www.grc.nasa.gov/www/k-12/airplane/isentrop.html
    :param gamma:
    :param expansion_ratio:
    :param mach:
    :return:
    """
    return (((gamma + 1) / 2) ** (-(gamma + 1) / (2 * (gamma - 1))) * (1 + (gamma - 1) / 2 * mach ** 2)
            ** ((gamma + 1) / (2 * (gamma - 1))) / mach - expansion_ratio)


def exit_mach(expansion_ratio, gamma):
    return dichotomie(lambda mach: er_mach(gamma, expansion_ratio, mach), 1, 1000, 0.0001)


def main():
    # that's for the RS-25
    # that's the propellant
    M = 59 * 10 ** (-3)  # mass
    max_isp = 500
    gamma = 1.3
    c_p = 4009
    Pa = 10 ** 5
    thrust = 200000 * 9.81
    size = 3000 / 1000  # m3 volume of the chamber
    print("A*:" + str(get_a_throat(size)))
    Er = np.linspace(2.01, 300, 1000)
    Machs = np.array([exit_mach(er, gamma) for er in Er])
    print("T :" + str(get_chamber_temperature(max_isp, c_p)))
    Ve = get_exhaust_velocity(Machs, R / M,
                              get_exhaust_temperature(Machs, c_p,
                                                      gamma, max_isp),
                              gamma)
    Isps = Ve / 9.81
    q = thrust / Isps
    Pc = get_chamber_pressure(M, c_p, gamma, max_isp, q, size)
    Pe = Pc * (1 + (gamma - 1) / 2 * Machs ** 2) ** (-gamma / (gamma - 1))
    fig, axs = plt.subplots(2, 2)
    axs[0, 0].plot(Er, Isps, label="isp")
    axs[0, 0].legend()
    axs[0, 1].plot(Er, Machs, label="machs")
    axs[0, 1].legend()
    axs[1, 1].plot(Er, Pc / Pa, label="normalized chamber pressure", color='red')
    axs[1, 1].plot(Er, Pe / Pa, label="normalized exhaust pressure", color='green')
    axs[1, 1].legend()

    axs[1, 0].plot(Er, get_exhaust_temperature(Machs, c_p,
                                               gamma, max_isp),
                   label="exhaust temperature")
    axs[1, 0].plot(Er, np.full_like(Er, get_chamber_temperature(max_isp, c_p)),
                   label="chamber temperature")
    axs[1, 0].legend()
    plt.show()


def get_chamber_pressure(M, c_p_eau, h_gamma, h_max_isp, q, size):
    return (q * (get_chamber_temperature(h_max_isp, c_p_eau) * R / M / h_gamma) ** 0.5 / get_a_throat(size)
            * ((h_gamma + 1) / 2) ** ((h_gamma + 1) / (2 * (h_gamma - 1))))


def get_exhaust_velocity(mach, Rs, Tes, h_gamma):
    return mach * (h_gamma * Rs * Tes) ** 0.5


def get_exhaust_temperature(mach, c_p_eau, h_gamma, h_max_isp):
    return (1 + (h_gamma - 1) / 2 * mach ** 2) ** (-1) * get_chamber_temperature(h_max_isp, c_p_eau)

#main()


def calculate(max_isp, chamber_temperature, mid_efficiency_Er):
    c_p = get_enthalpy(max_isp) / chamber_temperature
    isp = max_isp / 2
    gamma = 1.3
    mach = exit_mach(mid_efficiency_Er, gamma)
    Rs = ((isp * 9.81) / (mach * (gamma * get_exhaust_temperature(mach, c_p, gamma, max_isp) ** 0.5))) ** 2
    print(Rs)
    M = (R / Rs)
    print("maxIsp : " + str(max_isp))
    print("Cp : " + str(int(c_p)))
    print("gamma : 1.3")
    print("M : " + str(int(M * 1000)))


calculate(500, 3000, 2)

```