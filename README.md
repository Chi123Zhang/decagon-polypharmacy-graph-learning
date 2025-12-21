# Decagon Polypharmacy Graph Learning
Benchmarking baseline models on the Decagon (TWOSIDES) dataset for polypharmacy side-effect prediction.

This project focuses on predicting adverse side effects caused by **drug combinations**. Since a drug pair can have **multiple** side effects, the primary setting is **multi-label prediction**; a simpler **binary** setting (any side effect vs. none) is also included.

## Tasks
- **Binary association prediction**: predict whether a drug pair exhibits *any* polypharmacy side effect (binary classification).
- **Multi-class side effect prediction**: predict the *dominant* side effect type for a drug pair, formulated as a large-scale multi-class classification problem (up to 1,317 side-effect classes).
- **Hierarchical (coarse-grained) evaluation**: map fine-grained side effects to broader disease-level categories (766 classes) using `bio-decagon-effectcategories.csv` to mitigate extreme class imbalance.
  
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
4. Specifics for each model:
   - GROVER: please first retrieve the SMILEs strings from the ChemBERTa notebook before using GROVER to tokenize the drugs into embeddings
   - R-GCN + ChemBERTa / GROVER: please first retrieve the embeddings from GROVER / ChemBERTa notebook before running this model

Notes:
- Several notebooks include `!pip install ...` cells intended for Colab. If you manage dependencies yourself, you can skip those cells.
- Some experiments expect intermediate artifacts (e.g., `refined_drug_embeddings_*.pkl`, model checkpoints) that are not committed; they are produced when running the notebooks end-to-end.
- For the GROVER model, we cloned from git using this version: https://github.com/tencent-ailab/grover.git

### Results
- `results/model_results_summary.xlsx`: Summary of binary classification performance (AUROC/AUPR) across baseline, tensor factorization, graph neural networks, and transformer-based models.
  
## Reference

- Seyone Chithrananda, Gabriel Grand, and Bharath Ramsundar. 2020. Chemberta: Large-scale self-supervised pretraining for molecular property prediction. arXiv preprint arXiv:2010.09885. Submitted to NeurIPS 2020 Workshop on Machine Learning for Molecules.
- S. Hakim and A. Ngom. 2025. Polyllm: Polypharmacy side effect prediction via llm-based smiles encodings. Frontiers in Pharmacology, 16:1617142.
- S. Lin, G. Zhang, D. Q. Wei, and Y. Xiong. 2022. Deeppse: Prediction of polypharmacy side effects by fusing deep representation of drug pairs and attention mechanism. Computers in Biology and Medicine, 149:105984.
- Maximilian Nickel, Volker Tresp, and Hans-Peter Kriegel. 2011. A three-way model for collective learning on multi-relational data. In Proceedings of the 28th International Conference on Machine Learning (ICML), pages 809–816.
- Michael Schlichtkrull, Thomas N. Kipf, Peter Bloem, Rianne van den Berg, Ivan Titov, and Max Welling. 2017. Modeling relational data with graph convolutional networks. arXiv preprint arXiv:1703.06103.
- Marinka Zitnik, Monica Agrawal, and Jure Leskovec. 2018. Modeling polypharmacy side effects with graph convolutional networks. Bioinformatics, 34(13):i457–i466.
