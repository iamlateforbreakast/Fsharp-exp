Scope
=====
This document reviews 2 different Data Handling architectures and attempts to estimate the development cost of a lunar rover system from a systeme software perspective as a parametric coefficient applied to the SFR original software development cost (150000h). An attempt at parametric FA cost is also provided.

The baseline for the SFR mission consists of one OBC based on SPARC Leon2FT architecture associated to a Leon4 (GR740) architecture. In this design, the main OBC executes the equipment management including wheel actuation, the autonomous FDIR, data handling management, the mission planning and part of the GNC algorithms (path planning). The co processor executes image processing and visual odometry and the rest of the GNC algorithms.

[fig]

Architectural Considerations
===≠========================
When considering a system software, the following component are identified:
o GNC
o Data handling
o FDIR & Operations
o Infrastructure

TODO: explain GNC
TODO: explain data handling scope
TODO: FDIR operations
TODO: Infrastructure

In order to provide a unified synthetic view across all components, coefficients are allocated to each component to reflect the impact on the complexity therfore cost of software development.
o GNC (25%)
o Data Handling (25%)
o FDIR & Operations (25%)
o Infrastructure (25%)

Architecture A
==============
For this architecture, a central OBC is considered using a quad core 32bit ARM at 667MHz. FPGA based acceleration is not considered in this exercise. All software elements operate on this OBC.

o GNC Architecture
o Data Handling Architecture
o FDIR Architecture
Architecture A requires the acquisition of an external supervisor license.

TODO: Impact on software development.

Architecture B
==============
This architecture uses 2 on board computers interconnected. A platform OBC and a Data Processing Unit connected throught a Canbus or Spacewire bus.

o GNC Architecture
Currently, the GNC uses 2 closed loops. One closed loop is between path control and locomotion management to assess the effects of wheel actuation. The other closed loop is between the path control and the visual odometry. In the architecture, the locomotion is controlled by the platform computer and the visual odometry by the DPU. [Fig]

o Data Architecture
The mechanisms to exchange data between the platform OBC and DPU needs to be established. For example,

o FDIR Architecture
A strong characteristic of this architecture, it the extreme simplification of the failure management at DPU level. A failure a GNC sensor would invalidate the whole chain. The DPU would mark the chain as failed. The platform OBC would then need to switch to the redundant sensor chain.

Conclusion
==========
Both architecture A and B, if selected require up front effort to confirm their cost impact. Architecture A requires preliminary assessment to understand the impact of separating the execution of the GNC algorithms across 2 or 3 cores as well as structural impact on data management.
Architecture B requires preliminary assessment to understand the feasibility to isolate the GNC execution. Whilst the separation of the GNC execution over several cores is available for free, it requires a more flexible approach to the wheel actuation. It is important to note that effort will have to be expanded to design a suitable method to exchange data between platform OBC and DPU. The extreme simplification of FDIR if confirmed by further analysis also greatly simplifies the software design and verification.

TODO: Propose RND plan.


