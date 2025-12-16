# decagon-polypharmacy-graph-learning
Benchmarking different models on the Decagon dataset for polypharmacy side-effect prediction.
# Graph-Based Polypharmacy Side Effect Prediction

This project benchmarks graph-based learning models on the Decagon dataset for predicting polypharmacy-induced side effects.  
We investigate both binary association prediction and multi-class side effect prediction under a unified graph learning framework.

## Models
The following models are implemented and evaluated:
- Frequency-based baseline
- RESCAL (binary and multi-class settings)
- R-GCN (binary and multi-class settings)

## Data
We use the Decagon drug–drug interaction dataset, which contains known side effects induced by combinations of drugs.  
Each drug pair may be associated with one or more side effect types.

The experiments were run in Google Colab using data stored on Google Drive.

- File: `bio-decagon-combo.csv`
- Original source: Decagon (Zitnik et al., 2018)
- Download link: https://snap.stanford.edu/decagon/

Due to file size constraints, the dataset is not included in this repository.
If neaded, please download the data manually and place it under `data/`.


## Repository Structure
- `notebooks/` — codes model training, evaluation, and visualization notebooks  
- `report/` — final project report (PDF)  
- `slides/` — forum presentation slides
