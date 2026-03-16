# REIT Value Signal Indicator
 
A Python-based tool that identifies US-listed REITs trading below their estimated intrinsic value, generating actionable value signals for personal trading decisions.
 
## Thesis
 
Real Estate Investment Trusts publish detailed financial statements that allow estimation of Net Asset Value (NAV) per share. When a REIT's market price trades at a significant discount to estimated NAV — and the discount is not explained by deteriorating fundamentals — this represents a potential value opportunity.
 
This tool automates the detection of such mispricings across a curated universe of 28 US-listed REITs spanning six sub-sectors.
 
## Universe
 
| Sub-Sector | Tickers | Count |
|---|---|---|
| Residential | AVB, ESS, MAA | 3 |
| Office | BXP, KRC, VNO, SLG | 4 |
| Industrial | PLD, EGP, FR, STAG, REXR | 5 |
| Retail | SPG, O, FRT, BRX | 4 |
| Data Centers | EQIX, DLR, IRM | 3 |
| Self-Storage | PSA, EXR, CUBE | 3 |
| **Total** | | **22 tickers** |
 
Selection criteria: US-listed, market cap > $1B, publicly traded since at least 2015, sufficient liquidity and data availability.
 
## Methodology
 
### NAV Estimation
- **Primary approach:** Adjusted book value with cap-rate adjustments
- **Inputs:** Quarterly balance sheet data (total assets, liabilities, property values, debt breakdown), FFO/AFFO, shares outstanding
- **Output:** Estimated NAV per share for each REIT
 
### Signal Generation
- Core signal: NAV discount/premium = (Market Price – Estimated NAV) / Estimated NAV
- Quality filters: Debt-to-equity, interest coverage, FFO payout ratio, occupancy trends
- Trend overlay: Moving average filter to avoid catching falling knives
- Composite score: Weighted combination of value + quality + momentum
 
### Validation
- Backtested against VNQ (Vanguard Real Estate ETF) benchmark
- Out-of-sample testing: Train on 2015–2020, test on 2021–2025
- Paper traded for minimum 8 weeks before live deployment
 
## Project Structure
 
```
reit-value-signal/
├── data/
│   ├── raw/           # Raw API pulls stored as CSVs
│   ├── cleaned/       # Cleaned and validated data
│   └── universe.csv   # 28 tickers + metadata
├── models/            # NAV estimation logic
├── signals/           # Signal generation and scoring
├── backtest/          # Backtesting framework
├── notebooks/         # Jupyter notebooks for exploration
├── dashboard/         # Streamlit app for live monitoring
├── tests/             # Unit tests
├── requirements.txt
├── .gitignore
└── README.md
```
 
## Data Sources
 
- **Financial statements:** Financial Modeling Prep API (free tier) / SEC EDGAR
- **Market prices:** Yahoo Finance via `yfinance`
- **Earnings transcripts:** (Phase 6 — AI enhancement layer)
 
## Setup
 
```bash
git clone https://github.com/YOUR_USERNAME/reit-value-signal.git
cd reit-value-signal
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```
 
## Requirements
 
```
pandas
numpy
yfinance
requests
matplotlib
seaborn
jupyter
openpyxl
```
 
## Roadmap
 
- [x] Phase 1: Foundation & data pipeline
- [ ] Phase 2: Valuation engine (NAV model)
- [ ] Phase 3: Signal generation & filtering
- [ ] Phase 4: Backtesting & validation
- [ ] Phase 5: Dashboard & live monitoring
- [ ] Phase 6: AI enhancement layer (optional)
 
## Limitations & Disclaimers
 
- This is a personal research and learning tool, not financial advice.
- NAV estimates are approximations based on publicly available data and simplified assumptions. They will differ from sell-side analyst estimates.
- Past performance of any signal does not guarantee future results.
- All trading decisions remain the sole responsibility of the user.
 
## Author
 
Austin — MSc Finance | Built as a personal trading tool and portfolio project.
 
## License
 
MIT
