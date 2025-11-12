
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

## Quick Start
1. Ensure `spam.csv` (UCI SMS Spam Collection; columns `v1`=label, `v2`=text) is available.
2. Open and run `NSA_Spam_Detection.ipynb` end-to-end.
3. Artifacts (metrics & plots) will appear under `results/`.

## Default NSA Settings
- Encoding: **character k-grams** with `k=6`
- Matching rule: **r-chunk** with `m=3` fixed positions (3 wildcards)
- Number of detectors: `10000`
- Alphabet: `a-z`, digits, and space (after normalization)
- Seed: `1337`

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

## Notes
- r-contiguous random k-grams often produce **0 recall** (useful baseline to motivate r-chunk).
- You can swap in **Hamming-radius** detectors to allow point mutations instead of wildcards.
- Consider word-level r-chunk or mixed scales for robustness.



