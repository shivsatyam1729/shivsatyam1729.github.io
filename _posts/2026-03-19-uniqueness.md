---
layout: post
title: "Uniqueness, laplacian and divergence"
date: 2026-03-16
---

The idea of uniqueness in electrostatics bothered me when i first studied it. Every other explanation covering uniqueness always revolved around boundary conditions. Why can there not be multiple potential functions satisfying the same equation and the same boundary values?

### Poisson’s Equation and Gauss’s Law

In general, for a warmup, Lets take a simple surface bounding some volume with density  $\rho$.

<img width="400" height="234" alt="image" src="https://github.com/user-attachments/assets/c0724210-9565-4926-bc12-26675009c4c6" />

Now, for this surface, we could use the Gauss's law which relates the divergence of the electric field with its charge density and vacuum permittivity.

$\vec{\nabla} \cdot \vec{E} = \dfrac{\rho}{\epsilon_o}$

where $\vec{\nabla} = \dfrac{\partial}{\partial x}\hat{i} + \dfrac{\partial}{\partial y}\hat{j} + \dfrac{\partial}{\partial z}\hat{k}$  

But, from Poisson's idea $-\vec{\nabla} \phi = \vec{E}$ which, in general terms is basically $-\vec{E} \cdot \vec{dr} = d\phi$.

Substituting this idea in **Gauss's** equation, we get $-\nabla^2 \phi = \dfrac{\rho}{\epsilon_o}$ which is also called the Poisson's equation.

If $\rho = 0$, the equation we get is called the ‘**Laplace’s equation**’. What does this even mean? Well if $\rho = 0$, there are no bound/free charges in the hypothetical surface.

<img width="400" height="232" alt="image" src="https://github.com/user-attachments/assets/de4dde16-6791-48f1-bf41-34dfcd56f7a3" />

### Analyzing an uniform spherical surface

Lets assume an uniformly charged sphere has a potential function such that $V = V(r, \theta, \phi)$ in spherical coordinates. Where $\theta$ is the polar angle and $\phi$ is the azimuthal angle. For more information, read more about [spherical coordinates](https://en.wikipedia.org/wiki/Spherical_coordinate_system).

<img width="400" height="368" alt="image" src="https://github.com/user-attachments/assets/5d6f2b29-fb4b-4e4c-ad95-d40c791b29a6" />


From $-\nabla^2\phi = \dfrac{\rho}{\epsilon_o}$,

lets define $\nabla^2 = \dfrac{\partial^2}{\partial x^2} + \dfrac{\partial^2}{\partial y^2} + \dfrac{\partial^2}{\partial z^2}$. Also, note that $\nabla^2 = \nabla \cdot \nabla$. Its just the dot product of the differential operator nabla.

For a uniform spherical conducting shell, the potential doesn’t depend on the polar angle and azimuthal angle. It only depends on the radial distance from the center (0, 0, 0). For a scalar function in spherical coordinate, the Laplacian is 

$\nabla^2 V = \frac{1}{r^2} \frac{\partial}{\partial r} \left(r^2 \frac{\partial V}{\partial r} \right) + \frac{1}{r^2\sin \theta}\frac{\partial}{\partial \theta}\left(\sin \theta \cancel{\frac{\partial V}{\partial \theta}}\right) + \frac{1}{r^2\sin^2 \theta} \cancel{\frac{\partial^2 V}{\partial \phi^2}}$

We get the Laplacian

$\nabla^2 V =\frac{1}{r^2}\frac{d}{dr}\left(r^2\frac{dV}{dr}\right)$

But, from Gauss’s law we know that the Laplacian of electric potential always equals $-\dfrac{\rho}{\epsilon_o}$.

using Gauss’s law, $\nabla^2 V =\frac{1}{r^2}\frac{d}{dr}\left(r^2\frac{dV}{dr}\right) = -\dfrac{\rho}{\epsilon_o}$

$\frac{1}{r^2}\frac{d}{dr}\left(r^2\frac{dV}{dr}\right) = -\dfrac{\rho}{\epsilon_o}$

$\frac{d}{dr}\left(r^2\frac{dV}{dr}\right) = -\dfrac{\rho r^2}{\epsilon_o}$

$\int{\left(r^2\frac{dV}{dr}\right)} = -\int{\dfrac{\rho r^2 dr}{\epsilon_o}}$

$\frac{dV}{dr} = -\dfrac{\rho r^3}{3\epsilon_o} + C_1$

Integrating again, we get,

$V = \dfrac{-\rho r^2}{6 \epsilon_o} + \dfrac{-C_1}{r} + C_2$

For an uniform sphere, $r = 0$ is a valid condition, therefore forcing us to put $C_1 = 0$. Therefore getting $V = \dfrac{-\rho r^2}{6 \epsilon_o} + C_2$. Now lets say that we know the potential at the surface. We could say $V_o = \dfrac{\rho R^2}{6 \epsilon_o} + C_2$. Subtracting $V$ from $V_o$ to get 

$V = V_o + \dfrac{\rho}{6 \epsilon_o}[R^2 - r^2]$

The whole point of this derivation is to ponder about the possibilities of potential with a non-uniform body and for a body that could be written by using the spherical coordinates, $r = 0$ would always be a problem. Since $\lim_{r \to0} \dfrac{-C_2}{r} \to -\inf$, we could intuitively say that we would always get an expression like $V = V_o + (...)$ which in turn proves that for $R \gt r$, $V \geq V_o$. Assuming $\rho > 0$.

### A Classic Proof of Uniqueness

Without loss of generality, lets take another surface such that we have the potential at every point on the surface (boundary). Lets assume that there are ≥ 2 solutions to the Laplace equation for this surface only.

Lets assume that there are two functions $V_1(\vec{r})$, $V_2(\vec{r})$ such that the Laplace’s equation holds true for $1 \text{ and } 2$ . We have the potential at the surface which is $V_o$. 

$\nabla^2V_1(\vec{r}) = 0$

$\nabla^2V_2(\vec{r}) = 0$

$V_{1s}(\vec{r}) = V_o$

$V_{2s}(\vec{r}) = V_o$

In the definitions, $V_{1s}$ is the potential due to function 1 at surface. 

But, lets define another function $V_3(\vec{r}) = V_1(\vec{r}) - V_2(\vec{r})$. 

After applying Laplacian we get, $\nabla^2\vec{V_3} = \nabla^2\vec{V_1} - \nabla^2\vec{V_2}$  . But $\nabla^2\vec{V_3}$  turns out to be 0, concluding that $\vec{V_3}$ is also a solution to the Laplacian. Also, $V_3(\vec{r}) = V_1(\vec{r}) - V_2(\vec{r}) = 0$ which is stupid because with this, we get that $V_3(\vec{r})$ is 0 on the surface.  But we just concluded with Poisson’s equation that $V \geq V_o$ where $V_o$ is the non-zero potential at the surface, forcing the solution of the Laplace to be constant (0).

In short the minimum can’t occur anywhere except the boundary but if $V_3(\vec{r})$ exists, $V_1(\vec{r}) = V_2(\vec{r})$ which proves our hypotheses that there is only one function that asserts the Laplace’s equation and the condition of boundary for a given surface.
