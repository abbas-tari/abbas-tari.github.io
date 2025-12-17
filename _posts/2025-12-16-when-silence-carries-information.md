---
title: "When Silence Carries Information: Physics-Based Compression at the OT Edge"
tags: control-systems edge-computing iot lyapunov
shortdesc: Physics-based event-triggered control for efficient communication in OT edge systems.
---

<div class="justify-text">

At the OT edge, communication costs more than computation. With 5G rollouts accelerating and edge chips getting cheaper, it's easy to think bandwidth-saving techniques like Event-Triggered Control, which only transmit when something changes, are irrelevant, however, they're not.

## The Jevons Paradox of Industrial Data

In 1865, William Stanley Jevons observed that improvements in coal efficiency didn't reduce coal consumption. They increased it. Cheaper energy meant more machines, more factories, more demand. The efficiency gains were real. So was the explosion in total usage.

We're watching the same pattern with industrial data. 5G promises massive bandwidth. Edge chips promise local intelligence. The response from industry has been to generate more data, deploy more sensors, run more models.

But 5G has physical limits that marketing materials don't mention.

5G struggles with dense networks of devices transmitting simultaneously. The Random Access Channel has only 48 available orthogonal preamble sequences [1]. When tens of thousands of sensors on a factory floor report at once, collisions stack up. Theoretical peak bandwidth means nothing when packets wait in queue.

Battery technology hasn't kept pace either. Energy density in lithium-ion cells improves at 5–8% per year [2]. Moore's Law, before it slowed, delivered 41% annual gains in transistor density. We've been riding exponentials in compute while crawling forward in energy storage. That gap compounds.

And then there's the fundamental physics of radio transmission. Sending one bit wirelessly burns roughly 1,000× more energy than executing an instruction locally [3]. This isn't a limitation of current technology waiting to be engineered away. It's thermodynamics. Modulating a carrier wave, amplifying it to overcome path loss, encoding and decoding on both ends: these operations require energy that local computation simply doesn't.

A concrete example from our work: a two-second LoRa transmission at full power draws enough charge to keep an STM32L4 processor in low-power sleep for over 33,000 hours. Two seconds of transmission, or nearly four years of sleep.

For industrial IoT, autonomous vehicles coordinating over wireless links, and distributed robotic systems, the communication channel determines operational lifetime [4].

## The CPU Bottleneck

The old argument for edge computing was "reduce bandwidth to the cloud." That argument still holds. But a newer problem emerges as we push neural networks onto robots and AGVs.

The CPU itself becomes the bottleneck.

Consider a sensor node feeding data to an onboard AI running navigation or anomaly detection. If that sensor interrupts the processor 1,000 times per second to report "nothing changed," it's not just wasting radio power. It's stealing compute cycles from the neural network trying to keep the robot from hitting a wall.

RTOS context switches cost around 490 clock cycles each [5]. That's the overhead just to handle the interrupt, not to process the data. And cache pollution can slow inference by 2–3× [6] as the processor flushes and reloads working memory.

So we have a situation where sensors reporting "everything is fine" actively degrade the AI's ability to detect when things aren't fine. The redundant data isn't just wasteful. It's counterproductive.

## Physics-Based Compression

The fix requires rethinking what we're actually trying to communicate.

Traditional compression finds statistical redundancy in bitstreams. Physics-Based Compression finds semantic redundancy in the behavior of the physical system.

The core idea: if we know the physics of what we're monitoring, we can predict what the sensor should read. We only need to transmit when reality diverges from that prediction.

For control systems, this means calculating the system's energy state locally. A Lyapunov function V(x) = x^T P x gives us the system's "distance from stability" in a mathematically precise sense. If that distance is shrinking as expected, there's nothing to report. If it's growing faster than it should, something has changed and the network needs to know.

The energy economics favor this approach heavily. Waking a LoRaWAN radio costs about 5 millijoules per packet. Evaluating the quadratic form for a Lyapunov check costs about 10 microjoules on an STM32F4. That's a 500:1 ratio [7]. We can run 500 local physics checks for the energy cost of one transmission.

This inverts the traditional edge computing value proposition. We're not just reducing bandwidth to save cloud costs. We're spending microjoules to save millijoules, locally, at the sensor, before the radio ever wakes up.

The result is a Semantic Communication model where silence carries information. When the sensor stays quiet, the network knows: physical reality hasn't changed enough to matter. The absence of a message is itself a message.

## Safety Certification for Edge AI

The same Lyapunov function that tells us whether to transmit can also tell us whether an action is safe. If we're running a neural network controller for motion planning or process optimization, we typically have no formal guarantee that its outputs won't destabilize the system. Neural networks are black boxes. They work until they don't.

But the physics check doesn't care where the control command came from. It just asks: will this action cause the system's energy to grow or shrink?

We extended the triggering condition into what we call a Lyapunov Safety Gate [8]. If a neural network proposes an action that would violate stability bounds, the check catches it and holds the last safe command instead. The evaluation takes under one microsecond on a 168 MHz microcontroller [9]. Compared to actuation delays of 1–10 milliseconds, that's negligible latency for a mathematically provable safety guarantee.

This matters because alternative approaches to neural network safety are either expensive (formal verification, which doesn't scale) or slow (simulation-based testing, which can't cover all cases).

A physics-based runtime check isn't a complete solution. It requires knowing the Lyapunov function, which requires knowing the system dynamics, which isn't always possible. But for the large class of systems where we do have a physics model, even an approximate one, we get hard safety bounds that pure connectivity cannot provide.

## Validation

We built a directional triggering method that exploits not just whether the system is stable, but which directions in state space affect stability and which don't. Errors aligned with the Lyapunov gradient demand immediate correction. Errors orthogonal to it can be ignored regardless of magnitude.

Monte Carlo simulation across 100 trials shows 43.6% fewer transmissions than optimally tuned isotropic baselines, with no loss in control quality [10]. The isotropic methods (Tabuada's original approach) treat all error directions identically. They can't distinguish critical from benign errors. So they trigger conservatively and waste bandwidth.

Time-varying methods (like Mazo's approach) achieve similar transmission counts but with 2.1× worse control performance [11]. They let the system drift too far between updates.

Under real industrial conditions (accounting for battery degradation over two years, 1–10% packet loss requiring retransmissions, duty cycling), the 43.6% transmission reduction translates to 35–50% longer battery life [12]. For sensors that are supposed to run five years without replacement, that margin determines whether we meet requirements.

## Applicability and Limitations

Physics-Based Compression works when communication costs exceed computation costs by 100:1 or more. That's true for wireless sensor networks. It's not true for wired Ethernet, where transmission is nearly free.

It works when the system has directional asymmetry in its dynamics. In control terms: some state deviations push the system toward instability, others pull it back toward equilibrium. The method exploits this asymmetry to allow large errors in safe directions while tightly constraining errors in critical directions. Fully actuated systems with uniform controllability don't benefit as much.

It doesn't scale well to high-dimensional systems. The quadratic form evaluation is O(n²) in the state dimension. For n > 100, we burn enough compute that the energy savings disappear.

And it requires a physics model. If we don't know the system dynamics well enough to write down a Lyapunov function, we can't use this approach. Model-free learning is fashionable right now. Physics-based compression is decidedly model-required.

For the systems where it does work (process control, robotics, building automation, fleet coordination, remote monitoring), the gains are real and the implementation is straightforward.

## The Broader Point

The OT world is in a strange moment. Compute is cheap. Bandwidth is theoretically abundant. Cloud platforms will happily ingest whatever we send them. So the instinct is to transmit everything, store everything, analyze it later.

But physics doesn't care about cloud pricing. The radio still drinks power. The spectrum still fills. The CPU still stalls on interrupts. And the battery still dies.

The systems that will actually work at scale are the ones that respect these constraints. By making silence carry information. By spending microjoules to save millijoules. By using physics to decide what matters.

That's not a retreat from the promise of connected industry. It's the only way to deliver on it.

</div>

## References

<a class="substack-logo" href="https://abbasta.substack.com/p/when-silence-carries-information">Read the original article on Substack</a>

<a class="arxiv-logo" href="https://arxiv.org/abs/2512.03604">Read the technical paper on arXiv</a>
