# EffiCombatEngine

## Overview
EffiCombatEngine is an AI-driven system designed for **real-time health monitoring of military aircraft engines** using the NASA C-MAPSS dataset.  
Developed during an internship at **WireOT Pvt Ltd**, the project focuses on predictive maintenance by detecting anomalies, classifying engine health states, and estimating Remaining Useful Life (RUL) to enhance operational safety and mission readiness in military aviation.

---

## Features
- **Real-Time Engine Health Monitoring**  
  Uses time-series sensor data from turbofan engines to assess current engine status.
- **Anomaly Detection**  
  Statistical detection of abnormal sensor readings using a threshold-based approach.
- **Remaining Useful Life (RUL) Estimation**  
  Predicts the number of operational cycles before failure.
- **Lightweight Deployment**  
  Optimized for resource-constrained military devices.
- **Visualization Tools**  
  Plots sensor trends, anomaly points, and RUL distributions.

---

## Technologies Used
- **Programming Language:** Python 3.12.7  
- **Libraries:**
  - `pandas` – Data manipulation
  - `numpy` – Numerical computations
  - `scikit-learn` – Data preprocessing & ML utilities
  - `TensorFlow/Keras` – Neural network model development
  - `matplotlib` – Data visualization

---

## Dataset
- **Source:** NASA C-MAPSS (FD001 subset)  
- **Description:** Sensor readings from 100 simulated turbofan engines under various operational settings.
- **Structure:**
  - `train_FD001.txt` – Training data
  - `test_FD001.txt` – Test data
  - `RUL_FD001.txt` – Remaining useful life values for test engines

---

## Methodology

### 1. Data Preprocessing
- Load and structure sensor data with appropriate column names.
- Normalize features using **StandardScaler**.
- Label engine cycles as:
  - **Healthy** if RUL > 70% of total life
  - **Failing** otherwise

### 2. Engine Condition Classification
- **Model:** Multi-Layer Perceptron (MLP)
  - Input: 24 features (3 settings + 21 sensors)
  - Hidden Layers: 64 → 32 neurons (ReLU activation)
  - Output: Sigmoid (binary classification)
- Achieved **~80% validation accuracy**.

### 3. Anomaly Detection
- Calculate mean and standard deviation for each sensor in healthy engines.
- Flag anomalies when readings exceed `mean + 3 × std`.
- Identify “weird sensors” and use anomaly counts to refine classifications.

### 4. RUL Analysis
- Use `RUL_FD001.txt` to estimate engine lifespans.
- Set failure threshold at **10 cycles**.
- Integrate with anomaly detection for final engine classification.

---

## Results
- **Final Classification:**
  - Healthy Engines: 68
  - Failing Engines: 32
- **Model Performance:**
  | Model        | Accuracy | Precision | F1 Score | Notes |
  |--------------|----------|-----------|----------|-------|
  | MLP (Final)  | 80%      | 78%       | 79%      | Used in final analysis |
  | CatBoost     | 70%      | 65%       | 67%      | Struggled with time-series data |
  | LightGBM     | 71%      | 66%       | 68%      | Struggled with time-series data |
  | Autoencoder  | 68%      | 62%       | 65%      | Poor anomaly reconstruction |

---

## Hardware & Software Requirements
- **Hardware:**  
  - MacBook M2, 8GB RAM, 256GB storage  
- **Software:**  
  - macOS Ventura 13.0  
  - Python 3.12.7  
  - Anaconda (environment management)  
  - Jupyter Notebook  

---

## Learning Outcomes
- Enhanced skills in **time-series analysis**, **machine learning**, and **statistical anomaly detection**.
- Experience in model selection, feature engineering, and visualization.
- Improved professional skills including teamwork, communication, and problem-solving in a real-world aerospace AI project.

---

## Future Improvements
- Integrate **GPU acceleration** for faster model training.
- Explore **XGBoost** or **LSTM** models for improved RUL prediction.
- Deploy as an **edge AI application** for real-time monitoring in operational aircraft.

---

## Author
**Rahul N G**  
B.E. in Artificial Intelligence and Data Science  
Nitte Meenakshi Institute of Technology, Bengaluru  
Machine Learning Intern at WireOT Pvt Ltd

---

## References
- NASA Ames Prognostics Data Repository – Turbofan Engine Degradation Simulation Dataset
- Gardner, M. W., & Dorling, S. R. (1999). Statistical Methods for Anomaly Detection in Time-Series Data.
- Li, C., & Thompson, R. (2020). Deep Learning for Predictive Maintenance in Aerospace.

