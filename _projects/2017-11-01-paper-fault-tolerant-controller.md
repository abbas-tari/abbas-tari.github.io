---
title: Fault-Tolerant Controllers 
tags: paper
image: static/content/ftc/topologies.png
# image: static/content/ftc/cover1.png
shortdesc: (2017) of Nonlinear Multi-Agent Systems with Directed Link Failures, Communication Noise and Actuator Faults
---

<div class="justify-text">

## Description

This paper addresses the fault-tolerant control problem for multi-agent systems (MASs)—groups of interconnected agents such as robots or autonomous vehicles that coordinate their behavior. The primary objective is achieving "consensus," which means all agents' states converge to a common agreement using only local information from their neighbors. The challenge addressed here involves maintaining consensus when three critical problems occur simultaneously: directed link failures and recoveries in the communication network, communication noise that corrupts transmitted information, and actuator faults that reduce the effectiveness of agents' physical components.

The communication network topology is modeled as randomly switching, with failures and recoveries governed by a Markovian jump process—a stochastic model where transitions between network configurations follow probabilistic rules. Communication noise represents the inevitable corruption of information due to imperfect sensors, electromagnetic interference, and quantization errors. Actuator faults refer to "loss-of-effectiveness" scenarios where motors or control mechanisms operate at reduced or degraded capacity. The work employs Sliding Mode Control (SMC), a robust control technique, combined with weak infinitesimal operation to develop a passive Fault-Tolerant Control (FTC) strategy. "Passive" indicates the controller does not require fault detection and isolation mechanisms—it inherently compensates for faults through its design.

The main theoretical contribution establishes sufficient conditions for achieving consensus in the "mean square sense"—a statistical stability measure appropriate for stochastic systems where convergence is probabilistic rather than deterministic. The key requirement is that each possible communication topology must contain a "spanning tree," which is a connected graph structure ensuring information can propagate from at least one agent to all others. The proposed controller guarantees finite-time convergence to predefined stochastic sliding surfaces while maintaining robustness against all three disturbance types. Importantly, the controller design does not require precise knowledge of model uncertainties or bounds on nonlinear terms.

The theoretical framework transforms the consensus problem into a stochastic input-to-state stability problem for nonlinear switched systems. Validation is provided through numerical simulations of networked Euler-Lagrange systems—mathematical models representing mechanical systems with inherent physical constraints. This work represents the first comprehensive treatment simultaneously addressing nonlinearity, communication noise, directed link failures, and actuator faults in multi-agent consensus problems.
<div>


## Resources

<a class="tf-logo" href="https://ieeexplore.ieee.org/abstract/document/7576914">Link to</a>

[Download the Paper]({{ site.url }}/static/content/ftc/Main_Manuscript.pdf)


