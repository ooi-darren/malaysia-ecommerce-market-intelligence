# Malaysia E-Commerce Market Intelligence Report (2020–2024)

## The Question

How has Malaysia's e-commerce competitive landscape evolved between 2020 and 2024, and what should a business weigh when deciding where to invest?

## Status

✅ **Analysis complete.** Three notebooks, each answering a distinct sub-question, are done and committed. Key findings are summarized below.

## Key Findings

**1. Which customer segment is driving growth?** B2B remains the largest contributor by far (RM879.6 billion in 2024), but B2G is growing fastest (30.5% CAGR, 2021–2024) from a much smaller base. The right investment priority depends on time horizon: B2B for near-term scale, B2G for firms with a longer runway or existing government relationships. *([Notebook 01](./notebooks/01-ecommerce-segment-growth-analysis.ipynb))*

**2. Is B2C growth driven by rising household income?** Household income and B2C e-commerce income happened to share an identical 6.6% CAGR — but their trajectories moved in opposite directions. Income growth was front-loaded (2020–2022) and decelerating; B2C growth was back-loaded and accelerating through 2023–2024. This suggests B2C is increasingly decoupling from income growth — a sign of genuine digital channel shift, not just a wealthier consumer base spending more. *([Notebook 02](./notebooks/02-income-vs-ecommerce-growth.ipynb))*

**3. Which platform is actually winning?** No single metric gives a clean answer. Shopee's search interest has declined steadily since 2021, yet it remains the dominant platform by GMV and scale — likely reflecting habitual, direct-app usage replacing search-driven discovery. TikTok Shop's search interest stayed flat near zero throughout, even as its Malaysia GMV grew 150% in H1 2025 alone — a platform whose real growth search data alone would never reveal. A multi-platform strategy is the more defensible position for most businesses than betting on one. *([Notebook 03](./notebooks/03-platform-competitive-landscape.ipynb))*

## Why This Project

Most public "e-commerce analysis" projects run customer segmentation or sales prediction on generic transactional datasets — a technical exercise with no country or market context. This project takes a different approach: a market-level competitive intelligence report, built the way a consulting analyst would build one, using official public data rather than a Kaggle download.

## Data Sources

Every dataset is labeled **PUBLIC** (official government source), **DERIVED** (compiled by the author from public sources), or **ESTIMATED** (third-party market research, not government-verified). Full definitions and known limitations are documented in [`DATA_DICTIONARY.md`](./DATA_DICTIONARY.md).

| Dataset | Source | Classification | Frequency |
|---|---|---|---|
| Wholesale & Retail Trade | DOSM (OpenDOSM) | PUBLIC | Monthly |
| External Trade | DOSM (OpenDOSM) | PUBLIC | Monthly |
| Household Income | DOSM (OpenDOSM) | PUBLIC | Biennial survey |
| Household Income by State | DOSM (OpenDOSM) | PUBLIC | Biennial survey |
| E-Commerce Income (2020–2024) | Compiled from 5 DOSM ICTEC/Digital Economy reports | DERIVED | Annual |
| Platform Search Interest | Google Trends | PUBLIC (proxy metric) | Monthly |
| Platform GMV & Traffic | Third-party market research (Momentum Works, Mordor Intelligence, others) | ESTIMATED | Snapshot, 2024–2025 |

## Notebooks

| # | Question | Data Rigor |
|---|---|---|
| [01 — Segment Growth](./notebooks/01-ecommerce-segment-growth-analysis.ipynb) | Which customer segment (B2B/B2C/B2G) is driving growth? | PUBLIC + DERIVED |
| [02 — Income vs. E-Commerce](./notebooks/02-income-vs-ecommerce-growth.ipynb) | Is B2C growth tracking household purchasing power? | PUBLIC + DERIVED |
| [03 — Platform Landscape](./notebooks/03-platform-competitive-landscape.ipynb) | Which platform is actually winning, and what should a business do about it? | PUBLIC proxy + ESTIMATED |

## Methodology

Business problem → objectives → data acquisition → cleaning → analysis → visualization → insight → recommendation. Every notebook opens with the question and the answer, then shows the reasoning between them — including what the data didn't support.

## Repository Structure

```
data/
├── raw/          # Original files, unmodified, as downloaded from source
└── processed/    # Cleaned/compiled datasets ready for analysis
notebooks/        # Analysis notebooks
references/       # Source PDFs and supporting documents
DATA_DICTIONARY.md
```

## Author

Darren Ooi — [LinkedIn](https://www.linkedin.com/in/darrenooizhixian)