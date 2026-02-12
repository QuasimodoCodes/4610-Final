# Bees Algorithm (BA) for 0–1 Knapsack — README

This repository contains an all-in-one Jupyter notebook implementing the **Bees Algorithm** for the 0–1 knapsack problem, plus utilities for:

- Parsing common benchmark datasets (Pisinger knapPI\_*, WEING\_* style files, simple CSV).
- Running the BA solver with feasibility repair and statistics tracking.
- Greedy and DP-exact baselines for comparison.
- Reproducible single-run and batch-run helpers.
- Plotting convergence and summarising results.

---

## Repository Layout

- `BA_Knapsack.ipynb` — main notebook with all code, experiments, and plots.
- `requirements.txt` — Python dependencies for reproducing the notebook (recommended).
- `DATA/` — **not tracked**. Folder where benchmark instances should be placed (see below).
- `results/` — created automatically; stores summary CSVs and any tables exported from the notebook.

---

## Quick Start

### 1. Create and activate a virtual environment (optional but recommended)
    ```powershell
    python -m venv .venv
    .\venv\Scripts\Activate.ps1
    ```
2. **Install dependencies.**
    ```powershell
     pip install pip install numpy pandas matplotlib jupyter
    ```

3. **Create a folder called DATA in the repository root:**
    Place the following benchmark files inside DATA/ (filenames must match exactly, or adjust paths in the notebook):

    Pisinger knapPI CSV files (or compatible text/CSV variants), for example:

    knapPI_11_20_1000.csv

    knapPI_12_50_1000.csv

    knapPI_13_100_1000.csv

    WEING-style text instances (1-dimensional knapsack), for example:

    weing1.txt

    weing2.txt

    weing3.txt

    The notebook asserts that ./DATA exists and uses these filenames when building the benchmark instance list.


4. **Launch Jupyter Lab or Notebook and open `BA_Knapsack.ipynb`.**
   ```powershell
   python -m jupyter lab
   ```
5. **Run the notebook top-to-bottom.** Each task section is fully annotated, so you can execute cell-by-cell or choose `Kernel > Restart & Run All`.

    The notebook was executed with Python 3.10, Gymnasium 1.2.1, NumPy 2.2.6, and Matplotlib 3.8. Please match those versions (or newer) to avoid API changes.

## Notebook Roadmap

To make navigation easier, the notebook is structured into logical sections:

**Section 1 — Problem Representation & Utilities**
Defines the knapsack instance dataclass, objective helpers (total_value, total_weight), feasibility checks, and pretty-printing.

**Section 2 — Dataset Parsers**
Loaders for:

    Pisinger knapPI_* text/CSV blocks (parse_knapPI_multi_*, load_knapPI_by_name_any).

    WEING-style text instances.

    Simple tidy CSV instances for custom data.

**Section 3 — Baselines: Greedy & DP Exact**
Implements:

    Greedy ratio heuristic for a fast approximate solution.

    Classic 𝑂(𝑛𝑊) dynamic programming solver with a guardrail for large capacities.

**Section 4 — Bees Algorithm Implementation**

BAParams dataclass (number of scouts, elite/best sites, neighborhood radius, iteration limits, random seed, etc.).

Core BA loop with:

    Scout phase.

    Neighborhood search around elite/best sites.

    Feasibility repair for overweight solutions.

    Tracking of best solution and convergence statistics.

**Section 5 — Helpers: Single Run, Batch Run, Plotting**
Convenience wrappers to:

    Run BA once on a single instance (run_ba_on_instance).

    Run BA over many instances and seeds, collecting results in a pandas.DataFrame.

    Plot convergence curves and solution quality.

**Section 6 — Quick Sanity Check on a Tiny Dataset**
Uses a small instance to verify:

    BA produces feasible knapsack vectors.

    BA value ≥ greedy value and ≤ DP optimum value (when DP is enabled).

**Section 7 — Benchmark Instances from DATA/**

Asserts that DATA/ exists.

Loads a small panel of knapPI and WEING instances.

Prints n, capacity W, and basic statistics for each.

**Section 8 — Batch Experiments & Summary Table**

Runs BA (and baselines) over all instances.

Aggregates statistics (mean value, percentage of optimum, runtime, etc.).

Writes a compact report_table.csv to the results/ folder.


**How to Run & Test the Implementation**
A. Quick Functional Smoke Test (no external data needed)

Open the notebook.
Run all cells up to and including “Quick sanity check on a tiny CSV dataset”.
Confirm that:
The code runs without errors.
BA, greedy, and DP all return consistent objective values.
Convergence plots appear for the tiny instance.
This verifies that your environment, dependencies, and core BA logic work.

B. Single-Instance Debug Run

To experiment on one instance and see detailed behavior:
In the helpers / single-run section, locate the cell that:
Builds a KnapsackInstance (either custom or from DATA/).
Sets BAParams (e.g. params = BAParams(max_iters=300, seed=42)).
Run that cell and the following plotting cells.
Inspect:
Best value over iterations.
Feasibility of the final solution (total weight ≤ capacity).
Comparison with greedy or DP (if DP is safe for that capacity).
You can tweak BA hyperparameters (number of scouts, neighborhood radius, etc.) directly in BAParams and rerun.

C. Full Benchmark Run (reproducing results)

Ensure all required benchmark files are in DATA/ (see Prepare benchmark data above).
Run the “Load benchmark instances from DATA folder” section.
You should see available knapPI instance names printed for each CSV file.
Run the batch experiment cells that:
Iterate BA over all instances and seeds.
Build a summary_df / report_table.
At the end:
A table is displayed in the notebook.
A CSV summary is written to:
results/report_table.csv
This is the main “test suite” for the algorithm: it checks performance across multiple benchmark families and compares BA to baselines.

**Reproducing & Extending Experiments**

Change random seeds
Edit BAParams.seed or create a loop over seeds to study robustness.

Alternate parameter sets
Define multiple BAParams instances (e.g. “exploratory”, “exploitative”) and pass them to the batch-run helper to compare their performance.

Custom datasets

Format your instance as a tidy CSV or in the same style as the provided loaders.

Place it in DATA/ or reference an absolute path.

Use the existing parsing functions (parse_knapPI_* or a simple CSV reader) to plug it into the same evaluation pipeline.


**License and Reuse**

Created for the ACIT 4610 final group project.

**Acknowledgements**

Benchmark instances are based on standard 0–1 knapsack test sets (Pisinger knapPI, WEING, etc.).

AI tools were used to assist with documentation and structuring this project.
