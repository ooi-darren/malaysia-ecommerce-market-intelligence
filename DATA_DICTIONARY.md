# Data Dictionary

This document defines every variable used in the Malaysia E-Commerce Market Intelligence Report (2020–2024). Every dataset is classified as **PUBLIC** (published directly by an official source), **DERIVED** (calculated from public data), or **ESTIMATED** (third-party market research, not government-verified).

---

## iowrt.csv

**Source:** Department of Statistics Malaysia (DOSM), OpenDOSM Data Catalogue
**URL:** https://open.dosm.gov.my/data-catalogue/iowrt
**Classification:** PUBLIC
**Frequency:** Monthly
**Coverage used:** Jan 2020 – Dec 2024
**Description:** Malaysia's wholesale & retail trade performance: sales value and volume, published monthly by DOSM.

### Columns

| Column | Type | Description |
|---|---|---|
| `series` | string | Which representation of the data this row holds: `abs` (absolute value), `growth_yoy` (year-on-year % change), or `growth_mom` (month-on-month % change) |
| `date` | date | First day of the reporting month (e.g. `2020-01-01` = January 2020) |
| `sales` | float | Total retail & wholesale sales value, in RM millions |
| `volume` | float | Quantity of goods sold, as an index (base year 2015 = 100), not adjusted for seasonality |
| `volume_sa` | float | Same volume index, seasonally adjusted; use this one for trend analysis |

### Known limitations
- Three `series` values are stacked in the same file: filter to `series == "abs"` before treating `sales`/`volume` as raw numbers, or you'll accidentally mix absolute values with growth percentages in the same chart.

---

## trade_headline.csv

**Source:** Department of Statistics Malaysia (DOSM), OpenDOSM Data Catalogue
**URL:** https://open.dosm.gov.my/data-catalogue/trade_headline
**Classification:** PUBLIC
**Frequency:** Monthly
**Coverage used:** Jan 2020 – Dec 2024
**Description:** Malaysia's monthly external trade in goods: exports, imports, and trade balance.

### Columns

| Column | Type | Description |
|---|---|---|
| `series` | string | Which representation of the data this row holds: `abs` (absolute value), `growth_yoy` (year-on-year % change), or `growth_mom` (month-on-month % change) |
| `date` | date | First day of the reporting month |
| `exports` | float | Total exports (RM); gross exports before domestic/re-export split |
| `exports_domestic` | float | Exports of goods produced within Malaysia (RM) |
| `re_exports` | float | Exports of goods originally imported, then re-exported without significant processing (RM) |
| `imports` | float | Total imports (RM) |
| `imports_retained` | float | Imports retained for domestic use, excluding goods imported only to be re-exported (RM) |
| `total` | float | Total trade (exports + imports) (RM) |
| `balance` | float | Trade balance (exports − imports); positive = trade surplus |

### Known limitations
- Filter to `series == "abs"` before treating value columns as raw currency figures, same stacking issue as `iowrt.csv`.
- `exports_domestic`, `re_exports`, and `imports_retained` are blank for dates before 2008 (DOSM didn't report that breakdown yet). Not an issue for our 2020–2024 window, but don't reuse this file for anything earlier without accounting for it.

---

## hh_income.csv

**Source:** Department of Statistics Malaysia (DOSM), OpenDOSM Data Catalogue
**URL:** https://open.dosm.gov.my/data-catalogue/hh_income
**Classification:** PUBLIC
**Frequency:** Biennial (survey conducted every 2 years, not annual)
**Coverage used:** 2020, 2022, 2024 (3 data points only. See limitation below)
**Description:** National-level mean and median gross monthly household income in Malaysia, from Malaysia's Household Income & Expenditure Survey (HIES).

### Columns

| Column | Type | Description |
|---|---|---|
| `date` | date | Survey year (Jan 1 of that year, e.g. `2022-01-01` = 2022 survey) |
| `income_mean` | float | Mean gross monthly household income, in RM |
| `income_median` | float | Median gross monthly household income, in RM |

### Known limitations
- **This is not a continuous time series.** The survey runs every 2 years, so within our 2020–2024 window there are only 3 data points (2020, 2022, 2024), no 2021 or 2023. Do not chart this as a monthly or annual trend line; treat each point as a snapshot, and be explicit in the notebook that gaps between points reflect survey cadence, not missing data collection on our part.

---

## hies_state.csv

**Source:** Department of Statistics Malaysia (DOSM), OpenDOSM Data Catalogue
**URL:** https://open.dosm.gov.my/data-catalogue/hies_state
**Classification:** PUBLIC
**Frequency:** Biennial (survey conducted every 2 years, not annual)
**Coverage used:** 2022, 2024 (2 data points per state only. See limitation below)
**Description:** State-level household income, expenditure, poverty, and income inequality, from Malaysia's Household Income & Expenditure Survey (HIES).

### Columns

| Column | Type | Description |
|---|---|---|
| `date` | date | Survey year (Jan 1 of that year) |
| `state` | string | Malaysian state |
| `income_mean` | float | Mean gross monthly household income, in RM |
| `income_median` | float | Median gross monthly household income, in RM |
| `expenditure_mean` | float | Mean gross monthly household expenditure, in RM |
| `gini` | float | Gini coefficient: income inequality measure, 0 (perfect equality) to 1 (perfect inequality) |
| `poverty` | float | Poverty rate, as a percentage of the state population |

### Known limitations
- Same survey-cadence issue as `hh_income.csv`, but narrower: only 2022 and 2024 are available at state level within our window. Use for before/after state-level comparison, not for a trend line.

---

## ecommerce_income.csv

**Source:** Compiled by author from five DOSM publications (see `references/`)
**Classification:** DERIVED
**Frequency:** Annual
**Coverage:** 2020–2024
**Description:** Malaysia's e-commerce transaction income, manually extracted and combined from five separate DOSM ICTEC and Digital Economy report PDFs, since no single official release covers the full 2020–2024 window.

### Columns

| Column | Type | Description |
|---|---|---|
| `year` | int | Reference year |
| `income_rm_billion` | float | Total e-commerce transaction income (RM billion) |
| `domestic_rm_billion` | float | Income from domestic market (RM billion) |
| `international_rm_billion` | float | Income from international market (RM billion) |
| `b2b_rm_billion` | float | Business-to-Business income (RM billion) |
| `b2c_rm_billion` | float | Business-to-Consumer income (RM billion) |
| `b2g_rm_billion` | float | Business-to-Government income (RM billion) |
| `source_document` | string | Which PDF in `references/` this row's figures came from |

### Known limitations
- 2020 breakdown columns (domestic/international/B2B/B2C/B2G) are blank, the source document for that year only reported the headline total.
- 2022 and 2023 totals are corroborated by two independent DOSM publications each; 2020, 2021, and 2024 rely on a single publication.
- Figures were manually transcribed from PDF text, not programmatically parsed.

---

## multiTimeline.csv

**Source:** Google Trends (trends.google.com)
**Classification:** PUBLIC (proxy metric. See limitations)
**Frequency:** Monthly
**Coverage:** Jan 2020 – Dec 2025
**Description:** Relative search interest for "Shopee," "Lazada," and "TikTok Shop" in Malaysia. Used as a free, directly-downloadable proxy for consumer attention in notebook 03.

### Columns

| Column | Type | Description |
|---|---|---|
| `month` | date | First day of the reporting month |
| `shopee` | int | Search interest index for "Shopee," relative to the peak value across all three terms and the full date range (0–100) |
| `lazada` | int | Search interest index for "Lazada," same relative scale |
| `tiktok_shop` | int | Search interest index for "TikTok Shop," same relative scale. Original `<1` values converted to `0`. |

### Known limitations
- **Relative, not absolute.** Values represent search interest relative to the peak within this specific comparison, a score of "40" cannot be interpreted in isolation, and cannot be compared to a Trends export from a different query.
- **Structurally understates TikTok Shop.** TikTok Shop's discovery-driven model (algorithmic feed, in-app livestreams) means users transact without searching for the platform by name; its real usage and GMV growth (confirmed independently at +150% in H1 2025) are not reflected in this search-interest data. See notebook 03 for the full discussion.
## Context / Secondary Sources (Qualitative)

Each notebook's "Why Is This Happening?" section adds secondary-sourced explanation (industry/news reporting) for the mechanism behind that notebook's finding, not new PUBLIC/DERIVED/ESTIMATED datasets, so kept separate from the tables above.

- MalaysiaTenders / public procurement reporting on ePerolehan scale and adoption; used in Notebook 01. https://www.malaysiatenders.com/public-procurement.php
- PayNet, "8.44bil transactions processed in 2025 as digital payments become Malaysians' preferred way to pay"; used in Notebook 02. https://www.paynet.my/about-us/media-centre/press-release/8-44-billion-transactions-processed-in-2025-as-digital-payments-become-malaysians-preferred-way-to-pay.html
- Digital in Asia, "How Did TikTok Shop Grow in Southeast Asia? A 2026 Analysis"; used in Notebook 03. https://digitalinasia.com/tiktok-shop-southeast-asia-growth-10x/
- North Ridge Partners, "Live Commerce Examined: TikTok Takes Over in Southeast Asia"; used in Notebook 03. https://www.northridgepartners.com/content-news/live-commerce-examined-tiktok-takes-over
