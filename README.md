# Cross-Sectional Equity Factor Models: A Negative Result

Walk-forward study of five price-based factors on the S&P 500, 2006–2023.
The signal ranks the cross-section (top decile beats bottom by 1.40%/month),
but the spread is market beta — beta-neutralized, the strategy loses 1.5%/yr.

**[Full paper (PDF)](YOUR_OVERLEAF_LINK)**

`notebooks/01_factor_model.ipynb` — complete analysis, runs end to end
`requirements.txt` — dependencies

Data: Yahoo Finance via yfinance. Universe is current S&P 500 membership,
so the sample is survivor-biased by up to 8.8%/yr (measured in §2.2).
