# Malaysia E-Commerce Market Intelligence Report (2020–2024)

## The Question

How has Malaysia's e-commerce competitive landscape evolved between 2020 and 2024, and what should a business weigh when deciding where to invest?

## Status

🚧 **In progress — data acquisition stage.** Tier 1 macro datasets are collected and documented. Analysis and findings have not started yet — check back for updates, or follow the commit history to see progress as it happens.

## Why This Project

Most public "e-commerce analysis" projects run customer segmentation or sales prediction on generic transactional datasets — a technical exercise with no country or market context. This project takes a different approach: a market-level competitive intelligence report, built the way a consulting analyst would build one, using official public data rather than a Kaggle download.

## Data Sources

All data is sourced from Malaysia's Department of Statistics (DOSM) via the OpenDOSM open data portal, supplemented by official DOSM publications and third-party market intelligence for platform-level detail. Every dataset is labeled **PUBLIC**, **DERIVED**, or **ESTIMATED**, with full definitions and known limitations documented in [`DATA_DICTIONARY.md`](./DATA_DICTIONARY.md).

**Currently collected:**
| Dataset | Source | Frequency |
|---|---|---|
| Wholesale & Retail Trade | DOSM (OpenDOSM) | Monthly |
| External Trade | DOSM (OpenDOSM) | Monthly |
| Household Income | DOSM (OpenDOSM) | Biennial survey |
| Household Income by State | DOSM (OpenDOSM) | Biennial survey |

**Planned:**
- Usage of ICT and E-Commerce by Establishment (DOSM, annual)
- Malaysia Digital Economy report (DOSM, annual)
- Platform-level market intelligence (third-party, ESTIMATED)

## Methodology

Business problem → objectives → data acquisition → cleaning → analysis → visualization → insight → recommendation. Every notebook will open with the question and the answer, then show the reasoning between them — including what the data didn't support.

## Repository Structure

```
data/
├── raw/          # Original files, unmodified, as downloaded from source
└── processed/    # Cleaned datasets ready for analysis
notebooks/        # Analysis notebooks
references/       # Source PDFs and supporting documents
DATA_DICTIONARY.md
```

## Author

Darren Ooi — [LinkedIn](https://www.linkedin.com/in/darrenooizhixian)