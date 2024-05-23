# State-space representation of mechanical systems

## Equations of Motion
Let us consider *manipulator equations* in the form
$$
\bm{M}(\bm{q}) \ddot{\bm{q}} + \bm{c}(\bm{q},\dot{\bm{q}}) - \bm{\tau}_g(\bm{q}) = \bm{B}(\bm{q}) \bm{u}
$$
who's left-hand side may be for example derived from the system's kinetic $T$ and potential $V$ energy expressed in generalized coordinates by expanding Lagrange equations of the second kind. The terms as derived by this approach are
$$
\begin{aligned}
\bm{M}(\bm{q}) &= \frac{\partial^2 T}{\partial \dot{\bm{q}}^2} \\
\bm{c}(\bm{q},\dot{\bm{q}}) &= \frac{\partial^2 T}{\partial \dot{\bm{q}} \partial \bm{q}} \dot{\bm{q}} - \frac{\partial T}{\partial \bm{q}} \\
\bm{\tau}_g(\bm{q}) &= - \frac{\partial V}{\partial \bm{q}} \,.
\end{aligned}
$$

## Continuous-time dynamics
Most commonly used state-space representation of a mechanical system in continuous time is attained by concatenating $q$ and $\dot{q}$ to form the system's state 
$$
\bm{x} = \begin{bmatrix} \bm{q} \\ \dot{\bm{q}} \end{bmatrix} \,,\quad \dot{\bm{x}} = \bm{f}(\bm{x},\bm{u}) = \begin{bmatrix} \dot{\bm{q}} \\ \bm{M}^{-1}(\bm{q}) \left( \bm{\tau}_g(\bm{q}) - \bm{c}(\bm{q},\dot{\bm{q}}) + \bm{B}(\bm{q}) \bm{u} \right) \end{bmatrix} \,.
$$

### Linearization
The system's dynamics can be linearized by performing a Taylor expansion around a point $\{\bm{x}^*,\bm{u}^*\}$ which yields
$$
\dot{\bm{x}} = \bm{f}(\bm{x}, \bm{u}) \approx \bm{f}(\bm{x}^*,\bm{u}^*) + \frac{\partial \bm{f}}{\partial \bm{x}}(\bm{x}^*,\bm{u}^*) (\bm{x} - \bm{x}^*) + \frac{\partial \bm{f}}{\partial \bm{u}}(\bm{x}^*,\bm{u}^*) (\bm{u} - \bm{u}^*) \,.
$$

If $\{\bm{x}^*,\bm{u}^*\}$ is a fixed point, i.e. $\bm{f}(\bm{x}^*,\bm{u}^*) = \bm{0}$, first order partial derivatives of the system's dynamics simplify to
$$
\begin{aligned}
\frac{\partial \bm{f}}{\partial \bm{x}}(\bm{x}^*,\bm{u}^*) &= \begin{bmatrix} \bm{0} & \bm{I} \\ \bm{M}^{-1}(\bm{q}^*) \left( \frac{\partial \bm{\tau}_g}{\partial \bm{q}}(\bm{q}^*) + \frac{\partial \bm{B}}{\partial \bm{q}}(\bm{q}^*) \, \bm{u}^* \right) & \bm{0} \end{bmatrix} \\
\frac{\partial \bm{f}}{\partial \bm{u}}(\bm{x}^*,\bm{u}^*) &= \begin{bmatrix} \bm{0} \\ \bm{M}^{-1}(\bm{q}^*) \, \bm{B}(\bm{q}^*) \end{bmatrix}
\end{aligned}
$$
as terms involving $\frac{\partial \bm{M}^{-1}}{\partial \bm{q}}$ drop out because $\bm{\tau}_g - \bm{c} + \bm{B} \bm{u}^* = \bm{0}$ for all fixed points. Partial derivatives of $\bm{c}$ also disappear as all of its terms contain second degree products of velocities and all velocities must be equal to zero at a fixed point.

## Discretization via integration using the explicit Euler scheme
The most basic approach with which we may discretize continuous-time dynamics of a nonlinear system is by integrating the systems state with a timestep of $h$ using the explicit Euler scheme
$$
\bm{x}_{k+1} = \bm{x}_k + h \bm{f}(\bm{x}_k,\bm{u}_k) \,.
$$

### Linearization
Compared to more advanced integration methods, linearization of these discrete time dynamics around a point $\{\bm{x}^*,\bm{u}^*\}$ is trival:
$$
\begin{aligned}
\bm{x}_{k+1} - \bm{x}^* &= \bm{x}_k + h \bm{f}(\bm{x}_k, \bm{u}_k) - \bm{x}^* \\
&\approx \bm{f}(\bm{x}^*,\bm{u}^*) + \left( \bm{I} + h \frac{\partial \bm{f}}{\partial \bm{x}}(\bm{x}^*,\bm{u}^*) \right) (\bm{x}_k - \bm{x}^*) + h \frac{\partial \bm{f}}{\partial \bm{u}}(\bm{x}^*,\bm{u}^*) (\bm{u}_k - \bm{u}^*) \,.
\end{aligned}
$$
