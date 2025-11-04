---
title: Finite-Time Input to State Stability
tags: paper
image: static/content/ftiss/Communication.jpg
shortdesc: (2020) of Discontinuous Dynamical Systems, A Case Study of Networked Euler-Lagrange Systems
---

<div class="justify-text">

## Description

This work addresses Finite-Time Input-to-State Stability (FTISS) for Discontinuous Dynamical Systems (DDSs). DDSs are systems whose mathematical descriptions contain discontinuities—abrupt changes in system behavior rather than smooth transitions. These discontinuities appear in practical applications such as robotic manipulators with environmental contact, where Coulomb friction (friction between dry surfaces in contact) causes both velocity jumps and force discontinuities. The analysis employs extended Filippov's solutions—a mathematical framework for handling differential equations with discontinuous right-hand sides—and non-smooth Lyapunov functions, which are stability-proving functions that need not be differentiable everywhere.

Input-to-State Stability (ISS) means that system states remain bounded whenever inputs are bounded, and states reach equilibrium when inputs approach zero. Finite-Time Input-to-State Stability extends this concept by guaranteeing that system trajectories converge to a desired band in finite time and remain there for all future times, rather than only achieving asymptotic convergence. The theoretical framework uses non-smooth and set-valued analysis—mathematical tools for functions that are not differentiable. Set-valued maps assign a set of values rather than a single value to each point, naturally capturing uncertainties in system parameters or behavior.

The main contribution is a theorem establishing sufficient conditions for FTISS of DDSs. This theorem uses non-smooth FTISS Lyapunov functions with relaxed conditions compared to existing results, meaning the requirements are less restrictive while still guaranteeing stability. The approach handles systems where conventional Lipschitz continuous vector field conditions do not apply. The theoretical results are applied to Multi-Agent Systems (MASs) with Euler-Lagrange dynamics—mathematical models describing mechanical systems like robotic manipulators governed by energy principles. A decentralized sliding mode controller is designed for finite-time leader-following consensus, where multiple agents (followers) synchronize their positions and velocities with a leader agent in finite time.

Sliding Mode Control (SMC) is a robust control technique that forces system trajectories to "slide" along predefined surfaces where desired behavior is guaranteed, providing natural resistance to disturbances and discontinuities. The proposed algorithm applies to directed communication topologies (where information flows in specific directions between agents) and guarantees consensus despite the presence of discontinuous dynamics. Numerical simulations using 2-DOF planar robot manipulators validate the effectiveness of the approach, demonstrating impedance control—regulation of the interaction force between the manipulator and its environment—while following desired trajectories in both free motion and constrained motion phases.
<div>


## Resources

<a class="ieee-logo" href="https://ieeexplore.ieee.org/abstract/document/9083577">Link to</a>

[Download the Paper]({{ site.url }}/static/content/ftiss/SICE_ISCS.pdf)


