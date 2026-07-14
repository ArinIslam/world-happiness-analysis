# Synthetic Health Metrics Generator & Anomaly Detector

This repository contains a Python pipeline designed to synthesize, preprocess, and analyze time-series health metrics. It simulates realistic physiological data, introduces common sensor artifacts alongside critical clinical anomalies, cleans the dataset, and applies a rule-based anomaly detection engine.

---

## Data Generation & Simulation

Since real-world clinical data is highly protected, this tool synthetically builds a realistic health telemetry dataset from scratch using `numpy` and `pandas`:

* **Base Time-Series:** Generates **2,000 hourly timestamps** starting from `2025-01-01`.
* **Physiological Baselines:** Uses normal distributions to model healthy human baselines:
  * **Heart Rate:** $\sim\mathcal{N}(75, 10)$ bpm
  * **Systolic Blood Pressure (BP):** $\sim\mathcal{N}(120, 15)$ mmHg
  * **Diastolic Blood Pressure (BP):** $\sim\mathcal{N}(80, 10)$ mmHg
  * **Oxygen Saturation ($SpO_2$):** $\sim\mathcal{N}(98, 1)$ %
  * **Temperature:** $\sim\mathcal{N}(36.8, 0.3)$ °C
* **Clinical Anomalies:** Artificially injects severe physiological anomalies (e.g., sudden fever, spikes/drops in blood pressure, tachycardia, and hypoxia) into **3%** of the dataset.
* **Sensor Imperfections:** 
  * Introduces **5% random missing values** across all vital signs to simulate connection drops.
  * Adds random white Gaussian noise to represent minor sensor measurement inaccuracies.
* **Safety Clipping & Rounding:** Restricts values within realistic medical boundaries (e.g., $SpO_2$ cannot exceed 100% or drop below 70%) and rounds them to typical clinical precision.

---

## Data Preprocessing

The raw generated dataset is cleaned and prepared using the following steps:
1. **Feature Extraction:** Converts timestamps to datetime objects and extracts helper columns (`Date` and `Hour`).
2. **Imputation:** Missing data points are resolved using **linear time interpolation** to maintain smooth transitions over the time-series, followed by backward/forward filling for any boundary edge cases.

---

## Main Results

### 1. Summary Statistics (Post-Imputation)

| Vital Sign | Mean | Median | Min | Max | Std Dev |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Heart Rate** | 75.02 | 75.0 | 40.0 | 129.0 | 11.30 |
| **Blood Pressure (Systolic)** | 119.80 | 120.0 | 70.0 | 205.0 | 16.39 |
| **Blood Pressure (Diastolic)** | 80.41 | 80.0 | 40.0 | 135.0 | 10.61 |
| **Oxygen Saturation ($SpO_2$)** | 97.75 | 98.0 | 86.0 | 100.0 | 1.76 |
| **Temperature (°C)** | 36.81 | 36.8 | 34.0 | 40.4 | 0.53 |

### 2. Anomaly Detection Performance
Using predefined clinical thresholds (e.g., $SpO_2 < 92\%$, Heart Rate $> 120$ or $< 50$ bpm, Temp $> 38.5$°C, or Blood Pressure $\ge 180/\ge 120$), the engine flags critical events:
* **Normal Readings:** 1,933 frames
* **Flagged Anomalies:** 67 frames ($\sim 3.35\%$ of the dataset)

---

## Getting Started

### Prerequisites
Make sure you have the following packages installed:
```bash
pip install pandas numpy matplotlib seaborn
