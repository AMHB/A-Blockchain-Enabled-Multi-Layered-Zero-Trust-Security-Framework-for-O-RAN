# A Multi-Layered Zero-Trust Security Framework for O-RAN

**Ali Mehrban · Zakaria Abou El Houda · Hajar Moudoud · Bouziane Brik · Lyes Khoukhi**  
“A Blockchain-Enabled Multi-Layered Zero-Trust Security Framework for O-RAN,” *Proceedings of the 2025 IEEE International Wireless Communications & Mobile Computing Conference (IEEE IWCMC 2025)*, pp. 1564-1569.  
DOI: 10.1109/IWCMC65282.2025.11059720 | IEEE Xplore: <https://ieeexplore.ieee.org/document/11059720>

This repository hosts the **Colab / Jupyter notebook** that reproduces all core experiments reported in the peer-reviewed IEEE publication.  
We implement and evaluate a two-layer security solution for Open Radio Access Networks (O-RAN):

1. **Intelligent Threat Detection Layer**  
   * Distributed IoT anomaly detection that fuses **Transfer Learning (TL)** and **Federated Learning (FL)**.  
2. **Decentralized Access-Control Layer**  
   * A **blockchain-backed Zero-Trust** manager enforcing real-time identity and policy decisions via smart Access-Control Contracts (ACCs).

---

## Notebook Outline

| Step | Purpose |
|------|---------|
| **1. Environment Check & Imports** | Verify library versions (pandas, NumPy, scikit-learn, TensorFlow, LightGBM, Dask, seaborn, …). |
| **2. Google Drive Mount** | Attach your Drive so data files can be read/written. |
| **3. Data Ingest & Split** | Load the TON-IoT CSV, clean labels, stratified 80/20 split. |
| **4. Data Prep & Feature Selection** | Encode categorical vars, scale numerics, create 100 virtual devices for FL. |
| **5. Neural-Network Global Pre-training** | 2 × 64-unit MLP trained 20 epochs; smoothed learning curves. |
| **6. Federated Transfer Learning (NeuralNetwork_TL)** | Local fine-tuning on each shard → FedAvg aggregation → global eval. |
| **7. LightGBM Transfer Learning (LightGBM_TL)** | 100-round global booster + 50-round per-device fine-tune; best shard wins. |
| **8. Classical ML on Shards** | RF, KNN, SVM trained per shard; highest-AUC shard becomes global model. |
| **9. Final Evaluation & Visualization** | Report Accuracy, Precision, Recall, F1, AUC; draw ROC curves & confusion matrices. |

---

## Quick Start

1. **Upload** `train_test_network.csv` to `Colab/ORAN_Security_IWCMC_2025/` in your Google Drive.  
2. **Open** the notebook in Google Colab (or any Jupyter environment) and execute cells 1 → 9 sequentially.  
3. **Review** the printed metric table and plots to replicate the paper’s results.

---

## Tested Environment

| Package | Version (min) |
|---------|---------------|
| Python  | 3.10 |
| pandas  | 2.2.3 |
| numpy   | 2.0 |
| scikit-learn | 1.6 |
| tensorflow | 2.18 |
| lightgbm | 4.6 |
| dask | 2024.12 |
| seaborn | 0.12 |

Exact versions are re-printed in **Cell 1** at runtime.

---

## Citation

If you build upon this work, please cite the IEEE paper:

```bibtex
@INPROCEEDINGS{11059720,
  author    = {Mehrban, Ali and Abou El Houda, Zakaria and Moudoud, Hajar and Brik, Bouziane and Khoukhi, Lyes},
  title     = {A Blockchain-Enabled Multi-Layered Zero-Trust Security Framework for O-RAN},
  booktitle = {2025 IEEE International Wireless Communications and Mobile Computing Conference (IWCMC)},
  year      = {2025},
  pages     = {1564--1569},
  doi       = {10.1109/IWCMC65282.2025.11059720},
  keywords  = {Open RAN; Zero Trust; Security; Internet of Things; Anomaly Detection; Blockchain; Federated Learning}
}
