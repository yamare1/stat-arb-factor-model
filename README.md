# Statistical Arbitrage & ML Factor Models

## Overview
End-to-end equity factor research system on the S&P 500 universe. Builds and compares linear (Ridge) and nonlinear (XGBoost) factor models to predict 1-month forward returns, constructs a dollar-neutral long-short portfolio, and evaluates performance using institutional metrics.

## Results
| Metric | Value |
|--------|-------|
| Aggregate IC (Ridge) | 0.109 |
| Aggregate IC (XGBoost) | 0.107 |
| Walk-Forward IC (XGBoost) | 0.060 |
| Gross Sharpe (Monthly Rebal) | 2.88 |
| Net Sharpe (after costs) | 2.82 |
| Total Return (2022–2023) | 143.63% |

## Factors
| Factor | Type | SHAP Rank |
|--------|------|-----------|
| Volatility (21d) | Risk | 1 |
| Vol-Adjusted Momentum | Momentum | 2 |
| Short-term Reversal | Mean Reversion | 3 |
| 3-Month Momentum | Momentum | 4 |
| Debt-to-Equity | Fundamental | 5 |
| P/B Ratio | Fundamental | 6 |
| P/E Ratio | Fundamental | 7 |
| Earnings Growth | Fundamental | 8 |
| 12-1 Month Momentum | Momentum | 9 |

## Key Findings
1. **Linear vs Nonlinear**: Ridge and XGBoost achieve nearly identical IC, suggesting largely linear factor relationships in large-cap U.S. equities
2. **Low-Vol Anomaly**: Volatility is the dominant factor — consistent with Frazzini & Pedersen (2014)
3. **Momentum Decay**: Classic 12-1 momentum shows near-zero IC across all horizons in the post-2019 period
4. **Fundamentals**: Adding fundamental factors improves Ridge IC from 0.109 → 0.118; debt-to-equity is the strongest fundamental signal
5. **Transaction Costs**: Daily rebalancing is unviable (Sharpe: 2.48 → -37.35); monthly rebalancing reduces drag to 4.5% over 2 years
6. **Regime Dependence**: Strategy achieves 6.51 Sharpe in low-vol regimes vs 1.11 in medium-vol regimes

## Structure

stat-arb-factor-model/
├── notebooks/
│ └── 01_factor_model.ipynb # Main analysis
├── data/ # Raw price + fundamental data (gitignored)
├── src/ # Source modules
├── requirements.txt
└── README.md


## Setup
```bash
git clone https://github.com/yamare1/stat-arb-factor-model.git
cd stat-arb-factor-model
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
jupyter notebook
```

## Dependencies
- pandas, numpy — data manipulation
- yfinance — market data
- scikit-learn — Ridge regression, preprocessing
- xgboost — gradient boosting
- shap — model interpretability
- hmmlearn — Hidden Markov Model regime detection
- matplotlib, seaborn — visualization

## Limitations
- Survivorship bias in S&P 500 constituent selection
- Fundamental data is a current snapshot, not point-in-time
- No options-based hedging during high-vol regimes

## References
- Frazzini, A. & Pedersen, L. (2014). Betting Against Beta. *Journal of Financial Economics*
- Fama, E. & French, K. (1993). Common Risk Factors in Stock Returns. *Journal of Financial Economics*
