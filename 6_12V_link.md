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

The ODG 12V Link supports communications between devices attached to the bus
through a variation of the LIN Bus used for low-speed communications in automobiles.
This communications interface is optional for load devices but required for
power sources except for AC adapters. These communications are used to
manage a bus with more than one power source,
implement priority allocation of power to loads, and for the remote management
of appliances or other loads that choose to implement it including PAYG.
The communications system includes the concept of a functional bus manager
but this function is not restricted to a particular physical device
as with a typical LIN Bus and can potentially be shifted between devices
as needed when devices are attached or removed from the bus.
While capable of general purpose messages, this communication system is intended
primarily for bus management and should not be considered a substitute
for high speed communications through WiFi or other technologies.
Communications details are provided in the following sections. 

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
| V<sub>AC</sub> | 1 V P-P | minimum AC noise protection |
| V<sub>dropout</sub> | 4.5 V | maximum voltage during drop-out protection test |
| I<sub>max</sub> | 8 A | maximum current through a connector |
| I<sub>sleep</sub> | 10 mA | maximum load current in sleep mode |
| I<sub>disconnect</sub> | 100 uA | maximum load current in disconnect mode |
| f<sub>AC_min</sub> | 50 Hz | minimum frequency of AC noise test |
| f<sub>AC_max</sub> | 25 kHz | maximum frequency of AC noise test |
| t<sub>dropout</sub> | 0.1 s | time of the voltage drop-out test |
| t<sub>sleep</sub> | 5 s | maximum delay before entering sleep state |
| t<sub>LED_sleep</sub> | 5 s | period the status LED sleeps |
| t<sub>LED_delay</sub> | 60 s | delay until the LED goes to sleep  |

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

Note that devices are expected to delay entering the sleep or disconnect states to
prevent the interruption of normal operation during temporary voltage dropouts (see below).
The delay before entering a sleep state must be at least t<sub>dropout</sub> but no
longer than t<sub>sleep</sub>. 

All ports except AC adapter ports shall implement sustained over-voltage protection to V<sub>ovp</sub>.
This protection applies to both negative and positive poles as well as the communications signal.
During the over-voltage, the device is not required to maintain normal operation (Functional Status 1),
but may enter a less functional state (Functional Status 3). When the voltage returns to normal
limits the device must resume normal operation (Functional Status 1) with no intervention by the user.
Details of the required conformance test are given in Appendix C.
that include stress pulses of various voltage peaks, durations and repetitions.

Source ports and bidirectional ports operating as sources shall limit the voltage overshoot to less than V<sub>ovs</sub>
when a load is disconnected. Test conditions are given in Appendix C and require the disconnect
of the maximum rated load for the port.

Load ports and bidirectional ports receiving power shall limit conducted emissions
to voltages less than V<sub>cond</sub>. This is normally only relevant to inductive loads.
Test conditions are given in Appendix C.

### Current

The maximum current supplied by a source or bidirectional port, or consumed by a load 
through a connector shall be I<sub>max</sub>.
A source or bidirectional port is not required to provide any minimum level of current. 

A device in sleep mode shall reduce its current consumption to I<sub>sleep</sub> or less.
A device in disconnect mode shall reduce its current consumption to I<sub>disconnect</sub> or less.

Devices requiring current in excess of I<sub>max</sub> 
or sources providing more current may exceed these current limits 
if they provide alternate means of connection such as screw terminals. Such devices
shall conform to all voltage requirements and shall describe their wiring requirements
in their documentation. Sources shall provide over-current protection suitable to protect
the wiring and connections as described in their documentation. They shall also
implement the sleep mode and disconnect mode current limits.

All devices supplying power through a source or bidirectional port shall implement communications over those ports.
Devices offering non-standard connections such as screw terminals shall include terminals
for communications that is compatible with the connector-based communications signaling.

More than one power source can be attached to a bus. To allocate current fairly between sources, all sources
shall implemented droop control. [Details TBD.] 

Communications signaling between sources is used to limit the
the maximum current flow through the bus wiring.
All source devices shall have the capability of limiting their maximum current output
to a level designated in a configuration message from the current bus manager. 
By default, the maximum current from all sources shall be limited to I<sub>max</sub>.
The maximum current from all sources in an installation shall be configurable to
level higher than I<sub>max</sub> through appropriate management software
if a trained installer can ensure that the wiring can support the higher current.
It is the responsibility of the current bus manager (see TBD) to ensure that all power sources
are appropriately configured to the designed bus current limit.

[Should we permit non-droop control sources on a bus? A device could identify itself as either
being droop controlled or not. A not droop control source would not permit any other sources on the bus.]

The maximum current of an AC adapter port is not defined by this standard.
It is the responsibility of the load to ensure that it does not draw enough
current to damage its connector or wiring.

### Over-current Protection

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

### Grid Overload and Fault Isolation

Many circumstances can cause the overall power demand from loads to exceed the power available from sources.
In the simple case with a source supplying power to non-communicating loads wired to a common bus
this can manifest as an over-current condition analogous to blowing a fuse on a normal AC grid.
The source must use its normal over-current protection and disconnect current flow.

A managed grid like ODG has more options. If its sources have multiple ports that can controlled
independently, it may be able via current monitoring to isolate the overload to one port
and disconnect that port while leaving the others functioning. If the load on each
port is below I<sub>max</sub> but the aggregate exceeds the current capacity of the source,
it may choose to shut down a subset of its ports on a priority basis.

Communicating loads give the source or sources more options. Among the parameters that
a communicating load is required to supply is its normal power demand. The grid can selectively
prioritize loads using administrative configuration.

[More TBD]

### Reverse Polarity Protection

All ports shall implement reverse polarity protection so that the device is not damaged
when connected to a voltage source of V<sub>reverse</sub> for an indefinite period.
When connected with reverse polarity, the device is not expected to function (Functional Status 3)
but must resume normal operation (Functional Status 1) when correct polarity is re-applied
with no intervention by the user required.

If a port supports communications, recommended that the communications logic
be powered by a full-bridge rectifier so that it will continue to operate
with the power poles reversed and can report the fault using the methods
described in section TBD.

It is recommended [ Required?? ] that all devices implement an LED that will
illuminate red with the power poles are reversed.

### Drop-out Protection

Various conditions as when new loads are attached
may cause the bus to temporarily drop to a lower than normal voltage,
a condition known as voltage dropout.
Load devices are expected continue to operate normally (Functional Status 1)
during voltage dropouts. During the test to verify the device,
voltage is lowered to V<sub>dropout</sub> for a period t<sub>dropout</sub>
and then return to normal.
Details of the conformance test are given in Appendix C.

### Noise Immunity

Load devices are expected normally (Functional Status 1) when an AC voltage of V<sub>AC</sub> is superimposed
on their normal supply voltage. This AC voltage can be any frequency between f<sub>AC_min</sub>
and f<sub>AC_max</sub>. Details of the conformance test are given in Appendix C.

### Slow Rise and Fall of Supply Voltage

Load devices are expected to transition through levels of function when the voltage they
receive increase or decrease slowly as might be expected from a battery charging or discharging.
From 0 volts to V<sub>min_c</sub>, the device is expected to be in the disconnect state
drawing negligible current. It may have no apparent function. From V<sub>min_c</sub> to V<sub>min_l</sub>
it should be in the sleep state such that communications is operating normally (Functional Status 1)
but the devices primary function may not be available (Functional Status 3). It must enter
normal operation (Functional Status 1) when the voltage enters the normal operating range of V<sub>min_l</sub>
to V<sub>max_l</sub>. The reverse sequence must occur when the supply voltage begins to decrease.
As part of its drop-out protection the device is may delay changing to a higher functional
for a period no more than V<sub>dropout</sub>. While the voltage is dropping, the device
must enter the sleep or disconnect state within t<sub>sleep</sub>. 
Details of the conformance test are given in Appendix C.

There is another test requiring that the device maintain the proper operational state when
the supply voltage fluctuates to progressively lower level and then returns to normal
in steps with a period of t<sub>sleep</sub> or greater.  
Again, test details are provided in the appendix.

### Starting Profile

[TBD - is this test needed?]

### Transient Immunity

Various conditions may trigger brief voltage spikes that exceed the normal over-voltage protection
for brief periods. In the the automobile environment, the requirements for transient immunity are
given by ISO 7637.

[ODG requirements TBD.]

### Open Circuit

Disruptions during wiring and maintenance of a grid may cause some circuits to open in unexpected ways.
For example, the communications signal may be connected when either the positive or negative power
circuit is disconnected. The device shall be undamaged but potentially non-functional (Functional Status 3)
under all combinations of attached wiring.

A load device that implements communications but does receive the normal communications recessive signal
shall assume that it is connected to a non-standard power source. It should perform all its normal
functions. One exception is a device that implements PAYG whose payment token is expired. In this case
it should indicate this condition to users using the methods in section TBD.
 
Details of the conformance test are given in Appendix C.

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

[ Use communications to stage power on. TBD]

### Port Labeling

[ Use ODG label with separate icon for load, source or bidirectional. Power consumption or supply in Watts. TBD]

### Port Status Indicator

All devices implementing a 12V Link port shall indicate the status of that port with a multicolor LED using
the following predetermined patterns. Load devices only need a two-color LED that can display green, red
or amber (both green and red on). Source-only devices need a blue / red LED. Bidirectional ports need
an LED that includes red, blue and green. 

To minimize power consumption, the LED shall be in an awake state
or a sleep state, states that are independent of the overall device state except that the LED shall be off
and consuming no power when the device is in the disconnect state. 
In the awake state the LED is illuminated but indicating additional status details via a pulsing
pattern to repeats in a period of t<sub>LED_sleep</sub>. In the sleep state the LED is off but
awakens to display its status in a period t<sub>LED_sleep</sub>, the inverse pattern of the awake state.
The LED shall be in its awake state whenever the device transitions into its normal operating state.
The LED shall transition to its sleep state after t<sub>LED_delay</sub>, even if the device itself
is operating normally.

| Color | Blink Dots | Description |
|--------|:-----:|-------------|
| Green | 1 | load receiving normal power |
| Green | 2 | load receiving normal power but without communications |
| Amber | 1 | load or source voltage below V<sub>min_l</sub> (sleep) |
| Amber | 2 | load with insufficient priority for power |
| Amber | 3 | load or source PAYG disabled |
| Red | 1 | source over-current |
| Red | 2 | reverse polarity |
| Red | 3 | overvoltage or device malfunction |
| blue | 1 | source suppling normal power |
| blue | 2 | source suppling normal power but without communications |
  

### Communications

[LIN physical with ODGTalk link layer. Details to follow. ]

### 1-Wire Communications

[ Laptop power adapters typically include an identification ROM in the power supply that can be read by
the load using the 1-Wire protocol. Currently the content of these ROMs are all proprietary. We could
propose a standard for this content. I think a smart load could attempt 1-Wire to determine
if the source is compatible and if that fails, attempt to initiate ODG communications. ]


