# Nonlinear Pendulum Stability and Region of Attraction

## Overview

This project uses MATLAB to simulate and analyze the stability of a **nonlinear damped pendulum** using Lyapunov stability concepts.

The purpose of the project is to demonstrate how numerical simulation and Lyapunov analysis can be used together to study a nonlinear dynamical system. In particular, the program estimates the **region of attraction** of the stable downward equilibrium by simulating the pendulum from a grid of different initial angles and angular velocities.

The numerical results are then compared with an energy-based boundary obtained using the pendulum's mechanical energy as a Lyapunov function.

---

## Pendulum Dynamics

The state variables are defined as:

* $\theta$ — pendulum angle (rad)
* $\omega$ — angular velocity (rad/s)

The nonlinear damped pendulum is modeled by:

$$
\dot{\theta} = \omega
$$

$$
\dot{\omega} = -\frac{g}{l}\sin(\theta) - \frac{k}{m}\omega
$$

where:

* $g$ = gravitational acceleration
* $l$ = pendulum length
* $m$ = pendulum mass
* $k$ = damping coefficient

The dynamics and stability analysis were based on the treatment of nonlinear systems in **Hassan K. Khalil's *Nonlinear Systems*** and the Lyapunov analysis presented in MIT's **Underactuated Robotics** notes.

---

## Purpose

The goal of this project is to explore several concepts in nonlinear control and dynamical systems:

* Numerical simulation of nonlinear differential equations
* Stability of an equilibrium point
* Estimation of a region of attraction
* Lyapunov stability analysis
* Energy-based Lyapunov functions
* Phase-plane analysis
* Comparison of numerical and analytical stability results

Rather than relying only on a linearized model near the equilibrium, the complete nonlinear pendulum dynamics are simulated.

---

## Numerical Region of Attraction

The program generates a grid of initial conditions covering:

$$
-2\pi \leq \theta_0 \leq 2\pi
$$

and

$$
-7 \leq \omega_0 \leq 7
$$

For every combination of initial angle $\theta_0$ and angular velocity $\omega_0$, MATLAB's `ode45` solver simulates the nonlinear system for **20 seconds**.

A trajectory is classified as converging to the downward equilibrium when its final state satisfies:

$$
|\theta_f| < 0.05
$$

and

$$
|\omega_f| < 0.05
$$

The result for each initial condition is stored in a matrix and displayed as a colour map. This provides a numerical visualization of which initial states converge to the equilibrium.

---

## Lyapunov Function

The total mechanical energy of the pendulum relative to the downward equilibrium is used as the Lyapunov function:

$$
V(\theta,\omega)
=
\frac{1}{2}ml^2\omega^2
+
mgl(1-\cos\theta)
$$

The first term represents the pendulum's kinetic energy:

$$
T = \frac{1}{2}ml^2\omega^2
$$

and the second term represents its gravitational potential energy relative to the downward
