# NAICS Budget and Diversity Insights

An interactive Power BI dashboard for IMEX Cargo to track updated NAICS codes using cleaned historical data and live API sources, supporting trade compliance, business registration, and market analysis.

---

## Introduction

This project helps IMEX Cargo, a North American freight forwarding company focused on trade with the Middle East and North Africa, analyze federal contract activity through a structured data pipeline and interactive dashboard. We collected NAICS codes from historical files and live government sources, cleaned and standardized the data, and joined it with budget and diversity records. The resulting Power BI dashboard allows IMEX Cargo to:

- Ensure accurate business registration under correct NAICS codes
- Monitor budget execution against allocated federal funds
- Evaluate supplier diversity (woman-, minority-, and veteran-owned)
- Identify new market opportunities based on trade and industry patterns

With daily refresh capability, this dashboard provides real-time decision support for compliance, outreach, and growth strategies.


The dashboard enables IMEX Cargo to track industry changes, register companies accurately, and identify new market opportunities.

---

## Usage and Purpose

IMEX Cargo can use this NAICS data platform for:

- Business registration with government entities like SAM (System for Award Management), where up to 5–10 NAICS codes may be assigned.
- Simplifying trade documentation through accurate industry classification for customs and tariff compliance.
- Market research by identifying potential customers, competitors, and trade partners in global markets.

By using NAICS-based analytics, IMEX can streamline operations and improve outreach strategies.

---

## Key Tasks and Plan

This project involved three main phases:

1. Data collection from historical files and government APIs
2. Data cleaning and transformation across multiple sources
3. Visualizing the processed data in Power BI

---

## Schema and Cleaning Highlights

- All `naics_code` fields were padded to six digits.
- Dollar values were normalized for arithmetic operations.
- Agency and recipient names were upper-cased and trimmed.
- Incomplete or blank NAICS rows were removed.
- Portfolio spending was aggregated for benchmarking.
- Ownership flags in the recipients table were converted to numeric (1/0) for boolean logic.

---

## Analytical Views

1. **PTAC × Recipients View**: Combines awards with diversity flags to identify small and diverse businesses.
2. **PTAC × DLA × Portfolio View**: Computes budget execution ratios by combining allocated, transactional, and historical spend.
3. **Diversity Scorecard View**: Categorizes NAICS × agency combinations as High, Medium, or Low diversity based on contract shares.
4. **export_contracts_analysis Table**: Combines all logic into a single fact table with industry sector breakdown.

---

## Join Workflow and Power BI Model

- All joins are based on the cleaned and padded `naics_code`.
- Recipients are joined using normalized `recipient_name` (future upgrade will use CAGE or UEI).
- Inside Power BI, a star schema connects the `export_contracts_analysis` fact table with three dimension tables: agency, recipient, and NAICS.

DAX measures are used to calculate metrics like Budget Execution % and Diversity Share %.

---

## Limitations

- Name-based joins may miss matches until CAGE/UEI is implemented.
- Some contracts (pre-2012) lack dollar values, limiting trend analysis.
- API rate limits require overnight caching for timely updates.
- Outlier spending affects execution rate metrics; future versions may include smoothing techniques.

---

## Conclusion

The system helps IMEX Cargo monitor NAICS-related activity, flag budget performance issues, track supplier concentration, and assess inclusion efforts. With daily data refreshes and interactive filtering, the dashboard offers a reliable decision-support tool for trade, compliance, and outreach planning.

