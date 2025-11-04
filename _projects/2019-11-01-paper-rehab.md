---
title: Multi-User Tele-rehabilitation Robots
tags: paper
# image: static/content/rehab/Rehab_vrep.png
image: static/content/rehab/Rehab_Adams.jpg
shortdesc: (2019) Actuator Fault and Link Failure Accommodation for Disturbed Multi-User Telerehabilitation Systems Subject to Communication Noise
---

<div class="justify-text">

## Description
This work addresses Fault Tolerant Control (FTC) for Multi-User Telerehabilitation Systems (MUTSs), which are modeled as Itô stochastic differential equations—mathematical models that capture systems affected by random processes and noise. The system experiences actuator loss-of-effectiveness faults (motors operating at reduced capacity), directed link failures (communication connections that break and restore), communication noise (corrupted information transmission), and external disturbances. MUTSs represent a configuration where multiple remote robots (slaves) are controlled by a local robot (master), with slave states converging to the master's states using only local neighbor information.

The proposed solution uses an active FTC strategy based on Adaptive Sliding Mode Control (ASMC). "Active" FTC means the controller adapts its parameters in response to detected faults. The ASMC method enables the system to achieve stochastic consensus in the mean square sense—a statistical measure where the expected squared deviation from consensus converges to zero—onto predefined stochastic switching sliding surfaces in finite time. Directed link failures are modeled using Markovian Jump Systems (MJSs), where the communication topology switches randomly according to probabilistic rules.

The theoretical framework establishes Stochastic Input-to-State Stability (SISS), which guarantees that bounded inputs and disturbances produce bounded state deviations in a probabilistic sense. This represents the first comprehensive treatment of active FTC for MUTSs that simultaneously considers communication noise, actuator faults, directed link failures, and disturbances. Numerical simulations validate the effectiveness of the proposed control laws, demonstrating stable coordinated operation despite multiple concurrent fault types.
<div>


## Resources

<a class="ieee-logo" href="https://ieeexplore.ieee.org/document/8795781">Link to</a>

[Download the Paper]({{ site.url }}/static/content/rehab/rehab_paper.pdf)


