# Cross-Sectional Equity Factor Models: Real Signal, Zero Alpha

Walk-forward study of five price-based factors on the S&P 500 (2006–2023, 2.0M stock-day observations).

**[Full paper (PDF)](paper.pdf)** · **[Notebook](notebooks/01_factor_model.ipynb)** (runs end to end)

## Key results
- **Only realized volatility predicts returns.** IC 0.043 (t ≈ 2.84). All three momentum variants are indistinguishable from zero.
- **Multicollinearity was hiding the signal.** Two factors correlate at ρ = 0.91, and Ridge assigned them large opposing coefficients that cancel. Removing three redundant factors nearly doubled out-of-sample IC (0.024 → 0.045) and raised positive folds from 71% to 86%.
- **The ranking power is real, but the money is beta.** The top decile beats the bottom by 1.40%/month, but the spread is explained by a long-leg beta of ≈1.3 vs. a short-leg beta of ≈0.6. Beta-neutralized and net of costs, the portfolio returns −1.46%/yr (Sharpe −0.20).

Figures: [decile returns](figures/deciles.pdf) · [equity curves](figures/equity_curves.pdf)

## Method
- Cross-sectionally rank-normalized factors: long-horizon momentum, short-term reversal, realized volatility, volatility-scaled momentum, medium-horizon momentum
- 14 rolling walk-forward folds with 21-day purged train/test boundaries (no look-ahead leakage)
- Models: Ridge regression and XGBoost, evaluated on per-date Spearman information coefficient
- Beta-neutral long-short decile portfolio with transaction costs

## Caveat
The universe is current S&P 500 membership, so the sample is survivor-biased. The paper measures this at roughly 9 percentage points per year (§2.2).

## Stack
Python · pandas · NumPy · scikit-learn · XGBoost · statsmodels · SciPy · SHAP · yfinance

```bash
pip install -r requirements.txt
jupyter notebook notebooks/01_factor_model.ipynb
```
