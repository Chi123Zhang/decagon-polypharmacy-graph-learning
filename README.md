# decagon-polypharmacy-graph-learning
Benchmarking models on the Decagon dataset for polypharmacy side-effect prediction.

## Overview
This project benchmarks learning-based baselines on the Decagon (TWOSIDES) polypharmacy dataset for predicting adverse side effects caused by **drug combinations**.

Because a single drug pair can be associated with **multiple** side effects, the primary problem setting is **multi-label prediction**. We also include a **binary** setting (predict whether a drug pair has any reported side effect).

## Tasks
- **Binary association prediction (link existence)** Predict whether a drug pair has *any* associated polypharmacy side effect.
- **Multi-label side effect prediction** Predict the set of side effects associated with a drug pair (one pair → many labels).
- **(Optional) Hierarchical / coarse-label evaluation** Map fine-grained side effects to broader disease classes for an additional multi-label evaluation.

## Models 
Implemented and evaluated:
- Frequency-based baseline
- RESCAL (binary and multi-label settings)
- R-GCN (binary and multi-label settings)
- MLP baselines using precomputed drug embeddings (e.g., ChemBERTa / GROVER variants)

## Metrics
We report metrics suited for highly imbalanced multi-label prediction:
- AUROC (micro / macro)
- AUPR / AUCPR (micro / macro)
- AP@50 (ranking metric)
- F1 (micro / macro) at a chosen threshold

## Data
We use the Decagon drug–drug–side-effect dataset (Zitnik et al., 2018). The project expects the following files (not included due to size constraints):
- `bio-decagon-combo.csv`
- `bio-decagon-effectcategories.csv` (for hierarchical / coarse mapping)

Original source: https://snap.stanford.edu/decagon/

Download the files manually and place them in the expected location (see notebook `base_path` variables and/or a local `data/` folder).

## Repository Structure
Top-level folders in this repository:
  - `RESCAL/` — RESCAL baselines and experiments
  - `Graph Model/` — R-GCN experiments (binary + multi-label), plus feature-augmented variants
  - `ChemBERTa/` — ChemBERTa embedding + MLP experiments
  - `GROVER_FINAL/` — GROVER embedding generation + MLP experiments
  - `report/` — final project report (PDF) 
  - `slides/` — presentation slides *(if included)*

  ## Notes

  Experiments were originally run in Google Colab and later adapted to local/remote paths using `base_path`.
