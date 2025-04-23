# 📈 IV Skew Trading Strategy

**Author:** Vishruth Anand  
**Date:** April 2025  
**Repo Goal:**  
Use implied volatility skew and VIX term structure to predict SPY returns via both rule-based and machine learning strategies.

---

## 📊 Summary

This project explores whether the **SKEW index percentile** and **VIX / VIX3M slope** contain predictive power over **1-month SPY returns**. Strategies are evaluated in a **volatility-targeted** framework (10% annualized target), with performance assessed via **Sharpe ratio**, **CAGR**, and **hit rate**. Logistic regression is used to assess the marginal value of statistical learning over handcrafted rules.

---

## 🧠 Strategy Breakdown

| Strategy                        | Sharpe | CAGR  | Hit Rate |
| ------------------------------- | ------ | ----- | -------- |
| Naïve Skew (Rule-Based)         | 0.12   | 0.76% | 21.6%    |
| Continuous Z-Score Strategy     | 0.77   | 0.3%  | 18.8%    |
| Logistic Regression (In-Sample) | 1.09   | --    | --       |
| Logistic Regression (OOS)       | 0.78   | 7.5%  | 64.0%    |

> 🔒 **Vol-targeted returns** ensure fair risk-adjusted comparison.

---

## 🧭 Notebook Outline

1. **Setup & Data Ingestion**  
   Load historical VIX, VIX3M, and SKEW data from local CSVs.

2. **Feature Engineering**  
   Compute:

   - Skew percentile (1-year rolling)
   - VIX / VIX3M slope
   - SPY 1-month forward returns

3. **Naïve Skew-Only Strategy**  
   Long if skew < 20th percentile, short if > 80th.

4. **Continuous Strategy (Z-Score)**  
   Multiply z-scored slope × skew percentile (flipped sign), clamp, and grid search thresholds.

5. **Logistic Regression Model**  
   Classify next-month SPY direction based on skew + slope.

6. **Out-of-Sample Diagnostics**  
   ROC curve, classification metrics, and return breakdown.

---

## 🗂️ Files

| File                               | Description                     |
| ---------------------------------- | ------------------------------- |
| `notebooks/iv_skew_strategy.ipynb` | Full end-to-end notebook        |
| `data/`                            | Local CSVs for SKEW, VIX, VIX3M |
| `README.md`                        | Project overview (this file)    |

---

## ✅ Next Steps

- Add new features (e.g. realized vol, options volume)
- Try tree-based classifiers or logistic ensemble models
- Backtest on sector ETFs or higher-frequency data

---

> Feel free to fork, run your own ideas, or get in touch if you'd like to collaborate.
