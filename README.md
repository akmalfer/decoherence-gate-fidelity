# decoherence-gate-fidelity
# Single-Qubit Decoherence and Gate-Fidelity Simulation

This repository contains the Jupyter Notebook (`Decoherence and Gate Fidelity.ipynb`) for simulating single-qubit quantum gate fidelity under Lindblad open-system dynamics. The notebook provides numerical validation, parameter sweeps, bivariate least-squares fitting, and cross-checks of weak-dissipation perturbation theory.

## Key Features

* **Interactive Colab & Jupyter Setup**: Automatically detects and installs missing dependencies like `qutip` when executed in Google Colab.
* **Lindblad Dynamics & Physical Validation**: Simulates single-qubit unitary rotations ($R_x, R_y, R_z$), $T_1$ energy relaxation, pure dephasing $T_\phi$, and combined dissipation trajectories benchmarked against exact analytical solutions.
* **6-Cardinal State Gate Fidelity**: Computes average gate fidelity $\bar{F}$ over all six cardinal initial states ($\vert{}0\rangle, \vert{}1\rangle, \vert{}+x\rangle, \vert{}-x\rangle, \vert{}+y\rangle, \vert{}-y\rangle$).
* **In-Pulse Trajectory Diagnostics**: Evaluates instantaneous fidelity along the rotation path throughout the pulse duration.
* **Bivariate Fits & Curvature Analysis**: Features 2D least-squares fits over $(\epsilon_1, \epsilon_2)$ space and evaluates second-order weak-dissipation curvature coefficients.
* **Solver Convergence Checks**: Verifies stability of simulation results under varying ODE solver tolerances (`atol`, `rtol`) in `qutip.mesolve`.
* **Automated Figure Export**: Generates, saves, and archives 13 publication-ready figures into a downloadable ZIP file.

## Mathematical Framework

All simulations use microseconds ($\mu\text{s}$) for time and rad/$\mu\text{s}$ for drive frequencies.

### First-Order Weak Dissipation

For dimensionless dissipation parameters $\epsilon_1 = t_g / T_1$ and $\epsilon_2 = t_g / T_2$, average gate infidelity is evaluated at first order as:

$$1 - \bar{F} \approx \frac{1}{6}\epsilon_1 + \frac{1}{3}\epsilon_2$$

### Second-Order Expansion

To account for higher-order curvature under stronger dissipation, the model extends to second order:

$$1 - \bar{F} \approx a\epsilon_1 + b\epsilon_2 - (c_{11}\epsilon_1^2 + c_{22}\epsilon_2^2 + c_{12}\epsilon_1\epsilon_2)$$

For drive pulses along the $x$ or $y$ axes with target angle $\theta$, the closed-form curvature coefficients are:

$$c_{11}(\theta) = \frac{\theta^2 + \sin^2\theta}{24\theta^2}, \quad c_{22}(\theta) = \frac{1}{8} + \frac{\sin^2\theta}{24\theta^2}, \quad c_{12}(\theta) = \frac{\theta^2 - \sin^2\theta}{12\theta^2}$$

For $z$-axis rotations, the coefficients simplify to $c_{11} = 1/12$, $c_{22} = 1/6$, and $c_{12} = 0$, independent of $\theta$.

## How to Run

### Option 1: Run in Google Colab (Recommended)

1. Click the **Open In Colab** badge above or upload `Decoherence and Gate Fidelity.ipynb` directly to [Google Colab](https://colab.research.google.com/)[cite: 1].
2. Select **Runtime > Run all**.
3. QuTiP will be automatically installed if not present.
4. At the end of execution, `decoherence_figures.zip` containing all generated figures will automatically download to your browser.

### Option 2: Run Locally in Jupyter
