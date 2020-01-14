# Goals and Objectives

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
