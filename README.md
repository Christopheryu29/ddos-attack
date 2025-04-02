# 🛡️ DDoS Attack Detection in SDN using Machine Learning

This project implements a robust machine learning pipeline to detect **DDoS (Distributed Denial of Service)** attacks in **Software Defined Networks (SDNs)**. Multiple classification models are trained and evaluated on a public dataset to distinguish between **malicious** and **normal** network flows.

---

## 📂 Dataset

- **Path:** `/kaggle/input/dataset-sdn/dataset_sdn.csv`
- **Samples:** 104,345 network flow records
- **Features:** 23 total, including:
  - `pktcount`, `bytecount`, `pktrate`, `src`, `dst`, `Protocol`, etc.
- **Target Label:**
  - `label = 0`: Safe traffic
  - `label = 1`: Malicious traffic

---

## ⚙️ Preprocessing Steps

1. **Remove null and duplicate entries**
2. **Drop irrelevant columns:**
   - `switch`, `dur`, `dur_nsec`, `flows`, `port_no`, etc.
3. **One-Hot Encoding**:
   - Applied to `src`, `dst`, `Protocol`
4. **Feature Scaling**:
   - `StandardScaler` for normalization
5. **Train/Test Split**:
   - 80% training, 20% testing (`random_state=42`)

---

## 🧠 Models Implemented

Each algorithm is defined within a `Model` class and includes hyperparameter tuning:

| Model                 | Method                     |
|----------------------|----------------------------|
| Logistic Regression  | `M.LogisticRegression()`   |
| Support Vector Machine (SVM) | `M.SupportVectorMachine()` |
| K-Nearest Neighbors  | `M.KNearestNeighbor()`     |
| Decision Tree        | `M.DecisionTree()`         |
| Random Forest        | `M.RandomForest()`         |
| XGBoost              | `M.XGBoost()`              |

---

## 📊 Sample Results

| Model              | Accuracy  | Notable Details                          |
|-------------------|-----------|------------------------------------------|
| Logistic Regression | 80.08%   | Best with `newton-cg` solver             |
| Decision Tree      | 97.92%   | Criterion: `gini`, Depth: 7              |
| K-Nearest Neighbors | 99.48%  | Best with `n_neighbors=5`, weighted      |
| Random Forest      | 99.99%   | 200 estimators, very high precision      |
| XGBoost            | 100.00%  | Tuned with GridSearchCV (200 trees)      |
| SVM                | 98.40%   | Kernel: `rbf`, C=10, gamma=`scale`       |

---

## 📈 Visualizations

- **Correlation Matrix** of numeric features using Seaborn heatmap
- **Pie Chart** for label distribution (Safe vs Malicious)

---

## 🧪 How to Use

```python
# Prepare the model
M = Model(X)

# Train and evaluate models
M.LogisticRegression()
M.DecisionTree()
M.KNearestNeighbor()
M.RandomForest()
M.XGBoost()
M.SupportVectorMachine()
