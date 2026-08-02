# Data Dictionary

This document defines every variable used in the Malaysia E-Commerce Market Intelligence Report (2020–2024). Every dataset is classified as **PUBLIC** (published directly by an official source), **DERIVED** (calculated from public data), or **ESTIMATED** (third-party market research, not government-verified).

---

## iowrt.csv

**Source:** Department of Statistics Malaysia (DOSM), OpenDOSM Data Catalogue
**URL:** https://open.dosm.gov.my/data-catalogue/iowrt
**Classification:** PUBLIC
**Frequency:** Monthly
**Coverage used:** Jan 2020 – Dec 2024
**Description:** Malaysia's wholesale & retail trade performance — sales value and volume, published monthly by DOSM.

### Columns

| Column | Type | Description |
|---|---|---|
| `series` | string | Which representation of the data this row holds: `abs` (absolute value), `growth_yoy` (year-on-year % change), or `growth_mom` (month-on-month % change) |
| `date` | date | First day of the reporting month (e.g. `2020-01-01` = January 2020) |
| `sales` | float | Total retail & wholesale sales value, in RM millions |
| `volume` | float | Quantity of goods sold, as an index (base year 2015 = 100), not adjusted for seasonality |
| `volume_sa` | float | Same volume index, seasonally adjusted — use this one for trend analysis |

### Known limitations
- Three `series` values are stacked in the same file — filter to `series == "abs"` before treating `sales`/`volume` as raw numbers, or you'll accidentally mix absolute values with growth percentages in the same chart.

---

## trade_headline.csv

**Source:** Department of Statistics Malaysia (DOSM), OpenDOSM Data Catalogue
**URL:** https://open.dosm.gov.my/data-catalogue/trade_headline
**Classification:** PUBLIC
**Frequency:** Monthly
**Coverage used:** Jan 2020 – Dec 2024
**Description:** Malaysia's monthly external trade in goods — exports, imports, and trade balance.

### Columns

| Column | Type | Description |
|---|---|---|
| `series` | string | Which representation of the data this row holds: `abs` (absolute value), `growth_yoy` (year-on-year % change), or `growth_mom` (month-on-month % change) |
| `date` | date | First day of the reporting month |
| `exports` | float | Total exports (RM) — gross exports before domestic/re-export split |
| `exports_domestic` | float | Exports of goods produced within Malaysia (RM) |
| `re_exports` | float | Exports of goods originally imported, then re-exported without significant processing (RM) |
| `imports` | float | Total imports (RM) |
| `imports_retained` | float | Imports retained for domestic use, excluding goods imported only to be re-exported (RM) |
| `total` | float | Total trade (exports + imports) (RM) |
| `balance` | float | Trade balance (exports − imports); positive = trade surplus |

### Known limitations
- Filter to `series == "abs"` before treating value columns as raw currency figures — same stacking issue as `iowrt.csv`.
- `exports_domestic`, `re_exports`, and `imports_retained` are blank for dates before 2008 (DOSM didn't report that breakdown yet). Not an issue for our 2020–2024 window, but don't reuse this file for anything earlier without accounting for it.

---

## hh_income.csv

**Source:** Department of Statistics Malaysia (DOSM), OpenDOSM Data Catalogue
**URL:** https://open.dosm.gov.my/data-catalogue/hh_income
**Classification:** PUBLIC
**Frequency:** Biennial (survey conducted every 2 years, not annual)
**Coverage used:** 2020, 2022, 2024 (3 data points only — see limitation below)
**Description:** National-level mean and median gross monthly household income in Malaysia, from Malaysia's Household Income & Expenditure Survey (HIES).

### Columns

| Column | Type | Description |
|---|---|---|
| `date` | date | Survey year (Jan 1 of that year, e.g. `2022-01-01` = 2022 survey) |
| `income_mean` | float | Mean gross monthly household income, in RM |
| `income_median` | float | Median gross monthly household income, in RM |

### Known limitations
- **This is not a continuous time series.** The survey runs every 2 years, so within our 2020–2024 window there are only 3 data points (2020, 2022, 2024) — no 2021 or 2023. Do not chart this as a monthly or annual trend line; treat each point as a snapshot, and be explicit in the notebook that gaps between points reflect survey cadence, not missing data collection on our part.

---

## hies_state.csv

**Source:** Department of Statistics Malaysia (DOSM), OpenDOSM Data Catalogue
**URL:** https://open.dosm.gov.my/data-catalogue/hies_state
**Classification:** PUBLIC
**Frequency:** Biennial (survey conducted every 2 years, not annual)
**Coverage used:** 2022, 2024 (2 data points per state only — see limitation below)
**Description:** State-level household income, expenditure, poverty, and income inequality, from Malaysia's Household Income & Expenditure Survey (HIES).

### Columns

| Column | Type | Description |
|---|---|---|
| `date` | date | Survey year (Jan 1 of that year) |
| `state` | string | Malaysian state |
| `income_mean` | float | Mean gross monthly household income, in RM |
| `income_median` | float | Median gross monthly household income, in RM |
| `expenditure_mean` | float | Mean gross monthly household expenditure, in RM |
| `gini` | float | Gini coefficient — income inequality measure, 0 (perfect equality) to 1 (perfect inequality) |
| `poverty` | float | Poverty rate, as a percentage of the state population |

### Known limitations
- Same survey-cadence issue as `hh_income.csv`, but narrower: only 2022 and 2024 are available at state level within our window. Use for before/after state-level comparison, not for a trend line.