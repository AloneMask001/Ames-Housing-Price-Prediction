[README-2.md](https://github.com/user-attachments/files/28914976/README-2.md)
<p align="center">
  <h1 align="center">🏠 Ames Housing Price Prediction</h1>
  <p align="center">
    <strong>Predicting house prices using Advanced Regression Techniques</strong>
  </p>
  <p align="center">
    <img src="https://img.shields.io/badge/Python-3.8-blue?style=for-the-badge&logo=python&logoColor=white" alt="Python">
    <img src="https://img.shields.io/badge/XGBoost-ML-orange?style=for-the-badge&logo=xgboost&logoColor=white" alt="XGBoost">
    <img src="https://img.shields.io/badge/Pandas-Data-green?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas">
    <img src="https://img.shields.io/badge/Jupyter-Notebook-red?style=for-the-badge&logo=jupyter&logoColor=white" alt="Jupyter">
    <img src="https://img.shields.io/badge/Kaggle-Score%200.15175-20BEFF?style=for-the-badge&logo=kaggle&logoColor=white" alt="Kaggle">
  </p>
</p>

---

## ✨ About The Project

A machine learning project built on the **Ames Housing Dataset** — one of Kaggle's most popular advanced regression challenges. The project covers the full data science pipeline: data cleaning, NaN handling, ordinal encoding, feature importance selection and XGBoost regression.

> 💡 **Key Insight:** OverallQual, GarageCars and FullBath are the top 3 price drivers — accounting for over 50% of prediction power. Low-importance features (< 1%) were dropped to reduce noise and improve generalization.

---

## 📊 Quick Stats

<table>
  <tr>
    <td align="center"><b>📦 Dataset</b><br>1460 train / 1459 test</td>
    <td align="center"><b>🏙️ Location</b><br>Ames, Iowa</td>
    <td align="center"><b>📋 Raw Features</b><br>81 columns</td>
    <td align="center"><b>📍 Final Features</b><br>16 selected</td>
  </tr>
  <tr>
    <td align="center"><b>🤖 Model</b><br>XGBoost Regressor</td>
    <td align="center"><b>📈 Train R²</b><br>0.955</td>
    <td align="center"><b>🎯 Test R²</b><br>0.903</td>
    <td align="center"><b>🏆 Kaggle Score</b><br>0.15175 (RMSE log)</td>
  </tr>
</table>

---

## 🏆 Feature Importance

Features selected after dropping all columns below 1% importance threshold:

```
OverallQual     ████████████████████████████  23.1%  🏅 Overall Quality
GarageCars      █████████████████████         16.8%  🚗 Garage Capacity
FullBath        ████████████████████          12.0%  🚿 Full Bathrooms
BsmtQual        ██████                         6.0%  🏗️ Basement Quality
KitchenQual     █████                          4.1%  🍳 Kitchen Quality
GrLivArea       ████                           3.8%  📐 Above Ground Area
TotalBsmtSF     ████                           3.5%  📏 Total Basement Area
YearRemodAdd    ███                            2.9%  📅 Remodel Year
FireplaceQu     ███                            2.5%  🔥 Fireplace Quality
GarageCond      ██                             1.8%  🔧 Garage Condition
```

> 🔑 **Top 3 price determinants:** OverallQual, GarageCars and FullBath account for over **50%** of the prediction power.

---

## 📋 Selected Features

| Feature | Description | Encoding |
|:---|:---|:---:|
| `OverallQual` | Overall material and finish quality (1–10) | Numeric |
| `GarageCars` | Garage capacity in car count | Numeric |
| `FullBath` | Full bathrooms above grade | Numeric |
| `BsmtQual` | Basement height quality | Ordinal → Numeric |
| `KitchenQual` | Kitchen quality | Ordinal → Numeric |
| `GrLivArea` | Above grade living area (sqft) | Numeric |
| `TotalBsmtSF` | Total basement area (sqft) | Numeric |
| `YearRemodAdd` | Remodel year | Numeric |
| `FireplaceQu` | Fireplace quality | Ordinal → Numeric |
| `GarageCond` | Garage condition | Ordinal → Numeric |
| `GarageType` | Type of garage access | Label Encoded |
| `CentralAir` | Central air conditioning | Binary |
| `1stFlrSF` | First floor area (sqft) | Numeric |
| `2ndFlrSF` | Second floor area (sqft) | Numeric |
| `TotRmsAbvGrd` | Total rooms above grade | Numeric |
| **`SalePrice`** | **Property sale price (USD) — Target** | **Numeric** |

---

## 🔧 Data Pipeline

```
📥 Raw Data (81 columns, 1460 rows)
    │
    ├── 1️⃣  Drop high-NaN columns (> 50% missing)
    │       └── Alley, PoolQC, Fence, MiscFeature, MasVnrType removed
    │
    ├── 2️⃣  NaN Handling
    │       ├── Ordinal cols (BsmtQual, FireplaceQu, GarageQual...)
    │       │     └── NaN = "No Feature" → encoded as 0
    │       ├── Numeric cols (MasVnrArea, GarageYrBlt)
    │       │     └── Filled with train median
    │       └── Categorical cols (GarageType, Electrical)
    │             └── Filled with "No" or mode
    │
    ├── 3️⃣  Encoding
    │       ├── Ordinal: Manual map() (Ex=5, Gd=4, TA=3, Fa=2, Po=1, No=0)
    │       └── Nominal: map() with domain knowledge
    │
    ├── 4️⃣  Feature Importance
    │       └── Dropped all features < 1% importance (56 columns removed)
    │
    └── 5️⃣  Model Training & Submission
            │
            ▼
📊 Clean Data (16 features) → 🤖 XGBoost → 📤 Kaggle Submission
```

---

## 🤖 Model Configuration

```python
XGBRegressor(
    n_estimators=400,     # 🌲 Number of trees
    learning_rate=0.07,   # 📉 Step size shrinkage
    max_depth=3,          # 📏 Max tree depth
    random_state=42       # 🎲 Reproducibility
)
```

---

## 📈 Model Performance

| Metric | Train | Test |
|:---|:---:|:---:|
| **R² Score** | 0.955 | 0.903 |
| **Kaggle RMSE (log)** | — | **0.15175** |

> The gap between train and test R² (0.05) is within acceptable range — no significant overfitting detected.

---

## 🛠️ Technologies

<table>
  <tr>
    <td align="center"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" width="40"/><br><b>Python</b></td>
    <td align="center"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/numpy/numpy-original.svg" width="40"/><br><b>NumPy</b></td>
    <td align="center"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/pandas/pandas-original.svg" width="40"/><br><b>Pandas</b></td>
    <td align="center"><img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/matplotlib/matplotlib-original.svg" width="40"/><br><b>Matplotlib</b></td>
    <td align="center"><img src="https://upload.wikimedia.org/wikipedia/commons/0/05/Scikit_learn_logo_small.svg" width="40"/><br><b>Scikit-learn</b></td>
  </tr>
</table>

---

## 🚀 Installation & Usage

```bash
# 1. Clone the repository
git clone https://github.com/AloneMask001/Ames-Housing-XGBoost.git
cd Ames-Housing-XGBoost

# 2. Install dependencies
pip install numpy pandas matplotlib scikit-learn xgboost jupyter

# 3. Run the notebook
jupyter notebook Ames_Advance_DS.ipynb
```

> ⚠️ **Note:** Place `train.csv` and `test.csv` in the same directory as the notebook before running.

---

## 📁 Project Structure

```
Ames-Housing-XGBoost/
│
├── 📓 Ames_Advance_DS.ipynb   # Main analysis & modeling notebook
├── 📊 train.csv                # Training dataset
├── 📊 test.csv                 # Test dataset
├── 📤 submission.csv           # Kaggle submission file
└── 📄 README.md                # Project documentation
```

---

## 👤 Developer

**Semih Erdem Verep**  
2nd Year AI Engineering Student

---

## 📄 License

This project was developed for educational purposes as part of Kaggle's House Prices — Advanced Regression Techniques competition.

---


