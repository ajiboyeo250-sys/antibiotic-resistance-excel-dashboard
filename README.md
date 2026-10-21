 Antibiotic Resistance Dashboard (Excel)

An interactive Excel dashboard that shows antibiotic resistance patterns across 2,166 patients and 10,803 antibiotic tests. Built with Power Query, PivotTables, PivotCharts, and slicers.

> **Important:** The data is **synthetic**. It was generated for practice and does not describe real patients. The findings below describe this practice data only.

 What This Project Shows

- Cleaning a messy dataset in Power Query and recording every fix.
- Reshaping data (unpivot) so one PivotTable can compare several antibiotics.
- Building PivotTables and charts, then linking them with slicers.
- Designing a dark-themed dashboard with KPI cards and a key findings box.

 The Data

| Item | Value |
|---|---|
| Source | Synthetic practice dataset |
| Rows (raw) | 2,200 |
| Columns | 13 |
| Rows after cleaning | 2,166 patients |
| Antibiotic tests | 10,803 (after reshaping) |

**Columns:** Patient_ID, Age, Gender, Region, Hospital_Ward, Collection_Date, Amoxicillin, Ciprofloxacin, Meropenem, Vancomycin, Colistin, Test_Method, Resistance_Genes.

The data was made messy on purpose: inconsistent labels, impossible ages, text dates, blanks, and duplicate rows.

 Cleaning Log (Power Query)

| Problem Found | Fix Applied | Why |
|---|---|---|
| 34 duplicate rows | Removed duplicates using Patient_ID (2,200 to 2,166 rows) | To maintain one row per patient |
| Gender written as M, F, male, FEMALE, with spaces | Trimmed, capitalized, and replaced inconsistent values using exact matches | To ensure one consistent label per category |
| Antibiotic results written as R, S, resistant, RESISTANT, sensitive | Trimmed, capitalized, and replaced inconsistent values using exact matches | To ensure consistent resistance classifications |
| Region and Test_Method in mixed case with trailing spaces | Trimmed, standardized capitalization, and corrected Abuja FCT and MIC labels | To maintain consistent categories in slicers and charts |
| "None", "none", "NONE", and blanks in Resistance_Genes | Replaced variations with None while leaving gene names unchanged | To create a consistent category for no gene detected |
| Impossible ages (-3, 0, 215, 999) and blanks | Created a conditional column to set ages below 1 or above 100 to blank | To prevent invalid ages from distorting age-group analysis |
| Dates stored as a mixture of text and dates | Extracted the first 10 characters and converted dates using the UK locale (day first) | To ensure dates were recognized correctly and could be grouped by month |

 Additional Columns

Two additional columns were created during data transformation:

- **Age_Group:** Under 18, 18–34, 35–49, 50–64, 65+, and Unknown.
- **Is_Resistant:** Assigned 1 to Resistant results and 0 to Sensitive results.

 Data Reshaping

I created a table called `Antibiotic_Long` by unpivoting the five antibiotic columns into two columns:

- `Antibiotic`
- `Result`

The reshaped table contained 10,803 antibiotic test records. Tests without a result were excluded from the reshaped table.

 Decisions Made During Cleaning

- Blank ages and blank antibiotic results were **left blank**, not guessed. Inventing values would make the calculated rates inaccurate.
- Blank gene entries were treated as "None". In real data, a blank could mean the test was not done, so this would need to be checked with the laboratory first.
- Dates were interpreted using the day-first format (dd/mm/yyyy).

 What I Built

 Key Performance Indicators (KPIs)

- Total antibiotic tests
- Overall resistance rate
- Antibiotic with the highest resistance rate

 Interactive Slicers

The dashboard includes slicers for:

- Region
- Gender
- Hospital_Ward

The slicers are connected to the dashboard's PivotTables and visualizations, allowing users to explore different subsets of the data.

 Charts and Visualizations

- Resistance rate by antibiotic
- Resistance patterns by resistance gene
- Monthly resistance rate trends
- KPI cards
- A key findings box

A progress tracker sheet was also included to document the project workflow.

 Key Findings (Synthetic Data)

The analysis of the synthetic dataset showed:

- Overall resistance rate: **30.6%**
- **Amoxicillin** had the highest resistance rate at **61.5%**.
- **Colistin** had the lowest resistance rate. The exact percentage is not included here because it has not been provided.
- Patients with a resistance gene showed higher resistance than patients with none. The highest-resistance gene and its percentage have not been specified here.
- The monthly resistance rate varied over time, with no steady trend. The exact minimum and maximum percentages have not been specified here.

These patterns describe the synthetic practice data only. They should not be interpreted as real clinical findings or used to make medical decisions.

 Things I Learned and Project Limitations

 1. Case Sensitivity in Power Query

PivotTables ignore differences between uppercase and lowercase labels in certain comparisons, but Power Query transformations can treat differently written text as separate categories.

Labels such as `resistant` and `Resistant` initially produced different overall resistance rates (30.1% and 30.6%) until the labels were standardized.

 2. The Order of Data Transformation Matters

Derived columns should be added after the relevant cleaning steps have been completed. This helps ensure that calculated categories and metrics use consistent data.

 3. Small Groups Can Produce Unstable Percentages

Filtering to very small groups, such as one region, one gender, and one hospital ward, leaves fewer tests. Percentages can change significantly, and ties can occur by chance.

 4. Synthetic Data Has Limitations

The resistance patterns and gene associations depend on how the practice dataset was generated. They should not be interpreted as real-world clinical evidence.

 Tools Used

**Microsoft Excel**
- Power Query
- PivotTables
- PivotCharts
- Slicers
- Conditional formatting
- Data validation

 Skills Demonstrated

- Data cleaning and preprocessing
- Data transformation using Power Query
- Data validation
- Handling missing and inconsistent values
- Data reshaping using unpivot
- Exploratory data analysis
- PivotTable and PivotChart development
- Interactive dashboard design
- Data visualization
- Analytical thinking
- Communicating findings through data

 Project Files

The repository contains the project files and supporting materials used to build the dashboard, including the Excel workbook and dashboard screenshots.

Explore the repository to review the available files and project materials.

 Author

**Opeyemi Ajiboye**

GitHub: [@ajiboyeo250-sys](https://github.com/ajiboyeo250-sys)
