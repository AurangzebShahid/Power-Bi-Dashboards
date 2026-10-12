# ACS-IR: Data Monitoring Dashboard (Power BI)

A Power BI dashboard used to monitor data quality and study progress in **ACS-IR**, a WHO-funded implementation research trial in Pakistan evaluating antenatal corticosteroid use for preterm birth. It sits at the end of a pipeline: field data → Stata cleaning and QC → analysis dataset → this dashboard.

> **Only a small synthetic sample is included for demonstration. No real study data is in this repository.** See [Data]((https://github.com/AurangzebShahid/Power-Bi-Dashboards/blob/main/Full_database_analysis_P2_LONG_M_PK.xlsx).
> 
## What it does

The dashboard gives the data management team a weekly view of whether data collection is on track and whether the records look right, by cluster, facility and month.

| Area | Examples of what is monitored |
|---|---|
| **Overview** | Deliveries recorded, form completion, enrolment by cluster and study arm, month-on-month trend |
| **Delivery form (BDF) quality** | Mode of delivery, gestational age assessment, birthweight, ANC booking status, completeness and out-of-range values |
| **Gestational age and ultrasound** | Earliest-USG coverage, USG timing vs admission, provider GA vs USG GA agreement (±7 days), preterm classification |
| **Birthweight** | Weight categories, provider-preterm vs weight-preterm agreement, missed preterm (<2,000 g) |
| **ACS administration** | Antenatal corticosteroid coverage, dose timing relative to delivery |
| **Follow-up (NFU / MNFU)** | Pending, completed and lost-to-follow-up visits, overdue windows, by cluster |
| **Timeliness** | Delay between delivery and form submission |

[Overview](https://github.com/AurangzebShahid/Power-Bi-Dashboards/blob/main/Screenshots/Overview.png)
## Design

- **Four-arm-per-side cluster design**: clusters are grouped by study arm so intervention and control sites can be compared side by side.
- **Flags, not corrections.** Each page highlights records that need a field query (for example, a USG recorded after admission); data is corrected at source, not in the report.
- **Conditional formatting** follows a fixed scheme: dark red below 80%, light red up to 95%, green at 95% and above.

## Repository structure

```
├── Phase 2 Data Monitoring Dashboard.pbip          # Power BI project entry point
├── Phase 2 Data Monitoring Dashboard.Report/       # Report pages and visuals (PBIR format)
├── Phase 2 Data Monitoring Dashboard.SemanticModel/# Data model: tables, relationships, measures
└── docs/
    └── screenshots/                                # Anonymised screenshots
```

**Model tables:** `Dataset Long` (one row per delivery), `Dataset Wide` and `Project Timeliness`.

**DAX highlights:** caesarean-section rate, maternal age bins, birthweight categories, provider-vs-weight preterm agreement (provider only / weight only / both), missed preterm births, and follow-up pending-time buckets.

## Data

The dashboard reads a de-identified analysis dataset produced by the Stata pipeline (see the companion repository, [ACS-IR-](https://github.com/AurangzebShahid/ACS-IR-)). The dataset is not shared because it contains participant-level trial data.

To run the report on your own copy:

1. Open the `.pbip` in Power BI Desktop (current release; the project uses the PBIR report format).
2. Open **Transform data** and edit the `Source` step of each query to point at your analysis dataset.
3. Refresh. Column names are expected to match the analysis dataset (for example `BDF_GA_WEEKS`, `BDF_BIRTH_WEIGHT`, `MNFU_STATUS`).

## Requirements

- Power BI Desktop (recent release, with the PBIR/PBIP project format enabled)
- The analysis dataset (not included)

## Author

**Aurangzeb Shahid**, Data Manager, ACS-IR trial.
[GitHub](https://github.com/AurangzebShahid)

## Acknowledgements

Developed for the ACS-IR implementation research trial. Study sponsor, partners and clinical teams are credited in the trial protocol.

## License

Code and report definition: [choose a license, e.g. MIT]. This does not cover trial data, which is not distributed.
