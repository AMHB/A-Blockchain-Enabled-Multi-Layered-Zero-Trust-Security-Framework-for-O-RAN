# A Multi-Layered Zero-Trust Security Framework for O-RAN  
**Ali Mehrban et al.**, “A Blockchain-Enabled Multi-Layered Zero-Trust Security Framework for ORAN,” *IWCMC 2025*. :contentReference[oaicite:0]{index=0}:contentReference[oaicite:1]{index=1}

This repository contains a Colab / Jupyter notebook that implements the core experiments from the above paper. We demonstrate a two-layer security solution for Open Radio Access Networks (O-RAN):

1. **Intelligent Threat Detection Layer**  
   - Combines **Transfer Learning (TL)** and **Federated Learning (FL)** for distributed IoT anomaly detection.
2. **Decentralized Access Control Layer**  
   - Uses a **blockchain-backed Zero-Trust** identity and policy manager (Access Control Contracts) to enforce real-time access rights.

---

## Notebook Overview

The code is organized into **nine** sequential cells:

1. **Environment Check & Imports**  
   Load and print versions of all required libraries (pandas, NumPy, scikit-learn, TensorFlow, LightGBM, Dask, seaborn, etc.).

2. **Google Drive Mount**  
   Mount your Drive so that data files (`train_test_network.csv`, splits) can be read/written.

3. **Data Ingest & Split**  
   - Load the combined TON-IoT network traffic CSV.  
   - Drop any rows missing a ground-truth label.  
   - Perform a stratified 80/20 train/test split and save `train_network.csv` & `test_network.csv`.

4. **Data Preparation & Feature Selection**  
   - Load the saved splits.  
   - Drop high-cardinality or “leaky” fields (IP addresses, URIs, etc.).  
   - Encode remaining categorical features and standard-scale all numeric columns.  
   - Shuffle and shard the **training** split into **100** “virtual IIoT devices” for FL.

5. **Neural-Network Global Pre-training**  
   - Build a 2×64 MLP (ReLU→ReLU→sigmoid) with optional regularization.  
   - Pre-train on the entire **training** set, validating on the **test** set, for 20 epochs.  
   - Smooth the learning curves (3-epoch moving average) for clear visualization.

6. **Federated Transfer Learning (NeuralNetwork_TL)**  
   - Re-partition the training data into 100 shards.  
   - Clone the global model onto each shard, fine-tune locally for 10 epochs (TL step).  
   - Aggregate all 100 local models via **FedAvg** → new global model.  
   - Evaluate the updated model on the test set (loss, accuracy, precision/recall/F1/AUC).

7. **LightGBM with Transfer Learning (LightGBM_TL)**  
   - Pre-train a LightGBM booster on the full training split (100 rounds).  
   - Fine-tune each shard for 50 additional boosting rounds starting from the global init.  
   - Select the device model with the highest AUC on test as the final **LightGBM_TL**.

8. **Classical ML on Shards (RF_No_TL, KNN_No_TL, SVM_No_TL)**  
   - For each of 100 shards, train Random Forest, KNN, and SVM locally.  
   - Evaluate each shard’s model on the test set; select the shard with highest AUC as the “global” model for each algorithm.

9. **Final Evaluation & Visualization**  
   - Compute end-to-end metrics (Accuracy, Precision, Recall, F1, AUC) for all five final models.  
   - Plot consolidated ROC curves and display confusion matrices for each model group.

---

## How to Use

1. **Upload** the `train_test_network.csv` dataset to your Google Drive under `Colab/ORAN_Security_IWCMC_2025/`.  
2. **Open** the notebook in Colab (or Jupyter) and run cells 1–9 in order.  
3. **Inspect** the printed metrics table and plots to reproduce the paper’s experimental results.

---

## Dependencies

Tested with:

- Python 3.10+
- pandas ≥ 2.2.3  
- numpy ≈ 2.0  
- scikit-learn ≈ 1.6  
- tensorflow 2.18+  
- lightgbm 4.6+  
- dask 2024.12  
- seaborn 0.12+

Refer to the version checks in **Cell 1** for exact runtime compatibility.

---

## Citation

If you use this code in your research, please cite:

> A. Mehrban, Z. Abou El Houda, H. Moudoud, B. Brik, L. Khoukhi,  
> “A Blockchain-Enabled Multi-Layered Zero-Trust Security Framework for ORAN,” *Proc.* IEEE IWCMC 2025. :contentReference[oaicite:2]{index=2}:contentReference[oaicite:3]{index=3}

---
