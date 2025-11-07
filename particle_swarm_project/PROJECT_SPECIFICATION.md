# Particle Swarm Optimization (PSO) Project Specification

**Version:** 1.0  
**Date:** November 7, 2025  
**Status:** Active Reference Document

---

## 1. Overview

This project implements and analyzes **Particle Swarm Optimization (PSO)** as a metaheuristic for solving continuous optimization problems. The objective is to evaluate PSO's performance on standard mathematical benchmark functions across multiple dimensionalities, comparing convergence speed, stability, and final accuracy.

The project will be organized systematically within a dedicated workspace to ensure **reproducibility, traceability, and iterative development**.

---

## 2. Problem Statement

PSO is inspired by the social behavior of flocks of birds or schools of fish, where individuals (particles) move through a search space, sharing information about good positions. Each particle represents a candidate solution, and its movement is influenced by:

- **Inertia** — retaining some of its previous velocity
- **Cognitive component (c₁)** — attraction toward its own best position found so far
- **Social component (c₂)** — attraction toward the global or neighborhood best position found by others

The goal is to **minimize continuous functions** by adapting particle positions over time through these dynamics.

---

## 3. Objectives

1. Implement a standard PSO algorithm with configurable parameters
2. Test it on multiple benchmark functions of varying difficulty and dimensionality
3. Evaluate and compare convergence behaviors
4. Collect and analyze statistical performance results
5. Present visual and quantitative evidence of algorithm efficiency and robustness

---

## 4. Benchmark Functions

| Function       | Formula                                                                                           | Search Range      | Global Minimum                       |
| -------------- | ------------------------------------------------------------------------------------------------- | ----------------- | ------------------------------------ |
| **Sphere**     | $f(x) = \sum_{i=1}^{n} x_i^2$                                                                     | [-5.12, 5.12]     | $f(x^*) = 0$ at $x^* = 0$            |
| **Rosenbrock** | $f(x) = \sum_{i=1}^{n-1} [100(x_{i+1} - x_i^2)^2 + (x_i - 1)^2]$                                  | [-2.048, 2.048]   | $f(x^*) = 0$ at $x^* = (1,\ldots,1)$ |
| **Rastrigin**  | $f(x) = 10n + \sum_{i=1}^{n} [x_i^2 - 10\cos(2\pi x_i)]$                                          | [-5.12, 5.12]     | $f(x^*) = 0$ at $x^* = 0$            |
| **Ackley**     | $f(x) = -20\exp(-0.2\sqrt{\frac{1}{n}\sum x_i^2}) - \exp(\frac{1}{n}\sum\cos(2\pi x_i)) + 20 + e$ | [-32.768, 32.768] | $f(x^*) = 0$ at $x^* = 0$            |

### Function Characteristics:

- **Sphere**: Convex and smooth, easy baseline
- **Rosenbrock**: Narrow curved valley, harder to converge
- **Rastrigin**: Highly multimodal, many local minima
- **Ackley**: Flat outer region with central basin, tests global exploration

---

## 5. Experimental Setup

| Parameter                 | Description                           | Default Value              |
| ------------------------- | ------------------------------------- | -------------------------- |
| **Swarm size**            | Number of particles                   | 30 (50 for n=30)           |
| **Dimensions**            | Problem size                          | 2, 10, 30                  |
| **Iterations**            | Stopping limit                        | 300                        |
| **Inertia (ω)**           | Balances exploration/exploitation     | 0.7                        |
| **Cognitive coeff. (c₁)** | Pull toward particle's own best       | 1.5                        |
| **Social coeff. (c₂)**    | Pull toward global best               | 1.5                        |
| **Velocity clamp**        | Max velocity per dimension            | ±0.5 × (upper–lower bound) |
| **Position init.**        | Random uniform in bounds              | —                          |
| **Velocity init.**        | Random 10–20% of range                | —                          |
| **Stop criteria**         | Fitness ≤ threshold or max iterations | Function-dependent         |
| **Repetitions**           | Number of independent runs            | 30 per setup               |

---

## 6. Data to Record

### Per Iteration:

- Global best (gbest) fitness value

### Per Run:

- Final best fitness
- Best position vector
- Iterations or evaluations used

### Across 30 Runs:

- Mean, median, best, worst fitness
- Standard deviation
- Success rate (threshold reached or not)

---

## 7. Output and Evaluation

### Convergence Curves

Plot best fitness vs. iterations for each function and dimension.

- **X-axis**: iteration
- **Y-axis**: log-scaled best fitness

### Statistical Summary

Present a table with average, best, and standard deviation for each combination (function × dimension).

### Performance Discussion

- How quickly each function converges
- Which functions remain difficult (Rosenbrock, Rastrigin, Ackley)
- Stability of results (variance across runs)

### Parameter Study (Optional)

- Explore how varying (ω, c₁, c₂) affects performance
- Include **lbest vs gbest** comparison to discuss swarm diversity

---

## 8. Expected Results

- **Sphere** should converge near zero even at n=30
- **Rosenbrock** will converge slowly, often with residual error
- **Rastrigin** may plateau due to local minima
- **Ackley** should approach near-zero values if exploration remains balanced
- Increasing dimensionality typically increases difficulty

---

## 9. Implementation Requirements

### Language

Python (NumPy + Matplotlib required)

### Structure Options

**Option A: Modular Python Files**

- `pso.py`: Core algorithm
- `functions.py`: Benchmark definitions
- `run_experiments.py`: Batch test runner
- `results/`: Output folder for logs, plots, CSV summaries

**Option B: Jupyter Notebook (Current Approach)**

- `pso_analysis.ipynb`: All implementation in structured sections
- `results/`: Output folder for logs, plots, CSV summaries

### Reproducibility

- Random seed control
- Fixed hyperparameters per test

### Documentation

- Comments for each function and major block
- Figures labeled and saved automatically

---

## 10. Deliverables

✅ **Code Implementation** — working PSO program with modular design  
✅ **Convergence Plots** — for each function and dimensionality  
✅ **Result Tables** — summary of performance statistics  
✅ **Short Discussion** — insights about performance trends  
✅ **Logs and Notes** — maintained in `problems_log.md` and `features_backlog.md`

---

## 11. Evaluation Criteria

| Aspect           | Requirement                                             |
| ---------------- | ------------------------------------------------------- |
| **Correctness**  | Functions correctly implemented and bounded             |
| **Efficiency**   | Algorithm runs within reasonable time (≤ 1 min per run) |
| **Reliability**  | Consistent performance across 30 runs                   |
| **Reporting**    | Clear plots, well-labeled results, concise discussion   |
| **Code Quality** | Readable, modular, documented                           |

---

## 12. Optional Extensions

- Implement **Hybrid PSO** (PSO + local search like Nelder–Mead)
- Introduce **Dynamic Parameters** (time-varying ω, c₁, c₂)
- Add **Topological Variants** (Ring topology, Von Neumann)
- Include **Animation Visualization** of swarm movement for n=2

---

## 13. Purpose of This Document

This document serves as the **master reference** for the PSO project. All plans (`plan.json`), problems (`problems_log.md`), and features (`features_backlog.md`) must remain consistent with this specification. Any deviation, improvement, or experimental extension should be logged and justified against the objectives defined here.

---

## 14. Compliance Tracking

- ✅ **plan.json** — Updated to include all parameters and thresholds
- ✅ **features_backlog.md** — Contains optional extensions
- ✅ **problems_log.md** — Ready for issue tracking
- 🔄 **pso_analysis.ipynb** — Implementation in progress

---

**Last Updated:** November 7, 2025  
**Next Review:** After Step 2 completion
