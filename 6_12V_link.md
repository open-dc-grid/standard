# 12V Link

::: warning In Progress
This chapter is incomplete - still being written/defined.
:::

This section addresses the electrical and communications properties of an Open DC Grid (ODG) link
implemented as a DC bus with a nominal voltage of 12V. The ODG 12V Link includes a communications capability
based on the LIN Bus using a third signal wire besides the two power poles. Communications is required to be
provided by all conforming power sources but optional for loads such as appliances.

A bus connection means that multiple devices
are electrically connected via wires and will observe roughly the same electrical potential
though the actual observed potential may differ between devices due to resistive drops on the wires.

The actual wiring may be in a variety of topological configurations such as:

- point to point - two ports connect with a single link
- star where all drops are connected at a single point
- linear configuration with multiple taps branching from a distribution
- tree-like configuration with multiple branch points fanning out into a web of connections.

All conforming ODG 12V link devices must implement a sleep mode that reduces its current
consumption when the supplied voltage drops below a defined threshold to avoid
draining battery sources to unhealthy levels. In sleep mode, the communications
and management circuits are expected to operate normally. 
At a still lower voltage device are expected to go into a deeper form
of sleep referred to here as disconnect mode that consumes negligible
power to protect the power. When normal voltages are restored, devices shall
resume normal operation without user intervention.

The ODG 12V Link is defined for interoperability with most existing 12V appliances and power sources.
Most existing 12V appliances can be attached to an ODG conforming power source and will operate as expected.
In this section, such devices will be referred to as legacy devices.
Physical connectivity can be implemented with a passive adapter that matches the legacy device's connector
to the connector specified here. 
Similarly, ODG 12V Link conforming appliances and other loads will operate as expected 
except for communications when attached to existing 12V
power sources such as a 12V battery or automobile auxiliary power connector using a
passive adapter.

Devices conforming to the ODG 12V Link allow consumers to attach appliances to power sources and be
confident that their appliance will operate as expected but also have additional benefits for consumers and resellers.
The ODG 12V Link contains features such as polarity
protection that make it goof resistant when attached using ad-hoc wiring. 
When implemented by appliances, the optional communications capability enables many functions such as 
power allocation, remote control, management and PAYG.
Multiple conforming sources can be attached to a single 12V bus with default or
configuration-specific power allocation.

Low voltage DC connectivity has long been challenged by conflicting definitions
for the commonly used coaxial connectors, often referred to as barrel connectors.
The ODG 12V Link uses such a connector. It attempts to mitigate the risk of
conflicting definitions by selecting a connector that is less commonly
used except for the specific case of laptop AC power adapters and
this standard contains provisions that specifically permit such adapters
to be attached to conforming appliances. Such appliances will operate
as expected when attached to an AC power adapter so long as the adapter
can supply sufficient current and will fail gracefully when the adapter
cannot supply enough current.

The ODG 12V Link also provides compatibility to the ISO 16750 standard for automotive
electric devices in that devices conforming to the ISO standard will operate
when connected to an ODG power source and ODG conforming appliances will
operate when connected to an ISO power source. Most of the ISO test requirements
also apply to ODG 12V Link conforming devices but some extreme requirements
specific to the automotive environment are not required of ODG 12V Link devices.

## Port Types

As defined the the architecture section, this standard defines a port as
an electrical interface to a device with specified characteristics.
The ODG 12V link defines four types of ports:

- Load ports only consume power such as the port on an appliance
- Source ports only supply power
- Bidirectional ports can consume or supply power like a battery 
- AC adapter ports are a special kind of source port with reduced functionality

In the simplest configuration, a load port is attached to a source port with a cable.
More complex combinations are possible such as a source that powers multiple loads
or an arbitrary collection of load, source and bidirectional ports attached to
a common bus. AC adapter ports can only attach to a single load port or
a bidirectional port with the optional capability to support AC adapters.

## Connectors - Plugs and Sockets

The ODG 12V Link is based on a standard coaxial (barrel) connector currently used on many laptop AC power adapters:

- 7.5 mm outside diameter
- 5.0 mm inside diameter
- 3 pole

This connector is wired with the negative pole on the outer surface, the positive pole on the inner surface.
The center pin is used for data communications.

Source ports and bidirectional ports always use a female socket. 
Load ports are recommended to also use a female socket assuming a detachable male plug-to-plug cable
but they may optionally use a hardwired cable with a male plug.
Use of the female socket on load ports is recommended so they can be powered by existing
AC power adapters that come with hardwired male plugs on a cable. 
AC adapter ports are assumed to always have a male plug on a cable.

## Electrical Requirements

This section defines the electrical requirements of the ODG 12V Link which can vary by type of port. 
The following table of symbols applies to all parts of this section:

| Symbol | Value | Description |
|--------|:-----:|-------------|
| V<sub>max_s</sub> | 15 V | maximum source voltage |
| V<sub>max_l</sub> | 20 V | maximum voltage for loads operating normally |
| V<sub>max_a</sub> | 20 V | maximum AC adapter voltage |
| V<sub>ovp</sub>   | 25 V | minimum overvoltage protection |
| V<sub>ovs</sub>   | 25 V | source disconnect overshoot |
| V<sub>cond</sub>  | 25 V | load disconnect overshoot |
| V<sub>min_s</sub> | 10.5 V | minimum source voltage |
| V<sub>min_l</sub> | 10 V | minimum voltage for loads operating normally |
| V<sub>min_c</sub> | 9 V | minimum voltage for communications circuits |
| V<sub>reverse</sub> | -25 V | minimum reverse protected voltage |
| I<sub>max</sub> | 8 A | maximum current through a connector |
| I<sub>sleep</sub> | 10 mA | maximum load current in sleep mode |
| I<sub>disconnect</sub> | 1 mA | maximum load current in disconnect mode |


### Voltage and Over-voltage Protection

Source ports and bidirectional ports sourcing power shall supply power with the voltage in the range V<sub>min_s</sub> to V<sub>max_s</sub>,
as measured on the source connector. The source shall supply at least V<sub>min_s</sub> when sourcing its maximum rated power.
Load ports shall operate normally when receiving power whose voltage is in the range of V<sub>min_l</sub> to V<sub>max_l</sub> 
as measured on the load connector or plug.
AC adapter ports are permitted to source power with the voltage in the range V<sub>min_s</sub> to V<sub>max_a</sub> as measured at their plug.

Loads are expected to operate normally over a wider range than source ports normally supply
to let them operate with 19.5 V-style AC power adapters and, at the low end, to accommodate an IR voltage
drop between the source and the load. 
The normal source upper voltage limit is constrained to a lower voltage than V<sub>max_a</sub> to prevent 
damage to legacy devices attached to an ODG bus.

All load ports and bidirectional ports receiving power are expected reduce their current draw
and go into sleep mode when the received voltage drops below V<sub>min_l</sub>.
This standard makes a distinction between the communications circuits of a device and circuits related to its primary function.
The communications circuits are expected to operate at a lower voltage than the primary circuits
so they can report an under-voltage condition even when the primary function cannot be performed.
If implemented on a device, communications circuits are expected to operate normally when the received
voltage is in the range V<sub>min_c</sub> to V<sub>max_l</sub>. When receiving less than V<sub>min_c</sub>,
devices shall enter disconnect mode and draw negligible current.

All ports except AC adapter ports shall implement over-voltage protection.
The required protection level is defined by a series of tests given in Appendix TBD
that include stress pulses of various voltage peaks, durations and repetitions.

Source ports and bidirectional ports operating as sources shall limit the voltage overshoot to less than V<sub>ovs</sub>
when a load is disconnected. Test conditions are given in Appendix TBD and require the disconnect
of the maximum rated load for the port.

Load ports and bidirectional ports receiving power shall limit conducted emissions
to voltages less than V<sub>cond</sub>. This is normally only relevant to inductive loads.
Test conditions are given in Appendix C.

### Current and Over-current Protection

The maximum current supplied by a source or bidirectional port, or consumed by a load 
through a connector shall be I<sub>max</sub>.
A source or bidirectional port is not required to provide any minimum level of current. 

A device in sleep mode shall reduce its current consumption to I<sub>sleep</sub> or less.
A device in disconnect mode shall reduce its current consumption to I<sub>disconnect</sub> or less.

Devices requiring current in excess of I<sub>max</sub> may exceed these current limits 
if they provide alternate means of connection such as screw terminals. Such devices
shall conform to all voltage requirements and shall describe their wiring requirements
in their documentation. They shall provide over-current protection suitable to protect
the wiring and connections as described in their documentation. They shall also
implement the sleep mode and disconnect mode current limits.

All devices supplying power through a source or bidirectional port shall implement communications over those ports.
Devices offering non-standard connections such as screw terminals shall include terminals
for communications that is electrically compatible with the communications signaling.

Note that a bus can have more than one power source so the total current available may be more than I<sub>max</sub>.
Installations shall be configured for a maximum of I<sub>max</sub> from all sources if they use standard wiring.
If an installation is configured to supply more than I<sub>max</sub> on a single bus, 
it shall use wiring capable of supporting the maximum current for which the installation is configured. 

A port sourcing power shall include over-current protection to prevent damage to the device in the event
of a fault that shorts the positive pole to the negative pole for an unlimited time period.
The over-current protection from a source or bidirectional port shall automatically
reset so the device resumes normal operation when the fault is resolved.
An over-current condition shall be reported using communications as described in section TBD.

[ Must resume normal operations in TBD seconds. How is resume initiated? ]

[ The over-current condition shall be reported by an LED located near the connector as described in TBD. ???]

If a load device supports communications, it shall report the maximum normal operating current
of the device at the minimum supply voltage and shall also report the limit and duration of any
temporary current surges the device may experience such as those related to motor starts, using
the protocols described in TBD.

A load port is recommended but not required to provide over-current protection from faults internal
to the device that would result in current draws in excess of its rated maximum. Over-current
protection for a load may be implemented with a fuse. A replaceable fuse is recommended
but not required. If the device supports communications, it is recommended that the communications
be implemented such that communications remain operating even when the primary over-current protection
has disabled the device so the device may report the fault condition.

The maximum current of an AC adapter port is not defined by this standard.

The communications protocol is defined to have an inherent maximum current of TBD A
by sourcing current through a TBD ohm pull-up resistors.
For more details, see section TBD.
A fault that shorts the communications pin to either pole will disable communications
but not have any permanent effect on the device such that communications will resume
normal operation when the fault is resolved.

[ A load device is recommended but not required to report an over-current fault via
and LED located near the port as described in section TBD. ??? ]

[ Should we permit temporary current overloads in excess of 8 A? ]

[ Motor start overloads ?? ]

[ Capacitor overloads ?? ]

### Reverse Polarity Protection

All ports shall implement reverse polarity protection so that the device is not damaged
when connected to a voltage source of V<sub>reverse</sub> for an indefinite period.

If a port supports communications, recommended that the communications logic
be powered by a full-bridge rectifier so that it will continue to operate
with the power poles reversed and can report the fault using the methods
described in section TBD.

It is recommended [ Required?? ] that all devices implement an LED that will
illuminate red with the power poles are reversed.

### Drop-out Protection

[TBD]

### Galvanic Isolation

When multiple devices are powered by a single 12V Link, they may observe different voltage levels on each pole
relative to the source reference. Devices are typically implemented to use the negative pole as a signal ground
reference and therefor differences between the negative poles on each device may result in differing
signal ground references in each device. If these devices are connected together with another cable
besides the 12V Link power cable such as a USB communications cable that connects the grounds, 
unexpected current may flow through the ground connections. This condition is commonly referred
to as a ground loop. The ground loop will result in noise that disrupts the communications
signals and in extreme cases may result in damage to the equipment.

[Need illustration]

To avoid this problem, when any two devices powered by a signal 12V Link are connected 
with another cable, at least one of them must use a galvanic isolator on its power cable. 
This is a device that electrically isolates the power poles across the device so that
the down stream side is electrically floating relative to their common reference.
This isolation breaks the ground loop and solves the problem.

[Need illustration]

### Cold Start

[TBD]

### Port Labeling

[TBD]

### Communications

### 1-Wire Communications


