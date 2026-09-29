# 📈 Leakage-Free LSTM Evaluation for Next-Day Stock Opening-Price Forecasting

## 🔬 Overview

This repository contains the experimental code and supporting materials for the research study:

**“A Leakage-Free, Walk-Forward Evaluation of a Two-Layer Long Short-Term Memory Network for Next-Day Stock Opening-Price Forecasting Against Naive and Statistical Benchmarks”**

The study provides a rigorous and leakage-free evaluation of a **two-layer Long Short-Term Memory (LSTM)** network for next-day stock opening-price forecasting. Rather than proposing a new LSTM architecture, the study focuses on **evaluation methodology, benchmark comparison, statistical validation, and realistic out-of-sample assessment**.

The experiments use daily opening-price data for five large technology stocks:

* 🚗 **Tesla (TSLA)**
* 📦 **Amazon (AMZN)**
* 🔎 **Alphabet/Google (GOOG)**
* 🖥️ **NVIDIA (NVDA)**
* 💻 **Microsoft (MSFT)**

The dataset covers approximately **June 2010 to October 2025**, subject to stock-specific availability.

The forecasting framework uses the previous **30 trading days of opening prices** to predict the next trading day's opening price. The evaluation is designed to prevent information leakage by maintaining chronological separation between training, validation, and test observations and by fitting preprocessing steps using training data only.

---

## 🎯 Research Objective

The primary objective is to determine whether a two-layer LSTM provides **genuine out-of-sample forecasting value** for next-day stock opening prices when evaluated under a strict, leakage-free framework.

The study specifically examines whether apparently strong price-level metrics, such as high \(R^2\), translate into meaningful predictive performance when compared against:

* Persistence/random-walk forecasts
* Drift forecasts
* Seasonal-naive forecasts
* Exponential smoothing
* Holt's method
* ARIMA
* Linear regression

The analysis therefore emphasizes **benchmark-relative performance rather than standalone accuracy metrics**.

---

## 🧠 Forecasting Framework

The main model is a **two-layer LSTM** trained using a rolling historical window of the previous **30 trading days** of opening prices.

The experimental design incorporates:

* 📅 Chronological train/validation/test splitting
* 🔒 Training-only feature scaling
* ⏱️ Validation-based early stopping
* 🎲 Multiple random seeds
* 🔄 Rolling-origin benchmark forecasting
* 📊 Statistical forecast-comparison tests
* 🚶 Expanding-window walk-forward evaluation
* 📉 Return-based error analysis
* 📈 Directional-accuracy analysis
* 🌡️ Volatility-regime analysis
* 💰 Transaction-cost-adjusted trading analysis
* ⚙️ Hyperparameter sensitivity analysis
* 🧪 Model ablation analysis

This design is intended to reduce common sources of optimistic bias in time-series forecasting experiments.

---

## 📊 Key Findings

The results demonstrate an important distinction between **high price-level fit** and **useful forecasting skill**.

### 💡 Price-Level Accuracy

For four of the five stocks, the LSTM achieved very high price-level fit:

* **\(R^2 \geq 0.970\)**
* **MAPE ≤ 3.24%**

However, NVIDIA produced substantially weaker results:

* **\(R^2 = 0.336\)**
* **MAPE = 25.06%**

These results illustrate that strong price-level metrics do not necessarily imply that a forecasting model provides meaningful predictive information.

### 📏 Comparison with Persistence

When compared against the persistence/random-walk benchmark, the LSTM did **not** outperform the benchmark for any of the five stocks.

The reported **Theil's U2 values ranged from 1.055 to 13.632**, where values above 1 indicate worse performance than the persistence benchmark.

### 📐 Diebold–Mariano Testing

Statistical forecast-comparison testing further showed that the LSTM performed significantly worse than persistence for **24 of the 25 trained networks**.

This provides a benchmark-relative statistical assessment beyond simple price-level accuracy metrics.

### 🧭 Directional Accuracy

Directional accuracy ranged from approximately:

**44.9%–53.3%**

This indicates limited ability to consistently predict the direction of the next-day price movement.

### 🔄 Walk-Forward Evaluation

Under expanding-window walk-forward evaluation, **Theil's U2 remained greater than 1 for all 20 stock-fold combinations** reported in the study.

This provides additional evidence that the apparent price-level forecasting accuracy did not translate into improvement over the persistence benchmark under repeated out-of-sample evaluation.

### 🧪 Ablation Analysis

The parameter-matched **one-layer LSTM** was more accurate than the two-layer LSTM in the reported comparison.

However, it also failed to outperform the persistence benchmark.

---

## 🔬 Main Research Message

The central finding of the study is that:

> **High price-level \(R^2\) should not, by itself, be interpreted as evidence of useful forecasting skill in non-stationary financial time series.**

Because stock prices are highly persistent, a model can obtain strong price-level accuracy while providing little or no improvement over a simple persistence/random-walk forecast.

The study therefore emphasizes the importance of:

**Leakage-free evaluation → strong baseline comparison → statistical testing → walk-forward validation**

rather than relying solely on conventional regression metrics.

---

## 📂 Repository Contents

```text
📦 Repository
│
├── 📓 SIGMA_Stock_Revision_Experiments.ipynb
├── 📄 README.md
├── 📄 requirements.txt
├── 📄 .gitignore
│
├── 📁 data/
│   └── dataset_metadata / data description
│
├── 📁 figures/
│   └── generated figures used in the study
│
└── 📁 tables/
    └── generated result tables
```

The repository is intended to contain the **research code and reproducibility materials** associated with the study.

Generated experiment outputs, temporary files, large run directories, and manuscript/reviewer-response working documents should generally not be included unless specifically required for reproducibility.

---

## 💻 Notebook

The primary experimental notebook is:

**`SIGMA_Stock_Revision_Experiments.ipynb`**

It contains the experimental workflow used for the study, including model training, benchmark evaluation, statistical analysis, sensitivity analysis, ablation experiments, walk-forward evaluation, and supporting analyses.

The notebook can be opened directly using **Jupyter Notebook**, **JupyterLab**, or compatible notebook environments.

---

## 📊 Data

The experiments use daily stock-market data for:

| Ticker | Company         |
| ------ | --------------- |
| TSLA   | Tesla           |
| AMZN   | Amazon          |
| GOOG   | Alphabet/Google |
| NVDA   | NVIDIA          |
| MSFT   | Microsoft       |

The study uses **daily opening prices**, with the analysis covering approximately **June 2010 through October 2025**, depending on stock-specific data availability.

The experimental workflow retrieves market data programmatically and applies chronological processing before model training and evaluation.

---

## 🔒 Leakage-Free Evaluation

A central component of this research is the prevention of information leakage.

The evaluation framework maintains temporal ordering and ensures that information from future observations is not used during model development.

Important components include:

1. 📅 Chronological data splitting
2. 🔒 Training-only preprocessing/scaling
3. 🧪 Validation-based model selection
4. 🚫 No random shuffling across temporal observations
5. 🔄 Rolling-origin benchmark forecasts
6. 📈 Expanding-window walk-forward evaluation
7. 📊 Out-of-sample statistical comparison

These procedures are particularly important for financial time-series experiments, where random splitting or inappropriate preprocessing can produce overly optimistic results.

---

## ⚖️ Benchmark Models

The LSTM is evaluated against several conventional forecasting approaches:

| Benchmark                 | Description                                         |
| ------------------------- | --------------------------------------------------- |
| Persistence / Random Walk | Uses the most recent observed value as the forecast |
| Drift                     | Forecast based on historical drift                  |
| Seasonal Naive            | Seasonal benchmark forecast                         |
| Exponential Smoothing     | Exponential smoothing-based forecast                |
| Holt                      | Trend-aware exponential smoothing                   |
| ARIMA                     | Autoregressive integrated moving-average model      |
| Linear Regression         | Regression-based benchmark                          |

The **persistence/random-walk model** serves as a particularly important reference because of the strong persistence commonly present in stock-price levels.

---

## 📐 Evaluation Metrics

The study evaluates performance using multiple complementary measures, including:

* **R²**
* **MAPE**
* **MAE**
* **RMSE**
* **Theil's U2**
* **Directional accuracy**
* **Return-based forecast errors**
* **Statistical forecast-comparison tests**
* **Walk-forward performance**
* **Transaction-cost-adjusted trading measures**

No single metric is treated as sufficient evidence of forecasting usefulness.

---

## 📈 Statistical Evaluation

In addition to conventional prediction-error metrics, the study applies statistical forecast-comparison procedures to determine whether differences between forecasting approaches are statistically meaningful.

The **Diebold–Mariano test** is used to compare forecast errors between the LSTM and benchmark forecasts.

This helps distinguish apparent differences in numerical accuracy from differences supported by statistical testing.

---

## 🔄 Walk-Forward Evaluation

The study additionally uses **expanding-window walk-forward evaluation** to assess whether model performance persists when the model is repeatedly evaluated on future observations using only information that would have been available at the time.

This provides a more realistic assessment of deployment-like forecasting performance than a single static train/test split.

---

## ⚙️ Sensitivity and Ablation Analysis

The repository also supports additional experiments designed to examine the robustness of the reported results.

### Hyperparameter Sensitivity

The effect of selected model/training configurations is examined to determine whether conclusions depend strongly on specific parameter choices.

### Ablation Analysis

A parameter-matched **one-layer LSTM** is compared with the main **two-layer LSTM** configuration.

This helps evaluate whether additional network depth provides measurable forecasting benefits.

---

## 💰 Trading Analysis

The study also examines whether forecast information translates into trading-related performance.

The analysis includes:

* Directional signals
* Return-based evaluation
* Transaction costs
* Trading performance under the forecasting framework

This provides an additional perspective because predictive accuracy at the price level does not necessarily imply economically useful trading performance.

---

## 🛠️ Installation

Clone the repository:

```bash
git clone <YOUR-GITHUB-REPOSITORY-URL>
cd <YOUR-REPOSITORY-NAME>
```

Create a Python environment:

```bash
python -m venv .venv
```

Activate the environment.

### Windows

```bash
.venv\Scripts\activate
```

### macOS / Linux

```bash
source .venv/bin/activate
```

Install the required packages:

```bash
pip install -r requirements.txt
```

---

## 📦 Requirements

The main Python packages used by the experimental workflow include:

```text
numpy
pandas
scipy
matplotlib
tensorflow
scikit-learn
statsmodels
yfinance
python-docx
psutil
```

The exact environment may depend on the Python and TensorFlow versions used to execute the notebook.

---

## ▶️ Running the Experiments

After installing the dependencies, launch Jupyter:

```bash
jupyter notebook
```

or:

```bash
jupyter lab
```

Open:

```text
SIGMA_Stock_Revision_Experiments.ipynb
```

Run the notebook sequentially to reproduce the experimental workflow.

Because the notebook contains model training and multiple experiments, execution time and computational requirements may vary depending on hardware and configuration.

---

## 🧪 Reproducibility

The study emphasizes reproducibility through:

* Fixed chronological evaluation procedures
* Multiple random seeds
* Explicit benchmark definitions
* Training-only preprocessing
* Walk-forward evaluation
* Statistical forecast comparison
* Documented experimental settings

Results may show small numerical differences across environments because of differences in software versions, hardware, numerical libraries, data-provider revisions, or stochastic training behavior.

---

## 📚 Research Context

This repository accompanies the research paper examining whether a two-layer LSTM can provide meaningful next-day stock opening-price forecasts when evaluated against simple and statistical benchmarks under a strict leakage-free framework.

The work is motivated by the observation that neural forecasting models can achieve apparently strong accuracy on highly persistent financial price series, while their incremental value relative to simple baselines may remain limited.

Accordingly, the study places greater emphasis on **benchmark-relative and out-of-sample evidence** than on standalone price-level metrics.

---

## 🎓 Citation

If you use this repository, code, experimental design, or results in your research, please cite the associated paper.

**Paper title:**

> A Leakage-Free, Walk-Forward Evaluation of a Two-Layer Long Short-Term Memory Network for Next-Day Stock Opening-Price Forecasting Against Naive and Statistical Benchmarks

Citation details can be updated here once the final publication information, DOI, journal, and bibliographic details are available.

---

## 📜 License

Add the appropriate license for the repository before publication.

For example:

```text
MIT License
```

if an MIT license is selected.

---

## ⚠️ Disclaimer

This repository is intended for **academic research and reproducibility purposes**.

The forecasts, analyses, and trading-related results presented in this repository should not be interpreted as financial advice or as recommendations to buy or sell securities.

---

## 👤 Author

**Preetha**

Research repository accompanying the study on leakage-free LSTM evaluation for stock-price forecasting.

---

## ⭐ Acknowledgment

This repository is provided to support **transparency, reproducibility, and independent evaluation** of the experimental methodology and findings reported in the associated research study.

---

### 🔗 Repository Summary

**A reproducible, leakage-free evaluation of a two-layer LSTM for next-day stock opening-price forecasting against naive and statistical benchmarks.**
