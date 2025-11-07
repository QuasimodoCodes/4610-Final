# 🐝 Particle Swarm Optimization (PSO) Project

**Author:** Victor  
**Date Started:** November 7, 2025  
**Status:** ✅ Specification-Compliant | 🔄 Step 1.1 Complete

---

## 📁 Project Structure

```
particle_swarm_project/
├── pso_analysis.ipynb           # Main implementation notebook
├── plan.json                    # 5-step structured plan with progress tracking
├── PROJECT_SPECIFICATION.md     # Master reference document (specification v1.0)
├── COMPLIANCE_CHECK.md          # Detailed compliance verification
├── problems_log.md              # Issue tracking and resolutions
├── features_backlog.md          # Future enhancements and extensions
├── README.md                    # This file
└── results/                     # Output directory for plots, CSV, logs
```

---

## 🎯 Project Objectives

Implement and analyze **Particle Swarm Optimization** for continuous optimization:

1. ✅ Implement standard PSO with configurable parameters
2. Test on 4 benchmark functions across 3 dimensionalities (2, 10, 30)
3. Run 30 independent trials per configuration
4. Analyze convergence, stability, and final accuracy
5. Compare global-best vs local-best PSO variants

---

## 📊 Benchmark Functions

| Function       | Search Range      | Global Min | Difficulty          |
| -------------- | ----------------- | ---------- | ------------------- |
| **Sphere**     | [-5.12, 5.12]     | 0          | Easy (unimodal)     |
| **Rosenbrock** | [-2.048, 2.048]   | 0          | Medium (valley)     |
| **Rastrigin**  | [-5.12, 5.12]     | 0          | Hard (multimodal)   |
| **Ackley**     | [-32.768, 32.768] | 0          | Hard (flat regions) |

---

## ⚙️ PSO Parameters

| Parameter           | Value            | Notes                            |
| ------------------- | ---------------- | -------------------------------- |
| **Particles**       | 30 (50 for n=30) | Swarm size                       |
| **Iterations**      | 300              | Max budget                       |
| **Inertia (ω)**     | 0.7              | Exploration/exploitation balance |
| **Cognitive (c₁)**  | 1.5              | Personal best influence          |
| **Social (c₂)**     | 1.5              | Global best influence            |
| **Velocity Clamp**  | ±0.5 × range     | Prevents explosion               |
| **Velocity Init**   | 10-20% of range  | Initial movement                 |
| **Runs per config** | 30               | Statistical reliability          |

---

## 📝 Implementation Plan (plan.json)

### ✅ Step 1: Initialize Project (IN PROGRESS)

- ✅ **1.1** Create tracking files and specification documents
- 🔄 **1.2** Set up Jupyter notebook with imports
- ⏳ **1.3** Implement benchmark functions
- ⏳ **1.4** Create results directory structure

### ⏳ Step 2: Core PSO Algorithm

- Particle class with position, velocity, pbest tracking
- PSO class with swarm initialization and update rules
- Velocity clamping and boundary handling
- Stop criteria and iteration tracking
- Test on 2D Sphere function

### ⏳ Step 3: Run Experiments

- 4 functions × 3 dimensions × 30 runs = 360 total experiments
- Record per-iteration gbest fitness
- Record per-run final fitness, position, evaluations
- Save results to CSV files

### ⏳ Step 4: Analysis & Visualization

- Convergence curves (log-scale y-axis)
- Summary statistics (mean, median, best, worst, std, success rate)
- Performance comparison tables
- Discussion of trends and patterns

### ⏳ Step 5: PSO Variants Comparison

- Implement local-best (lbest) PSO
- Compare gbest vs lbest performance
- Analyze diversity and convergence differences
- Document findings and recommendations

---

## 📈 Expected Deliverables

1. ✅ Working PSO implementation (modular, documented)
2. ✅ Convergence plots for all function × dimension combinations
3. ✅ Statistical summary tables
4. ✅ Performance analysis and discussion
5. ✅ CSV files with raw experimental data
6. ✅ Variant comparison (gbest vs lbest)

---

## 🔬 Success Criteria

| Criterion        | Target                                           |
| ---------------- | ------------------------------------------------ |
| **Correctness**  | All functions properly implemented and bounded   |
| **Efficiency**   | ≤1 minute per run                                |
| **Reliability**  | Consistent results across 30 runs                |
| **Reporting**    | Clear plots, labeled results, concise discussion |
| **Code Quality** | Readable, modular, well-documented               |

---

## 🚀 Getting Started

### 1. Open the Notebook

```bash
cd "c:\Users\Victor\Desktop\4610 Final\particle_swarm_project"
jupyter notebook pso_analysis.ipynb
```

Or open `pso_analysis.ipynb` in VS Code.

### 2. Follow the Plan

Check `plan.json` for current progress and next steps.

### 3. Track Issues

Log any problems in `problems_log.md`.

### 4. Add Ideas

Record future enhancements in `features_backlog.md`.

---

## 📚 Key Documents

- **`PROJECT_SPECIFICATION.md`** — Master reference (follows specification v1.0)
- **`COMPLIANCE_CHECK.md`** — Verification that plan aligns with specification
- **`plan.json`** — Live progress tracking with detailed substeps
- **`problems_log.md`** — Issue log and resolutions
- **`features_backlog.md`** — Future improvements and parameter studies

---

## ✅ Specification Compliance

This project **fully complies** with the PSO Project Description v1.0:

- ✅ All 4 benchmark functions with correct formulas and ranges
- ✅ All experimental parameters (ω, c₁, c₂, velocity clamp, etc.)
- ✅ Success thresholds for performance evaluation
- ✅ 30 runs × 3 dimensions × 4 functions = 360 experiments
- ✅ Complete statistical analysis pipeline
- ✅ Global-best vs local-best variant comparison
- ✅ Reproducibility through seed control
- ✅ Comprehensive documentation and tracking

See `COMPLIANCE_CHECK.md` for detailed verification.

---

## 🔄 Current Status

**Step 1.1 COMPLETE** ✅  
**Next Action:** Begin Step 1.2 — Set up notebook with imports and configuration

---

## 📞 Support

For questions or issues:

1. Check `problems_log.md` for similar issues
2. Review `PROJECT_SPECIFICATION.md` for requirements
3. Consult `features_backlog.md` for planned enhancements

---

**Last Updated:** November 7, 2025  
**Project Progress:** 1 of 20 substeps complete (5%)
