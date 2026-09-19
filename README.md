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

and the second term represents its gravitational potential energy relative to the downward equilibrium:

$$
U = mgl(1-\cos\theta)
$$

Therefore:

$$
V = T + U
$$

For the damped pendulum, mechanical energy is dissipated by the damping term. This makes the energy function useful for studying the stability of the downward equilibrium.

---

## Energy Boundary

The program also calculates the energy associated with the upright equilibrium:

$$
\theta = \pi, \qquad \omega = 0
$$

Substituting this state into the Lyapunov function gives:

$$
V(\pi,0)
=
mgl(1-\cos\pi)
$$

Since:

$$
\cos\pi=-1
$$

the resulting energy level is:

$$
V(\pi,0)=2mgl
$$

The contour:

$$
V(\theta,\omega)=2mgl
$$

is plotted over the numerically simulated region of attraction.

This provides a visual comparison between the behavior observed through numerical simulation and the boundary obtained from the energy-based Lyapunov analysis.

---

## Visualizations

The MATLAB script generates several plots.

<img width="1192" height="769" alt="image" src="https://github.com/user-attachments/assets/1a15e270-5293-46c4-9dfd-6e39e0b80a1f" />
<img width="1174" height="762" alt="image" src="https://github.com/user-attachments/assets/0b8e3083-97fa-456d-8750-6bd5ba81e9aa" />
<img width="1208" height="777" alt="image" src="https://github.com/user-attachments/assets/a9e5f985-13d3-4f34-887d-0fc773a5ecf0" />
<img width="1224" height="804" alt="image" src="https://github.com/user-attachments/assets/27c7e69f-fd8a-48bc-8426-b2de18f32d18" />
<img width="1236" height="792" alt="image" src="https://github.com/user-attachments/assets/91192d7e-ac6e-45d3-b17e-5542bc7f9a56" />


### 1. Simulated Region of Attraction

A colour map shows which combinations of initial angle and angular velocity converge to the downward equilibrium.

The energy contour

$$
V(\theta,\omega)=2mgl
$$

is plotted on top of the simulated results for comparison.

### 2. Pendulum Angle vs. Time

The angle $\theta(t)$ is plotted over time for a sample initial condition.

### 3. Angular Velocity vs. Time

The angular velocity $\omega(t)$ is plotted over time.

### 4. Phase Portrait

The trajectory is plotted in the $(\theta,\omega)$ state space, providing a phase-plane representation of the pendulum's motion.

### 5. Lyapunov Function vs. Time

The value of

$$
V(\theta(t),\omega(t))
$$

is plotted over time to visualize how the pendulum's mechanical energy changes as damping dissipates energy from the system.

---

## Running the Simulation

The project requires **MATLAB**.

Run the main function using:

```matlab
main_Pendulum
```

The program will simulate the nonlinear pendulum and generate the region-of-attraction, state-response, phase-portrait, and Lyapunov-function plots.

---

## References

**H. K. Khalil**
*Nonlinear Systems*, 3rd Edition.
Prentice Hall, 2002.

**Russ Tedrake — MIT Underactuated Robotics**
*Lyapunov Analysis*
https://underactuated.mit.edu/lyapunov.html

---

## Notes

The simulated region of attraction is a **numerical estimate**. Its appearance depends on factors such as:

* Initial-condition grid resolution
* Simulation duration
* Numerical solver behavior
* Selected convergence tolerance

In this implementation, a trajectory is considered converged when both the final angle and angular velocity have magnitudes below `0.05`.

The project is intended as an educational demonstration of how **numerical simulation, phase-plane analysis, and Lyapunov methods** can be combined to investigate the stability of a nonlinear dynamical system.
