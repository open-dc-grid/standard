# Annex A: Wiring Recommendations

::: warning In Progress
This chapter is incomplete - still being written/defined.
:::
[Informative]

This makes recommendations for wiring devices in an Open DC Grid. These recommendations are not
formally part of the standard.

::: warning ToDo
Incorporate parts of P2030.10.
:::

 ## Critical Use Cases

 To be checked against the grid standard.

### Separate ground path via audio or USB connection

Phone connected to one nanogrid controller, sound system to another. An audio / USB cable connects both devices.

### Multiple inverters connected in different locations to public grid

Are inverters always galvanically isolated? If not, does it create issues in the grid?

### Different grounding of connected existing SHS

Typical PWM charge controllers are grounded at positive terminal (if grounded at all). MPPT charge controllers might be grounded at negative terminal. What happens if batteries of both of these systems are connected to the nanogrid?
