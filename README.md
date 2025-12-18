# Decagon Polypharmacy Graph Learning
Benchmarking baseline models on the Decagon (TWOSIDES) dataset for polypharmacy side-effect prediction.

This project focuses on predicting adverse side effects caused by **drug combinations**. Since a drug pair can have **multiple** side effects, the primary setting is **multi-label prediction**; a simpler **binary** setting (any side effect vs. none) is also included.

## Tasks
- **Binary association prediction**: predict whether a drug pair has *any* associated polypharmacy side effect.
- **Multi-label side effect prediction**: predict the set of side effects for a drug pair (one pair → many labels).
- **(Optional) Coarse / hierarchical evaluation**: map fine-grained side effects to broader categories using `bio-decagon-effectcategories.csv`.

## Models
- Frequency-based baseline
- **RESCAL** (binary + multi-label)
- **R-GCN** (binary + multi-label, implemented with PyTorch Geometric, ChemBERTA, and GROVER embeddings)
- **MLP baselines** on learned drug embeddings (ChemBERTa / GROVER variants)

## Metrics
- AUROC (micro / macro)
- AUPR / AUCPR (micro / macro)
- AP@50 (ranking)
- F1 (micro / macro) at a chosen threshold

## Data
The repository includes the core CSVs under `Data/`:
- `Data/bio-decagon-combo.csv`
- `Data/bio-decagon-effectcategories.csv`

Source and documentation: https://snap.stanford.edu/decagon/

## Repository Structure
- `RESCAL/` — RESCAL + baseline notebook
- `R-GCN/` — R-GCN notebooks (plain, +ChemBERTa features, +GROVER features)
- `ChemBERTa + MLP/` — ChemBERTa embedding + MLP notebook
- `GROVER + MLP/` — GROVER embedding + MLP notebook
- `Report/` — proposal / progress / final report PDFs

## Running
Most code lives in notebooks (`.ipynb`). Recommended workflow:
1. Start Jupyter from the repo root so relative paths work: `jupyter lab`
2. Open a notebook from one of the model folders.
3. Search for `base_path` in the notebook and update it to point at your local data location.

Notes:
- Several notebooks include `!pip install ...` cells intended for Colab. If you manage dependencies yourself, you can skip those cells.
- Some experiments expect intermediate artifacts (e.g., `refined_drug_embeddings_*.pkl`, model checkpoints) that are not committed; they are produced when running the notebooks end-to-end.

## Reference
- Zitnik, M., Agrawal, M., & Leskovec, J. (2018). Modeling polypharmacy side effects with graph convolutional networks. Bioinformatics.
- Nickel, M., Tresp, V., & Kriegel, H.-P. (2011). A Three-Way Model for Collective Learning on Multi-Relational Data (RESCAL). ICML.
- Schlichtkrull, M., Kipf, T. N., Bloem, P., van den Berg, R., Titov, I., & Welling, M. (2018). Modeling Relational Data with Graph Convolutional Networks. ESWC.
- Seyone Chithrananda, Gabriel Grand, and Bharath Ramsundar, “ChemBERTa: Large-Scale Self-Supervised Pretraining for Molecular Property Prediction,” arXiv:2010.09885, 2020.
- S. Hakim and A. Ngom, “PolyLLM: polypharmacy side effect prediction via LLM-based SMILES encodings,” Frontiers in Pharmacology, vol. 16, p. 1617142, July 31, 2025, doi:10.3389/fphar.2025.1617142. 
