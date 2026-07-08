# world-happiness-analysis
# World Happiness Report: Multivariate Analysis & Predictive Modeling

## 📌 Project Overview
This project presents a rigorous statistical and machine learning exploration of the **World Happiness Report (2024)** dataset. The objective is twofold:
1. **Multivariate Statistical Analysis:** Conduct foundational statistical examinations, including Principal Component Analysis (PCA) and foundational hypothesis testing across socio-economic indicators.
2. **Predictive Modeling:** Discretize national happiness levels into categorical classes (*High, Medium, Low*) and evaluate multiple classification algorithms to predict a country's tier based on structural attributes.

---

## 📊 Dataset & Features
The analysis utilizes global development, economic, and social indicators. Key features included in the modeling pipeline are:
* **Target Variable:** `HappyScore` (Discretized into `High`, `Medium`, `Low` tiers)
* **Socio-Economic Predictors:**
    * `log_GDP`: Logarithmic Gross Domestic Product per capita
    * `LifeExp`: Healthy life expectancy at birth
    * `Gini`: Gini index measuring income inequality
    * `Unemp`: Unemployment rate
    * `UrbanPop`: Urbanization population percentage
    * `Trade`: Trade openness indicators
    * `Corrupt`: Perceptions of corruption
    * `InternetUse`: Digital penetration rates

---

## 🛠️ Repository Structure
```text
├── data/
│   └── World_happiness_report_2024.csv    # Cleansed analysis dataset
├── notebooks/
│   └── happiness_analysis.ipynb           # Main Google Colab development notebook
└── README.md                              # Project documentation
