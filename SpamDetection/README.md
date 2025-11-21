
# NSA Spam Detection (Artificial Immune Systems via Negative Selection)

This repository/notebook implements a **Negative Selection Algorithm (NSA)** for spam detection using the SMS Spam Collection (UCI). NSA learns **only from ham** (self) and generates **detectors** that do not match self according to an **r-chunk (wildcard)** rule. At inference, a message is flagged as spam if it matches any detector.

## Highlights
- **Ham-only training** (NSA correctness asserted)
- **r-contiguous baseline** (demonstrates zero-coverage issue)
- **r-chunk detectors** (k=6, m=3 by default) — high recall with reasonable FPR
- **Metrics**: Precision/Recall/F1, Confusion matrices, **ROC-AUC**, **PR-AUC**
- **Plots**: PR, ROC, **Detector coverage** (recall vs #detectors)
- **Detector statistics**: avg matches per spam/ham, **diversity** summary
- **Baseline classifier**: TF-IDF + Logistic Regression
- **Reproducible**: fixed seed, stratified splits, labeled figures
- **Exports**: metrics and figures to `results/`

## Project structure

```
.
├─ NSA_Spam_Detection.ipynb        # Main notebook with full implementation
├─ spam.csv                         # SMS Spam Collection (UCI format; v1/v2 columns)
├─ results/                         # All generated plots/metrics are saved here
│   ├─ nsa_rchunk_metrics.json
│   ├─ nsa_rchunk_metrics.csv
│   ├─ baseline_tfidf_lr_metrics.json
│   ├─ baseline_tfidf_lr_metrics.csv
│   ├─ summary_nsa_vs_baseline.csv
│   ├─ pr_curve_test_rchunk.png
│   ├─ roc_curve_test_rchunk.png
│   ├─ Validation_Confusion_Matrix_(r-chunk).png
│   └─ Test_Confusion_Matrix_(r-chunk).png
└─ README.md                        # This file
```

## Environment & prerequisites
- Python ≥ 3.9  
- Recommended: a clean virtual environment (`venv` or conda)

## Quick Start
1. Ensure `spam.csv` (UCI SMS Spam Collection; columns `v1`=label, `v2`=text) is available.
2. Open and run `NSA_Spam_Detection.ipynb` end-to-end.
3. Artifacts (metrics & plots) will appear under `results/`.

## Run the notebook end-to-end
```bash
jupyter notebook NSA_Spam_Detection.ipynb
# or
jupyter lab NSA_Spam_Detection.ipynb
```

Run all cells. The notebook will:

1. Load and normalize the dataset  
2. Create **60/20/20** (train/val/test) splits with a fixed seed (`SEED = 1337`)  
3. Build **self** k-grams from **ham in train**  
4. Generate detectors  
   - **r-contiguous**: strict `k`-gram matching (baseline, usually zero coverage)  
   - **r-chunk**: wildcards with `m` fixed positions (effective)  
5. Assert **NSA correctness** (no self matches)  
6. Evaluate on validation & test; save plots and metrics to `results/`  
7. Train and evaluate **TF-IDF + LR** baseline on the same splits  
8. Export summary CSVs and PNG plots

## Default NSA Settings
- Encoding: **character k-grams** with `k=6`
- Matching rule: **r-chunk** with `m=3` fixed positions (3 wildcards)
- Number of detectors: `10000`
- Alphabet: `a-z`, digits, and space (after normalization)
- Seed: `1337`

## Expected runtime
- r-contiguous generation: fast  
- r-chunk detector generation (10,000 detectors with `k=6, m=3`): seconds to a minute on a laptop  
- Vectorizer + Logistic Regression: seconds

## Outputs
- `results/nsa_rchunk_metrics.json|csv` — NSA metrics (Val/Test)
- `results/baseline_tfidf_lr_metrics.json|csv` — TF-IDF+LR metrics
- `results/pr_curve_test_rchunk.png`, `results/roc_curve_test_rchunk.png`
- `results/Validation_Confusion_Matrix_(r-chunk).png`, `results/Test_Confusion_Matrix_(r-chunk).png`
- `results/summary_nsa_vs_baseline.csv`

## Reproducibility
- Stratified split: 60%/20%/20% (train/val/test)
- NSA trains on **ham only** from the train split.
- An assertion ensures **no detector matches self**.

## Tuning Guide
- `m↑` → **precision↑**, **recall↓**; `m↓` → **recall↑**, **FPR↑**
- `k↑` → **precision↑**, **recall↓**; `k↓` does the opposite
- More detectors → **recall↑** (see coverage curve), but watch FPR

## Key functions & where to tweak

- **Text normalization**: `normalize_text`  
- **k-gram extraction**: `kgrams(text, k)`  
- **Self set** (ham-only): `build_self_kgrams(texts, labels, k)`  
- **r-contiguous detectors**:  
  - `generate_detectors_rcontig(k, num, self_k)`  
  - `predict_with_detectors_rcontig(texts, detectors, k)`  
- **r-chunk detectors**:  
  - `generate_detectors_rchunk(k, m, num, self_k)`  
  - `predict_with_detectors_rchunk(texts, detectors, k)`  
- **Correctness checks**: assert **0 NSA violations** after generation  
- **Metrics/plots**: `evaluate(...)` (prints F1/precision/recall, plots PR/ROC when scores provided)  
- **Coverage curve**: `detector_coverage_curve(...)` (recall vs number of detectors)

## Notes
- r-contiguous random k-grams often produce **0 recall** (useful baseline to motivate r-chunk).
- You can swap in **Hamming-radius** detectors to allow point mutations instead of wildcards.
- Consider word-level r-chunk or mixed scales for robustness.



