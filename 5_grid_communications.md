# Grid Communications

::: warning In Progress
This chapter is incomplete - still being written/defined.
:::

This section addresses communications between nodes that are independent of any particular link implementation
and any particular communications implementation. This does not necessarily imply a particular level in
the usual protocol stack. In some cases, high level functionality can be mapped to low level protocols.

## Energy Transfer

Pricing based energy transfer between nodes with storage.

## Device Monitoring and Management

Enumerate devices
Report voltages and currents
Report battery status

## PAYGO

TBD


## General ideas

- Basic system control works without any higher-level communication, only based on measured grid voltage
- Energy management and higher level control (incl. monitoring) should use a protocol independent of the lower layers. So it should allow both wired (e.g. CAN, RS485) as well as radio (GSM, LoRa, WiFi, etc.) transfer methods.

