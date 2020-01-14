# Control

The main system level functions of the DC grid are:

- Current routing (wired connection between devices including switches and fuses)
- DC voltage control (e.g. for battery charging)
- Supervisory control for energy management and monitoring

## Current routing

Compared to conventional grids, where the energy flow is mostly uni-directional from the energy source to the consumer, the DC grid can operate in both directions. A battery for example can be a current source or a current sink. This requires advanced concepts for protection againgst overcurrent in parts of the system.

Traditional protection schemes for cables using a fuse at each energy source or at points where the cross-section changes don't work anymore for bi-directional current flow.

The suggested approach for the DC grid allows control of the current flow using semiconductor switches. These smart switches detect fault situations like overload or short circuits and automatically disconnect parts of the grid for protection.

## Voltage droop control

Using a DC/DC converter between all energy sources and the DC bus allows an independent control of the DC bus voltage.

The DC bus voltage is a measure for the system state and can be used for basic communication (e.g. a high voltage level means lots of available excess renewable energy in the system).

Load prioritization via different disconnect set-points is possible.

::: warning ToDo
Add voltage levels as defined in ISO 21780 and IEEE P2030.10 draft
:::

### Converter stability

::: warning ToDo
Add paragraph from James Gula
:::
