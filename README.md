# 📖 Credit Risk Pipeline

This document outlines the end-to-end framework, methodology, and execution phases implemented within the credit risk prediction pipeline.

---

## Phase 1: Project Setup & Scoping (Steps 1–3)

* **Step 1: Define Business Objectives**  
  Establish the core credit risk modeling targets, focusing on minimizing false negatives (defaulting customers predicted as safe) while balancing the financial impact of false positives.
* **Step 2: Initialize Git Repository**  
  Set up the remote GitHub repository structure, establish branching strategies, and configure `.gitignore` rules to exclude sensitive data files and virtual environments.
* **Step 3: Configure Environment**  
  Establish a dedicated Python virtual environment and compile a comprehensive `requirements.txt` tracking all core libraries including `pandas`, `numpy`, `scikit-learn`, and `openpyxl`.

---

## Phase 2: Data Ingestion & Inspection (Steps 4–7)

* **Step 4: Load Raw Data**  
  Ingest the raw dataset `merged_customer_data.xlsx` into the workspace memory using robust data ingestion tools.
* **Step 5: Verify Dimensions**  
  Confirm structural dimensions, ensuring the dataset conforms to the expected shape of 100 rows and 34 columns.
* **Step 6: Inspect Data Types**  
  Validate schema types across all features, explicitly categorizing text strings, categorical flags, and continuous or discrete numerical variables.
* **Step 7: Quality Assurance Check**  
  Perform a primary uniqueness audit to verify zero duplicate rows exist within the customer records.

---

## Phase 3: Data Cleaning & Integrity (Steps 8–11)

* **Step 8: Missing Value Audit**  
  Scan all 34 features systematically to identify any null, missing, or malformed data entries.
* **Step 9: Numerical Imputation**  
  Apply robust numerical imputation techniques (such as median or mean substitution) if any gaps are discovered in continuous variables.
* **Step 10: Categorical Imputation**  
  Handle missing categorical strings by injecting explicit placeholder markers or mode-based fill strategies.
* **Step 11: Outlier Detection**  
  Inspect numerical distributions using Interquartile Range (IQR) analysis to isolate extreme financial anomalies or data collection errors.

---

## Phase 4: Exploratory Data Analysis (EDA) (Steps 12–15)

* **Step 12: Numerical Summarization**  
  Calculate central tendencies, standard deviations, and range limits across all quantitative financial indicators.
* **Step 13: Categorical Distribution**  
  Analyze frequency tables and proportion splits across qualitative attributes like education level, marital status, and payment history classifications.
* **Step 14: Target Variable Analysis**  
  Evaluate the class distribution of the target variable `Default_y`, confirming the baseline class imbalance (70% non-defaults vs. 30% defaults).
* **Step 15: Correlation Analysis**  
  Generate correlation matrices to uncover potential multicollinearity issues and identify strong linear dependencies with the target label.

---

## Phase 5: Feature Engineering & Preprocessing (Steps 16–20)

* **Step 16: Categorical Feature Identification**  
  Isolate structural text features such as `Marital_Status`, `Education_Level`, and multi-tier payment history variables.
* **Step 17: Feature Encoding**  
  Transform qualitative text data into numerical arrays using optimal strategies like One-Hot Encoding or ordinal mapping.
* **Step 18: Domain-Specific Engineering**  
  Derive advanced financial ratios, credit utilization metrics, or aggregate risk indices to enrich predictive power.
* **Step 19: Distribution Transformation**  
  Apply logarithmic or power-scaling transformations to heavily skewed continuous attributes to normalize data shapes.
* **Step 20: Feature Scaling**  
  Standardize numerical variables using `StandardScaler` to ensure uniform feature magnitudes for distance- and gradient-based algorithms.

---

## Phase 6: Data Splitting & Strategy (Steps 21–23)

* **Step 21: Feature-Target Separation**  
  Isolate the feature matrix X (the 34 input dimensions) from the target label vector y (`Default_y`).
* **Step 22: Stratified Train-Test Split**  
  Partition data into an 80% training set and a 20% testing set while enforcing stratification on `Default_y` to maintain the 70:30 class ratio.
* **Step 23: Leakage Prevention Check**  
  Verify that all data transformation parameters (such as scalers and encoders) are fitted strictly on the training partition and applied independently to the test partition.

---

## Phase 7: Baseline Model Training (Steps 24–27)

* **Step 24: Algorithm Selection**  
  Select baseline classification algorithms, including Logistic Regression for linear separation and Random Forest for non-linear interactions.
* **Step 25: Hyperparameter Initialization**  
  Establish initial default configurations and regularization parameters for the chosen baseline models.
* **Step 26: Model Training**  
  Fit the baseline classifiers using the preprocessed training dataset.
* **Step 27: Cross-Validation**  
  Execute k-fold cross-validation across training subsets to measure score stability and guard against early-stage overfitting.

---

## Phase 8: Model Evaluation & Optimization (Steps 28–31)

* **Step 28: Performance Metric Tracking**  
  Evaluate model output using robust classification metrics, prioritizing ROC-AUC, Precision, Recall, and F1-Score over raw accuracy due to class imbalance.
* **Step 29: Confusion Matrix Analysis**  
  Analyze classification errors in detail, mapping false positives (lost business opportunities) against false negatives (high-risk defaults).
* **Step 30: Hyperparameter Tuning**  
  Execute systematic Grid Search or Randomized Search strategies to optimize key parameters and maximize validation performance.
* **Step 31: Champion Model Selection**  
  Select the final top-performing model based on cross-validated evaluation benchmarks and business risk tolerances.

---

## Phase 9: Deployment & Documentation (Steps 32–34)

* **Step 32: Model Serialization**  
  Save the finalized model pipeline, feature encoders, and scalers into serialized artifacts using `joblib`.
* **Step 33: Inference Scripting**  
  Develop a standalone scoring script capable of ingesting raw external customer records, executing the preprocessing pipeline, and outputting default probability scores.
* **Step 34: Repository Finalization**  
  Complete comprehensive project documentation, establish operational execution guides, and finalize the repository structure for release.
