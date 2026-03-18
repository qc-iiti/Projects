# Comprehensive Analysis of Grover's Amplitude Amplification Under Phase-Damping Channels

**Central doc link:** [https://docs.google.com/document/d/1Vuph1La7Tq0mi5d6wmS7WFSGgJU2EnORGaWDk2U3YZ8/edit?tab=t.0]

all the colab notebooks , observation docs , reports and sheets etc can be accessed through central doc 

A rigorous quantum-algorithmic framework for characterizing and mitigating the impact of environmental dephasing ($T_2$ noise) on Grover's search algorithm in Noisy Intermediate-Scale Quantum (NISQ) systems. This project integrates theoretical open quantum system models with numerical simulations to map the exact thresholds where quantum advantage is lost and demonstrates how early circuit termination ($k_{opt}$) acts as a zero-overhead mitigation strategy.

## Objective

To quantify the performance degradation of Grover's unstructured search under physical phase-damping constraints and identify the empirically optimal iteration count ($k_{opt}$) to maximize success probability before decoherence overwhelms the system.

## Key Principles

### Amplitude Amplification & The Oracle
Grover's algorithm provides a quadratic speedup $\mathcal{O}(\sqrt{N})$ for unstructured search by iteratively applying an oracle and a diffusion operator. This rotates the quantum state vector toward the target state via constructive interference.

### Phase-Damping ($T_2$) via Density Matrices
Models the hardware reality where interactions with the environment cause the loss of relative phase information without changing state populations. Simulated using the Lindblad master equation, this noise aggressively decays the off-diagonal elements (coherences) of the density matrix.

### The Iteration Trade-off & Peak Shift
Proves that in noisy environments, the theoretical ideal iteration count ($k_{ideal} \approx \frac{\pi}{4}\sqrt{N}$) is actively destructive. Because multi-controlled oracle gates drastically increase circuit depth, the "noise budget" is exhausted early. The empirical optimal iteration ($k_{opt}$) shifts leftward, requiring early termination to prevent the system from degrading into a maximally mixed state.

### The $N^{-1.1}$ Scaling Bottleneck
Highlights the critical limitation of near-term quantum search. The error threshold for maintaining a quantum advantage scales strictly as $N^{-1.1}$. Without full error correction, this exponential growth in dephasing acts as the absolute boundary for scaling unstructured search.

## Features

* **Density Matrix Simulation:** Uses Qiskit Aer's `density_matrix` simulator to accurately capture the non-unitary dynamics of $T_2$ decoherence.
* **Gate-Time Aware Noise Injection:** Binds noise directly to hardware execution speeds (e.g., 50ns for single-qubit, 300ns for two-qubit gates) to model realistic physical degradation.
* **Automated Peak Detection:** Systematically sweeps $n$ (qubits) and $T_2$ parameters to extract the maximum achievable success probability ($P_{max}$) and its corresponding $k_{opt}$.
* **Phase Diagram Generation:** Visualizes the "Quantum", "Transition", and "Degraded" operating regimes across the parameter space.
* **Analytical Modeling:** Utilizes Akaike (AIC) and Bayesian Information Criteria (BIC) to fit the complex decay of the quantum state, proving that a combined polynomial-power model best captures the hardware variance.

## System Workflow

1. **Circuit Generation:** Parameterize Grover circuits incorporating multi-controlled X (MCX) gates transpiled to native basis gates.
2. **Noise Configuration:** Define phase-damping channels calibrated to specific gate durations and varying $T_2$ coherence times.
3. **Execution & Parsing:** Run parallel density matrix simulations and extract the target state amplitude at every iteration step $k$.
4. **Data Aggregation:** Isolate $P_{max}$ and $k_{opt}$ for each configuration and log the metrics into structured datasets.
5. **Statistical Analysis:** Apply AIC/BIC modeling to derive predictive scaling laws for quantum hardware failure.

## Technologies Used

* Qiskit (Aer Simulator)
* Python
* Pandas (Data Aggregation)
* NumPy & Matplotlib (Phase Diagram/Heatmap Generation)
* SciPy (AIC/BIC Statistical Fitting)

## Background References

* *Comprehensive Analysis of Grover's Amplitude Amplification Under Phase-Damping Channels*
* L.K. Grover, *A fast quantum mechanical algorithm for database search*
* Nielsen & Chuang, *Quantum Computation and Quantum Information*
* Qiskit Documentation on Open Quantum Systems

## Contributors

* [Shubham sharma - IITI EP'29]
* [Arya Patil - IITI EP'29]
* [Parth Pawar - IITI MnC'29]
