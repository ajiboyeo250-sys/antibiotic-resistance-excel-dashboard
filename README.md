Antibiotic Resistance Dashboard (Excel)

An interactive Excel dashboard that shows antibiotic resistance patterns across 2,166 patients and 10,803 antibiotic tests. Built with Power Query, PivotTables, PivotCharts and slicers.

> **Important:** the data is **synthetic**. It was generated for practice and does not describe real patients. The findings below describe this practice data only.

![Dashboard overview, top](dashboard_overview_top.png)
![Dashboard overview, bottom](dashboard_overview_bottom.png)

What this project shows

- Cleaning a messy dataset in Power Query and recording every fix
- Reshaping data (unpivot) so one pivot can compare several antibiotics
- Building pivot tables and charts, then linking them with slicers
- Designing a dark-themed dashboard with KPI cards and a findings box

 The data

| Item | Value |
|---|---|
| Source | Synthetic practice dataset |
| Rows (raw) | 2,200 |
| Columns | 13 |
| Rows after cleaning | 2,166 patients |
| Antibiotic tests | 10,803 (after reshaping) |

Columns: Patient_ID, Age, Gender, Region, Hospital_Ward, Collection_Date, Amoxicillin, Ciprofloxacin, Meropenem, Vancomycin, Colistin, Test_Method, Resistance_Genes.

The data was made messy on purpose: inconsistent labels, impossible ages, text dates, blanks and duplicate rows.

 Cleaning log (Power Query)

| Problem found | Fix | Why |
|---|---|---|
| 34 duplicate rows | Remove Duplicates on Patient_ID (2,200 to 2,166 rows) | One row per patient |
| Gender written as M, F, male, FEMALE, with spaces | Trim, Capitalize Each Word, Replace Values (exact match) | One label per category |
| Antibiotic results written as R, S, resistant, RESISTANT, sensitive | Trim, Capitalize Each Word, Replace Values (exact match) | Pivots and rules need one spelling |
| Region and Test_Method in mixed case with trailing spaces | Trim, Capitalize Each Word, fixed Abuja FCT and MIC | Clean slicers and charts |
| "None", "none", "NONE" and blanks in Resistance_Genes | Replaced with None, gene names left untouched | One category for no gene detected |
| Impossible ages (-3, 0, 215, 999) and blanks | Conditional column: ages below 1 or above 100 set to blank | Bad ages would distort age groups |
| Dates stored as a mix of text and dates | Cut to 10 characters, converted with UK locale (day first) | Real dates allow monthly grouping |

Added columns: **Age_Group** (Under 18, 18-34, 35-49, 50-64, 65+, Unknown) and **Is_Resistant** (1 for Resistant, 0 for Sensitive).

Reshaped table: **Antibiotic_Long** was created by unpivoting the five antibiotic columns into Antibiotic and Result (10,803 rows). Tests with no result are left out.

 Decisions

- Blank ages and blank antibiotic results were **left blank**, not guessed. An invented value would make the rates wrong.
- Blank gene entries were treated as "None". In real data, a blank could mean the test was not done, so this would be checked with the lab first.
- Dates were read day first (dd/mm/yyyy).

What I built

- **KPI cards:** total tests, overall resistance rate, highest-resistance antibiotic
- **Slicers:** Region, Gender, Hospital_Ward, connected to every pivot
- **Charts:** resistance by antibiotic, resistance by gene, monthly resistance rate
- **Key findings box** and a progress tracker sheet

The slicers filter every card and chart. Example with Lagos selected:

![Filtered by Lagos, top](dashboard_lagos_top.png)
![Filtered by Lagos, bottom](dashboard_lagos_bottom.png)

 Key findings (synthetic data)

- Overall resistance rate: **30.6%**
- **Amoxicillin** has the highest resistance (**61.5%**)
- **Colistin** has the lowest (**__%**)
- Patients with a resistance gene show higher resistance than patients with none. The highest gene is **__** (**__%**) and **None** is **__%**
- The monthly rate moved between **__%** and **__%** with no steady trend

These patterns were built into the practice data, so they are not real clinical findings.

 Things I learned and limits

- **Case matters in Power Query.** Pivot tables ignore upper and lower case, but Power Query does not. Labels like "resistant" and "Resistant" gave two different overall rates (30.1% and 30.6%) until I cleaned them.
- Derived columns should be added **after** all the cleaning steps.
- Filtering to very small groups (for example one region, one gender and one ward) leaves few tests, so percentages jump and ties can happen by chance.
- Gene results depend on the synthetic data and should not be read as real.

 Tools

Microsoft Excel: Power Query, PivotTables, PivotCharts, slicers, conditional formatting, data validation.

 Files

- `Antibiotic_Resistance_Dashboard.xlsx`: the workbook with the data, queries, pivots and dashboard
- `dashboard_overview_top.png`, `dashboard_overview_bottom.png`, `dashboard_lagos_top.png`, `dashboard_lagos_bottom.png`: screenshots

Author

Opeyemi Ajiboye. GitHub: ajiboyeo250-sys

