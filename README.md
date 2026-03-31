# 🧬 Microgravity-Induced Muscle Atrophy Detection using Machine Learning

## 🚀 Overview

This project builds a **machine learning pipeline** to classify muscle samples as **Normal or Atrophied** using **high-dimensional gene expression data**.

The system integrates:

* Feature selection for dimensionality reduction
* Ensemble learning for robust classification
* Gradio interface for real-time prediction

---

## 📊 Dataset

* **Source:** NCBI GEO (GSE148152)
* **Samples:** 40
* **Original Features:** ~70,500 genes
* **Final Features:** 60

The dataset simulates microgravity conditions through prolonged bed rest, capturing gene-level changes in muscle tissue 

---

## ⚙️ Data Preprocessing & Feature Engineering (Core Strength)

Handling gene expression data is challenging due to **high dimensionality (p >> n problem)**.

### 🔹 1. Data Cleaning

* Extracted expression matrix from GEO series file
* Parsed metadata (group, subject, timepoint)
* Removed non-informative columns
* Ensured **no missing values** in final dataset

---

### 🔹 2. Normalization

* Applied **StandardScaler (Z-score normalization)**
* Ensures:

  * Mean = 0
  * Variance = 1
* Prevents bias toward high-magnitude genes

---

### 🔹 3. Outlier Handling

* Used **Interquartile Range (IQR) clipping**
* Reduces effect of extreme gene expression values
* Improves model stability

---

### 🔹 4. Dimensionality Reduction (Critical Step)

#### Step 1: Statistical Filtering (Paired t-test)

* Compared **paired samples (Pre vs Post condition)**
* Selected **top ~1000 statistically significant genes**
* Removes noise while preserving biological relevance

#### Step 2: Boruta Feature Selection

* Wrapper method built on Random Forest
* Compares real features with **shadow features**
* Retains only **truly important genes**

👉 Final reduction:
**70,500 → 1,000 → 60 features** 

---

### 🔹 5. Train-Test Strategy

* **Train:** 36 samples
* **Test:** 4 unseen samples
* Used **Stratified 5-Fold Cross Validation**

  * Maintains class balance
  * Prevents overfitting

---

## 🧠 Model Development

### Models Used:

* Random Forest
* XGBoost
* Support Vector Machine (RBF Kernel)

### Final Model:

👉 **Voting Ensemble Classifier**

Reason:

* Combines diverse learning patterns
* Improves robustness and generalization

---

## 📈 Performance

| Model         | Accuracy   | Precision  | Recall     | AUC      |
| ------------- | ---------- | ---------- | ---------- | -------- |
| Random Forest | 91.6%      | 93.5%      | 91.8%      | 0.99     |
| XGBoost       | 88.9%      | 90.8%      | 89.1%      | 0.93     |
| SVM (RBF)     | **97.78%** | **98.33%** | **97.78%** | **1.00** |

Best model: **SVM (RBF Kernel)** 

---

## 🌐 Deployment

Gradio-based interface:

* Input: Gene expression CSV
* Output: Classification (Normal / Atrophied)
* Displays feature importance (SHAP)

---

## 📸 Interface Preview

<img width="1257" height="620" alt="Screenshot 2026-03-31 141802" src="https://github.com/user-attachments/assets/f9be7240-ee8b-4e7e-8378-00e323be5150" />


---

## 🛠️ Tech Stack

* Python
* scikit-learn
* XGBoost
* BorutaPy
* Gradio

---

## 🎯 Key Highlights

* Solved **high-dimensional biological data problem**
* Reduced features by **>99.9% without losing signal**
* Achieved **~98% accuracy**
* Built **interpretable + deployable ML system**

