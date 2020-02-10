# Introduction
::: warning In Progress
This chapter is incomplete - still being written/defined.
:::


## Goals and Objectives

This standard is a generic electrical interface that can be used whenever devices need to send, receive or exchange DC power.
Its focus, however, is on devices used for entry level off-grid power such as charge controllers, battery systems, DC appliances and AC inverters for attaching normal AC appliances.

This market has not developed to its full potential for multiple reasons including:

* Off-grid and weak grid electricity costs too much.

    Using the concepts of the ESMAP matrix, a more nuanced statement is that too many people can’t afford the power/energy they need to personal and productive use, at multiple power levels. Costs matter. Steady progress has been made in reducing the cost of batteries and PV panels but less progress has been in reducing the cost of other parts of the problem including intermediate electronics such as charge controllers, battery management etc. There are many reasons but low unit volumes and market fragmentation is an important one. The cost of installation and maintenance is also a growing fraction of the total service cost.

* Existing low-end solar home systems (SHSs) tend to be inflexible.

    Most low-end SHSs have fixed power levels with no capability for expansion or alternate power sources and proprietary I/O except for basic USB charging. This is an impediment to adoption because customers are reluctant to invest in technology they may soon outgrow or be made obsolete by the promise of the national grid arriving at their home “any day now…”. When electricity access fulfills its promise of improving living standards, there is a natural aspiration for additional power.

* Implementing microgrids or flexible SHSs is too complicated.

    Once people get beyond the basic, entry-level SHS, complications rapidly emerge in selecting components that will work together properly. Designing a microgrid becomes a major engineering challenge, often addressed by outsourcing to a single vendor, limiting choice and competition.

There is clearly tension between these issues. There is a cost to flexibility. All else being equal, a non-expandable SHS will cost less than an expandable one. Flexibility also adds complication. Simplicity also often involves tradeoffs that add cost.

This standard attempts to make progress on these issues by incorporating two features: compatibility and scaling. Compatibility means that devices from multiple vendors can exchange power. One could call it “plug compatibility” except that plugs aren't necessarily involved. Scalability means the ability to combine multiple devices to deliver more power to an end-point than a single device can provide.

Compatibility can reduce costs by creating a competitive marketplace of devices that can be substituted for one another. Note that in the energy access market, this is more relevant to resellers and system integrators than users as the end users more often buy a service and may not have much knowledge of the devices that render that service. Scalability can reduce costs by increasing unit volumes and reducing the expense of non-recurrent engineering.

These benefits have to overcome the higher costs implicit in a standard interface compared to an interface that is cost optimized to a specific task. This hurdle can be reduced by remaining cognizant of implementation costs in the design of the interface and not assuming that some magic chip will solve all the cost problems. There are limits to the cost benefits of scalability. All else being equal, a device designed for twice as much power will generally cost less than two devices with half the power, but then all else is never equal.

This standard directly addresses the inflexibility issue but can only do so if the resulting SHSs can ultimately be reasonably price competitive with fixed function SHSs as seen by the end user. A key part of that flexibility needs to be the ability to add AC power sources to defuse the “national grid will be here any day” barrier and AC inverters to expand the market of appliances and tools available to end users.

Likewise, the standard attacks the complexity issue by reducing the number of proprietary interfaces that must be understood. It includes enough functionality that resellers don’t have to add another layer of proprietary functionality on top of the standard to deliver their core service. Resellers can add capabilities like customer relationship software on top of the standard as long as they are built using standards-based interfaces to lower level functionality like monitoring and PAYGO key management. Scalability is important for the complexity issue too because it means resellers can build up systems adaptively without having to engineer a perfect solution at the start.

## Requirements

::: warning Temporary
This section will not be part of the final standard. It's here to guide the development.
:::

As a high-level requirement, the nanogrid should provide the following features:

- Interconnect households in off-grid areas or devices on building level
- Plug-and play operation
- Safe (<60 V) and reliable

### Power demands

Focus on expected power per household grid connection (t.b.c.):

- 250 W peak
- 50 W avg

The power level can be higher if the connection between energy storage/source and load is short.

Devices depending on site type:

- Households
  - Lighting, phone charging, radio, TV
- Productive use
  - Printer, laptop, mills, welding machines
  - Loads with high peak power need local battery for buffering.
- Shops
  - Lighting, phone charging as business, radio, TV, fridge

### Safety

The standard should focus on links that are safe but may incorporate higher power links that operate at dangerous voltages.

48V nominal bus - grid voltage always below 60V (SELV = safe to touch).

Protection against

- Short circuit
- Overcurrent
- Reverse polarity during assembly
- Arcing

### Metering

Accuracy: t.b.d.

Tempering protection should be implemented.

### Easy to use

Automatic recovery after fault conditions.

Simple and straightforward installation.

### Reliability

Mesh topology should be supported to provide redundant current paths.

### Non-intelligent Loads and/or Sources

The standard needs a way to incorporate non-intelligent loads. This may be satisfied by defining ports that incorporate power limits but do not otherwise participate in power allocation negotiations.

Provisions for non-intelligent sources aren TBD but may also be in the form of ports that bridge to the managed domain.

### Backwards Compatibility

The standard may incorporate multiple revisions with enhanced functionality.
The standard must allow devices conforming to previous versions to participate in grids based on newer standards, possibly at reduced functionality compared to newer devices.

### Standalone operation

Grids must provide core functionality without connection to the global Internet.  
For specialize management functions such as PAYGO, the standard must define a way to enter data without an Internet connection.
Resellers may choose to not use such functionality for their systems.

### Hacker protection

The standard must recognize the risk that hackers pose to managed grids.
It must incorporate mechanisms such as digital signatures to permit safe firmware updates limited to authorized sources.
The standard will include a physical mechanism such as a jumper to disable firmware updates.
The standard should define a way to disable intelligent operation and revert to an unmanaged grid with potentially reduced functionality such single sources.
