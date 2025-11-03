---
title: Impedance Consensus Controllers 
tags: paper
image: static/content/mass/cover2.png
shortdesc: (2016) A dive into nonlinear leader-follower Impedance consensus controllers for multi-agent systems. An impedance consensus algorithm is presented for leader-following Lagrangian Multi-Agent Systems (MASs) with directed communication topology in the Input-to-State stability (ISS) sense.
---

<div class="justify-text">

## Description

In this study, an impedance consensus algorithm is presented. This is a set of rules that allows a group of agents to agree on their "impedance"—that is, their stiffness or resistance when interacting with their environment. This agreement is critical for practical tasks, such as multiple robots cooperatively carrying a single fragile object (preventing them from breaking it) or for safely interacting with a human.

This algorithm is designed for leader-following Lagrangian Multi-Agent Systems (MASs), which are teams of moving robots (agents) modeled using energy-based physics, where one robot acts as the leader and the others are followers. The method works even with a directed communication topology, meaning the communication links between agents might only go in one direction (e.g., Robot A can send info to B, but B cannot send info to A).

The system's stability is proven in the Input-to-State stability (ISS) sense, which guarantees that the team remains stable and predictable even if affected by small external disturbances. This is a key benefit, as it prevents minor errors from causing the robots to vibrate or waste energy by pushing and pulling against each other.

A general class of desired behaviors, called nonlinear impedance surfaces, is introduced. This "surface" is essentially the target rulebook for how the agents should behave when they touch or push against their surroundings. It is shown that the follower agents achieve this impedance consensus (all agree on the target "feel") in finite time (a fixed, predictable amount of time, not just eventually). This works as long as a directed spanning tree exists in the communication network, meaning there is at least an indirect communication path from the leader to every single follower.

Finally, it is proved that the proposed method also solves position and velocity consensus, meaning all agents agree on where to be and how fast to move. This is achieved using a robust technique called the sliding mode control method, which ensures all agents reach their goals while maintaining the desired impedance and overall system stability (ISS). This dual achievement is what allows the team to successfully perform a complex task, like jointly polishing a curved surface, where they must all move in perfect sync while applying the exact same delicate pressure.
<div>


## Resources

<a class="ieee-logo" href="https://ieeexplore.ieee.org/abstract/document/7576914">Link to</a>

[Download the Paper]({{ site.url }}/static/content/mass/ver14.pdf)


<!-- ## Tempest

![Result]({{ site.url }}/static/content/legos-steredenn/tempest.png)

- [Mecabricks model](https://www.mecabricks.com/fr/models/beDa5DyYvzg)
- [Brick list](http://www.brickowl.com/wishlist/view/abbast/steredenn-tempest)
- Manual (**not up-to-date**)

![Step]({{ site.url }}/static/content/legos-steredenn/tempest/1.png) -->
