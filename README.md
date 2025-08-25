# 📘 End-to-End ML Project – README
---
## Project Structure 

### Workflows--ML Pipeline

1. Data Ingestion
2. Data Validation
3. Data Transformation-- Feature Engineering,Data Preprocessing
4. Model Trainer
5. Model Evaluation- MLFLOW,Dagshub

## Workflows

1. Update config.yaml
2. Update schema.yaml
3. Update params.yaml
4. Update the entity
5. Update the configuration manager in src config
6. Update the components
7. Update the pipeline 
8. Update the main.py


---



## 🚀 Overview

This project demonstrates a **complete end-to-end Machine Learning workflow** implemented with modular coding practices.
It covers **data ingestion, validation, transformation, model training, evaluation, and deployment** via a Flask application.
The goal is to provide a **production-ready ML pipeline** with reusability, scalability, and maintainability.

---

## 📂 Project Structure

```
project/
│── src/
│   ├── components/         # Individual pipeline components
│   ├── pipelines/          # Training & prediction pipelines
│   ├── utils/              # Common utility functions
│   ├── logger/             # Custom logging
│   └── exception/          # Exception handling
│── artifacts/              # Stored data, models, transformers
│── config/                 # Configuration files (YAML, constants)
│── app.py                  # Flask app for serving predictions
│── requirements.txt        # Dependencies
│── setup.py                # Project packaging
```

---

## 🛠️ Environment & Setup

1. **Clone Repo & Install Packages**

   ```bash
   git clone <repo_url>
   cd project
   pip install -r requirements.txt
   ```

2. **Set Up Environment Variables**

   * Create a `.env` file with DB credentials, S3 keys, etc.

3. **Initialize Project**

   ```bash
   python setup.py install
   ```

---

## 🧩 Pipeline Stages

### 1. 🔧 Project Initialization & Utilities

* **Modules Added**:

  * `logger.py`: Centralized logging system.
  * `exception.py`: Custom error handling.
  * `common.py`: Utility functions (read/write YAML, create directories, save/load objects).
* **Purpose**: Foundation for reusability across all stages.

---

### 2. 📥 Data Ingestion

* **Steps**:

  * Connect to **MongoDB** / external source.
  * Create **feature store** (raw dataset).
  * Perform **train-test split**.
  * Save ingested data to `artifacts/ingested_data/`.
* **Artifacts Produced**:

  * `train.csv`, `test.csv`.

---

### 3. ✅ Data Validation

* **Config-driven validation**:

  * Schema checks (column names, datatypes, number of columns).
  * Missing values, duplicates handling.
  * Report generation in `validation_report.json`.
* **Artifacts**:

  * Validation status file.

---

### 4. 🔄 Data Transformation

* **Transformations Applied**:

  * Encoding categorical variables.
  * Standardization/scaling of numerical features.
  * Feature engineering & pipeline building.
* **Artifacts**:

  * Preprocessor object (`preprocessor.pkl`).
  * Transformed train/test arrays.

---

### 5. 🏋️ Model Training

* **Implemented Models**:

  * Linear Regression, Random Forest, Gradient Boosting, XGBoost, etc.
* **Steps**:

  * Train models with hyperparameters.
  * Save best-performing model with preprocessor.
* **Artifacts**:

  * `model.pkl` (final trained model).
  * Training logs & metrics.

---

### 6. 📊 Model Evaluation

* **Metrics Evaluated**:

  * R² Score, MAE, RMSE, Accuracy (depending on regression/classification task).
* **Process**:

  * Compare multiple models.
  * Select best model and store evaluation report.
* **Artifacts**:

  * Evaluation JSON/CSV reports.

---

### 7. 🌐 Model Deployment (Flask App)

* **Flask API** (`app.py`) serves:

  * **/predict** endpoint → Takes input JSON → Returns predictions.
* **Steps**:

  * Load preprocessor + model.
  * Pass request data through transformation.
  * Generate predictions.

Run locally:

```bash
python app.py
```

API Request Example:

```bash
curl -X POST http://127.0.0.1:5000/predict \
-H "Content-Type: application/json" \
-d '{"feature1": value1, "feature2": value2}'
```

---

## 📦 Artifacts Flow

1. **Raw Data** → `artifacts/data_ingestion/`
2. **Validated Data** → `artifacts/data_validation/`
3. **Transformed Data** → `artifacts/data_transformation/`
4. **Trained Model + Preprocessor** → `artifacts/model_trainer/`
5. **Evaluation Reports** → `artifacts/model_evaluation/`

---

## 🛡️ Logging & Monitoring

* **Custom logger** writes logs to both console and file.
* Tracks:

  * Pipeline start/end.
  * Errors/exceptions.
  * Metrics & artifacts created.


