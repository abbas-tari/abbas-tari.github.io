---
title: Dynamic Modeling of Soft Continuum Manipulators 
tags: paper
# image: static/content/lgvi/ENDM.png
# image: static/content/lgvi/Plot3D_Exp_vs_Sim_v3.jpg
# image: static/content/lgvi/TimeEvo/lvedBeam3.jpg
# image: static/content/lgvi/cover1.png
image: static/content/lgvi/TimeEvolvedBeam3.jpg
shortdesc: (2020) using Lie Group Variational Integration
---

<div class="justify-text">

## Intro: Key Concepts
This long post (yet I hope it is worth reading) principally deals with the variational principles of mechanics, particularly the Lagrangian and Hamiltonian descriptions of dynamical systems. For some of the concepts are borrowed from [this lecture](https://www.physics.usu.edu/torre/6010_Fall_2016/). A general remark is that feel free to familiarize yourself a few concepts listed here. They will help grasping the whole picture a bit better.
<!-- ### Aditional Concepts -->
<!-- ### <span id="aditional-concepts">Aditional Concepts</span> -->
- Configuration and Configuration space
- Generalized Coordinates
- (Extended) Velocity phase space
- 
### Variational principles

Variational principles are fundamental to understanding the behavior of physical systems. They involve finding the path, curve, surface, etc., which makes a certain quantity an extremum (minimum or maximum). for example, consider a simple pendulum. According to the principle of least action, the pendulum will swing along a path that minimizes the action, which is a quantity integrated along the path of the pendulum.



Among the variational principles, the Principle of Least Action is paramount. It posits that the path taken by a system between two points in its configuration space is the one that minimizes (or makes stationary) the action 
$$ S $$. The physical essence here is that among all conceivable paths the pendulum could take between two points in its configuration space (defined by the angle $$ \theta $$ and its rate of change $$ \dot{\theta} $$, it chooses the one that minimizes the action $$ S $$. This behavior is characteristic of all physical systems, not just the pendulum, and is a reflection of nature's tendency to follow a path of least resistance or extremum action.

The appearance of variational principles in classical mechanics can in fact be traced
back to basic properties of quantum mechanics. This is most easily seen using Feynman’s path integral formalism. For simplicity, let us just think about the dynamics of a point particle in 3-d. Very roughly speaking, in the path integral formalism one sees that the probability amplitude (In quantum mechanics, instead of probabilities, we often deal with probability amplitudes, complex numbers whose squared magnitudes give probabilities) for a particle to move from one place, $$ r_1 $$, to another, $$ r_2 $$, is given by adding up the probability amplitudes for all possible paths connecting these two positions (not just the classically allowed trajectory).

Richard Feynman developed a formulation of quantum mechanics called the path integral formalism. In this, the behavior of a quantum system is described by considering all possible paths a particle can take, rather than just one "classical" path. The probability amplitude for the particle to move from $$ r_1 $$ ​ to $$ r_2 $$ ​ is calculated by summing up the amplitudes for all possible paths the particle could take. The amplitude associated with a specific path 
$$ r(t) $$ is a funcion of the action functional for that path. The action functional assigns a number to each path between $$ r_1 $$ ​ and $$ r_2 $$. The way it does this depends on the physical specifics of the system like masses, potentials, and degrees of freedom.

In the classical limit, which typically applies to macroscopic systems, it’s shown that the dominant contributions to the sum over paths come from the critical (or "stationary") points of the action functional. The stationary paths are those where the action functional doesn't change appreciably for nearby paths. This is the core of a variational principle - the system's trajectory will be such that variations around it do not appreciably change the action.


Classical mechanics’ variational principles, like the principle of least action, emerge from the quantum mechanical description when considering macroscopic or classical limits. Feynman’s path integral formalism provides a mathematical framework that encapsulates this quantum-to-classical transition, showing how the classical "path of least action" is the dominant contribution among the sum over all possible quantum paths a particle can take between two points.



### Lagrangian and Hamiltonian Mechanics

One can view “classical mechanics” as an
approximation to the more fundamental “quantum mechanics”, this approximation being
valid, e.g., for macroscopic systems. A key link between these two descriptions of dynamics
is made via the Lagrangian and Hamiltonian formalisms.

<!-- Lagrangian Mechanics is a reformulation of classical mechanics introduced by Joseph Louis Lagrange. The Lagrangian function  $$ L $$  is defined as the difference between the kinetic energy  $$ T $$  and potential energy  $$ V $$  of a system, i.e., 
 $$ L=T−V $$ . Take a block sliding down a frictionless incline. Using Lagrangian mechanics, one can derive the equations of motion by applying the Euler-Lagrange equation, a fundamental equation in this formulation.

This is another reformulation by William Rowan Hamilton. The Hamiltonian function  $$ H $$  is defined as the sum of the kinetic and potential energies,  $$ H=T+V $$ .  In a simple harmonic oscillator (a mass on a spring), Hamiltonian mechanics allows us to write down the equations of motion in a succinct form, which can then be solved to find the position and velocity of the mass as functions of time. -->

Imagine you're at a skatepark with a skateboard. You start at the top of a ramp and skate down and up the other side. Lagrangian mechanics helps to describe your motion, accounting for your potential and kinetic energy at every point. Similarly, Hamiltonian mechanics can be used to analyze and predict your motion too.

When analyzing a dynamical system (systems whose configuration evolves
in time according to some deterministic law) the first task is to figure out what are the equations of motion. The Lagrangian
and Hamiltonian formalisms are the most powerful ways to do this. Next, most interesting dynamical systems are simply too complex in their
behavior for one to find closed-form, analytical expressions for their motion. In other
words, the solutions to the equations of motion exist, but you will never be able to write
them down in practice. So that is why we use numerical methods for example to come up with solutions. It should be noted that configuration
space for a system is a set of variables which characterizes what the system is
doing at a given time.


### Observables, States, and Laws

In particular, there are 3 key ingredients in a physical theory: Observables,
States, and Laws. Observables are, naturally, quantities which can be measured (at least in principle).
They are things like, the energy of a system, the position of a particle, etc. . In classical
mechanics, observables mathematically correspond to functions on phase space. (Think
about it: position, momentum, energy, angular momentum, etc. — all functions on phase
space.) The state of a system is a characterization of the values of all possible
observables when the system is in that state. Think about it: if observables
are functions on phase space, then if you know what point in phase space the system
occupies you know the value of all the observables. Laws come in various forms, but for dynamical theories (e.g., classical mechanics, quantum mechanics, electrodynamics,. . .) they will normally include a statement defining
the change of the system in time. In classical mechanics, the equations of motion play this
role.


### <span id="aditional-concepts">Aditional Concepts</span>
There are some more important concepts that I just list them here but no much explanation at the moment. Hopefully in the future, I will try to complete this post and establish a good foundation to explain the mothod used in the paper for modeling of soft continnum manipulators. You can read/download the paper in the given links in [Resources](#Resources) section.

- Hamilton’s Principle
  - The action integral
  - Euler-Lagrange equations
- The total time derivative
- Lack of uniqueness of the Lagrangian
- Coordinate Invariance of EL Equations
- Constraints: which restrict the motion to some subspace and they also shrink the configuration space.
- Conservation Laws/Constants of the motion (conservation of energy, momentum and angular momentum and so on): By a conservation law we mean a quantity constructed from the coordinates, velocities, accelerations, etc. of the system that does not change as the system evolves in time.
- Conservation of energy, momentum and angular momentum
- Time translation Symmetry and Energy Conservation
- Rotational Symmetry and Conservation of Angular Momentum

<div>


## <span id="Resources">Resources</span>

<a class="plosone-logo" href="https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0236121">Link to</a>

[Download the Paper]({{ site.url }}/static/content/lgvi/file.pdf)


