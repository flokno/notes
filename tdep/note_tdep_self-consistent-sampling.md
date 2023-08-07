sTDEP
===

Here we sketch the relation of *stochastic TDEP* (sTDEP), where harmonic sampling instead of molecular dynamics simulations is used to generate nuclear snapshots, and the self-consistent harmonic approximation which minimizes the free energy, and show that the two are equivalent for a one-dimensional, classical harmonic oscillator.

## Definitions

1D Harmonic model:

$$
\begin{align}
V_k (u) 
	&= - \frac{1}{2} k u^2 \\
f_k 
	&= ku^2
\end{align}
$$

with force constant $k$, displacement $u$, and force $f_k = - \partial_k V_k$.

Partition function:

$$
\mathcal Z_k 
= \int  {\rm e}^{- \beta V_k (u)} du
= \int  {\rm e}^{- \frac{\beta}{2} k u^2} du
= \sqrt{\frac{2 \pi}{\beta k}}
$$

Free energy:

$$
F_k 
= - \frac{1}{\beta} \ln \mathcal Z_k
= - \frac{1}{\beta} \ln \sqrt{\frac{2 \pi}{\beta k}}
$$

Expectation values:

$$
\begin{align}
\langle V \rangle_k
&= \frac{1}{\mathcal Z_k} \int V(u) ~{\rm e}^{- \frac{\beta}{2} k u^2} du \\
\langle u^2 \rangle_k
&= \frac{1}{\mathcal Z_k} \int u^2 ~{\rm e}^{- \frac{\beta}{2} k u^2} du
= \frac{1}{\beta k} \\
\langle V_k \rangle_k
&= \frac{1}{\mathcal Z_k} \int V_k(u) ~{\rm e}^{- \frac{\beta}{2} k u^2} du
= -\frac{1}{2 \beta}
\end{align}
$$


## Free energy minimization

Gibbs-Bogoliubov:

$$
F 
\leq F_k + \langle V - V_k \rangle_k
$$

Search extremum in $k$:

$$
\begin{align}
\partial_k F
	&= 0 \\
\partial_k F_k
	&= \frac{1}{2 \beta k} = \frac{1}{2} \langle u^2 \rangle_k \\
\partial_k \langle V_k \rangle
	&= 0 \\
\partial_k \langle V \rangle_k
	&= \frac{1}{2 k} \langle u f \rangle_k
\end{align}
$$

with force $f = - \partial_u V$, where integration by parts is used in the last step.

At the extremum, we therefore have

$$
k = \langle u^2 \rangle_k^{-1} \langle u f \rangle_k
$$

## Force fit

TDEP extracts the force constant $k$ by minimizing the loss function

$$
\begin{align}
\mathcal L_k 
	&= \langle (f - f_k)^2 \rangle \\
	&= \langle f^2 + f_k^2 - ff_k \rangle \\
	&= \langle f^2 \rangle + k^2 \langle u^2 \rangle + 2 k \langle u f \rangle~.
\end{align}
$$

The solution is given by

$$
\begin{align}
\partial_k \mathcal L_k 
	&= 0 \\
\implies
k
	&= \langle u^2 \rangle^{-1} \langle u f \rangle~,
\end{align}
$$

which is the _least-squares_ solution for a given trial nuclear distribution. An iterative solution, where $k_n$ from step $n$ is used to set up the next generation of displacements and obtain a new force constant $k_{n+1}$, leads to free-energy minimization when self-consistency is reached. Iterative sTDEP is therefore equivalent to self-consistent phonon schemes, as also noted in [[vanRoekeghem2021]](#suggested-reading).

## Suggested reading

- [R. Bianco *et al.*, Phys Rev B **96**, 014111 (2017)](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.96.014111)
- [A. van Roekeghem, J. Carrete, and N. Mingo, Comput Phys Commun **263**, 107945 (2021)](https://www.sciencedirect.com/science/article/pii/S0010465521000710?via%3Dihub)