# Loan Default & Credit Risk Analysis

**MySQL · Python · Power BI | Vehicle Finance & First-EMI Default Analytics**

An end-to-end analytics project examining **233,154 vehicle loan records** to understand first-EMI defaults, evaluate credit risk indicators, and identify borrower segments with elevated default rates. The analysis combines SQL-based data extraction, Python data preparation and exploratory analysis, and a **two-page interactive Power BI dashboard** for portfolio and credit risk monitoring.

## Business Challenge

Vehicle lenders must balance loan growth with credit quality. Identifying how financing terms, borrower characteristics, bureau classifications, and existing repayment histories relate to early defaults can help prioritize credit policy reviews and portfolio monitoring.

This project addresses five questions:

- What proportion of disbursed loans defaulted on the first EMI?
- How do loan-to-value (LTV) ratios and disbursed loan amounts relate to default rates?
- Which bureau risk categories and credit-history characteristics show elevated defaults?
- How are previously defaulted accounts, recent delinquencies, and credit inquiries associated with first-EMI defaults?
- How does portfolio performance vary across employment types, age groups, states, and branches?

## Results at a Glance

| Metric | Result |
| --- | ---: |
| Vehicle loans analyzed | **233,154** |
| Original dataset attributes | **41** |
| First-EMI defaults | **50,611** |
| Loans without first-EMI default | **182,543** |
| Overall first-EMI default rate | **21.71%** |
| Total amount disbursed | **₹1,267.36 crore** |
| Average disbursed loan amount | **₹54,356.99** |
| Loans without bureau history | **116,950 (50.16%)** |

**Metric scope:** `loan_default = 1` identifies a first-EMI default, not a lifetime default or a fully written-off loan. Total disbursement represents original loan principal, **not realized credit losses**.

## Dashboard

### Page 1 — Loan Portfolio Overview

![Loan Portfolio Overview dashboard](assets/loan_portfolio_overview.png)

The portfolio page displays loan volumes, disbursement value, average loan size, first-EMI default count and rate, and comparisons by **LTV, age, loan-size quartile, and employment type**.

### Page 2 — Credit Risk & Default Analysis

![Credit Risk and Default Analysis dashboard](assets/credit_risk_default_analysis.png)

The credit risk page examines **bureau risk classifications, previously defaulted primary accounts, credit inquiries, active primary accounts, and recently opened accounts**, alongside bureau-history segment KPIs. Both pages use **state, employment type, and disbursement date** slicers to support filtered portfolio analysis.

## Key Findings

### Loan-to-value (LTV) and first-EMI defaults

| LTV band | Total loans | First-EMI defaults | Default rate |
| --- | ---: | ---: | ---: |
| 0–60% | 26,089 | 3,627 | **13.90%** |
| 60–70% | 39,573 | 7,009 | **17.71%** |
| 70–80% | 85,604 | 18,827 | **21.99%** |
| 80–90% | 81,005 | 20,966 | **25.88%** |
| 90–100% | 883 | 182 | **20.61%** |

The default rate increases from **13.90%** in the lowest LTV band to **25.88%** in the 80–90% band, a difference of **11.98 percentage points**. The 90–100% group contains only **883 loans**, so its lower observed rate should be interpreted cautiously.

### Credit bureau risk classification

| Bureau risk category | Loans | Defaults | Default rate |
| --- | ---: | ---: | ---: |
| Very Low Risk | 50,728 | 8,018 | **15.81%** |
| Low Risk | 18,294 | 3,366 | **18.40%** |
| Medium Risk | 12,412 | 3,173 | **25.56%** |
| High Risk | 12,025 | 3,248 | **27.01%** |
| Very High Risk | 9,910 | 2,991 | **30.18%** |
| No Bureau History | 116,950 | 27,052 | **23.13%** |
| Not Scored | 12,835 | 2,763 | **21.53%** |

Very High Risk borrowers record a **30.18%** first-EMI default rate, compared with **15.81%** for Very Low Risk borrowers. **116,950 loans** have no available bureau history; this segment must be analyzed separately rather than treating an absent/zero score as an ordinary low credit score.

### Existing primary-account defaults

| Defaulted primary accounts at disbursement | Loans | First-EMI defaults | Default rate |
| --- | ---: | ---: | ---: |
| 0 | 206,879 | 43,408 | **20.98%** |
| 1 | 19,970 | 5,382 | **26.95%** |
| 2+ | 6,305 | 1,821 | **28.88%** |

Borrowers with **2+ previously defaulted primary accounts** record a **28.88%** first-EMI default rate versus **20.98%** among borrowers with none. In the dataset dictionary, *primary* refers to accounts taken by the borrower for personal use; the overdue-account fields represent accounts already in default at disbursement.

### Credit inquiries and recent delinquencies

| Credit inquiries | Loans | First-EMI defaults | Default rate |
| --- | ---: | ---: | ---: |
| 0 | 201,961 | 42,557 | **21.07%** |
| 1 | 22,285 | 5,441 | **24.42%** |
| 2 | 5,409 | 1,491 | **27.57%** |
| 3+ | 3,499 | 1,122 | **32.07%** |

The first-EMI default rate rises from **21.07%** among borrowers with no recorded credit inquiries to **32.07%** among those with **3+ inquiries**.

Recent delinquency is a separate measure: borrowers with **0, 1, and 2+ defaulted accounts in the preceding six months** record first-EMI default rates of **21.25%, 26.90%, and 27.97%**, respectively.

### Loan size and borrower characteristics

| Loan amount quartile | Loans | Average disbursement | Default rate |
| --- | ---: | ---: | ---: |
| Q1 — Smallest | 58,537 | ₹39,884 | **15.93%** |
| Q2 | 58,676 | ₹50,679 | **20.64%** |
| Q3 | 57,734 | ₹56,895 | **24.58%** |
| Q4 — Largest | 58,207 | ₹70,102 | **25.74%** |

The observed default rate increases across loan-size quartiles, from **15.93%** for Q1 to **25.74%** for Q4. This describes a group-level pattern and does not mean that an individual larger loan will necessarily default.

Additional segmentation findings:

- **Age:** The 18–25 group records **23.88%** first-EMI defaults, compared with **18.02%** for borrowers aged 56+.
- **Employment:** Self-employed borrowers record **22.77%**, salaried borrowers **20.35%**, and borrowers with unknown employment type **21.46%**.
- **Active primary accounts:** Borrowers with **3+ active primary credit accounts** record **18.01%**, compared with **22.66%** among those with none.
- **Geography:** `State_ID = 13` records **30.66%** first-EMI defaults across **17,884 loans**. State identifiers are retained as codes; no unverified state-name mapping is assumed.

These are **descriptive associations**, not causal explanations or the output of a predictive model.

## Technology Stack

| Component | Tools | Application |
| --- | --- | --- |
| Relational database | MySQL, SQL | Store and retrieve the original loan-level dataset |
| Database integration | SQLAlchemy, PyMySQL, pandas | Connect Python to MySQL and load the analytical table |
| Data preparation | pandas, NumPy | Inspect data quality, handle blank employment values, parse dates, and engineer segments |
| Exploratory data analysis | pandas, NumPy | Calculate portfolio KPIs and compare first-EMI default rates across borrower groups |
| Visualization | Matplotlib, Seaborn | Communicate LTV, age, bureau risk, overdue-account, and inquiry comparisons |
| Business intelligence | Power BI, DAX | Build a two-page report with responsive measures and slicers |
| Analysis environment | Jupyter Notebook | Execute and document the analytical workflow |

## Data Model

The original labeled dataset is stored in a **single loan-level MySQL table** (`loan`) in the `loan_default_analysis` database. Each row represents one vehicle loan; `UniqueID` identifies records, and `loan_default` is the binary target used for analysis.

| Source | Rows | Grain | Main fields |
| --- | ---: | --- | --- |
| `train.csv` → MySQL `loan` | **233,154** | One record per vehicle loan | `UniqueID`, `disbursed_amount`, `asset_cost`, `ltv`, `loan_default`, `State_ID`, `branch_id`, `Employment.Type`, `DisbursalDate` |
| Credit bureau fields within `loan` | Same rows | Loan-level attributes | `PERFORM_CNS.SCORE`, `PERFORM_CNS.SCORE.DESCRIPTION`, `PRI.OVERDUE.ACCTS`, `SEC.OVERDUE.ACCTS`, `PRI.ACTIVE.ACCTS`, `NO.OF_INQUIRIES` |
| Recent credit history within `loan` | Same rows | Loan-level attributes | `DELINQUENT.ACCTS.IN.LAST.SIX.MONTHS`, `NEW.ACCTS.IN.LAST.SIX.MONTHS`, `CREDIT.HISTORY.LENGTH` |

The accompanying `data_dictionary.csv` defines the original fields. `test.csv` is an unlabeled companion dataset and **is not used to calculate the reported default rates**.

## Analytical Workflow

1. **Load the data:** Import the labeled training dataset into MySQL as `loan`, then retrieve its **233,154 rows** into pandas using SQLAlchemy and PyMySQL.
2. **Audit data quality:** Check shape, column types and nulls; identify **7,661 blank employment-type values** and classify them as `Unknown`.
3. **Prepare dates and ages:** Parse disbursement and birth dates, calculate borrower age at disbursement, and create age bands.
4. **Engineer risk segments:** Build grouped categories for LTV, bureau descriptions, defaulted primary/secondary accounts, recent delinquencies, active accounts, credit inquiries, recently opened accounts, and loan-size quartiles.
5. **Calculate performance:** Aggregate loan counts and default events; compare segment default rates with the overall **21.71%** portfolio benchmark.
6. **Visualize findings:** Create targeted Python charts, then build an interactive **two-page Power BI dashboard** using DAX measures and slicers.
7. **Document results:** Summarize portfolio behavior, borrower risk indicators, interpretation limits, and recommendations in the project report.

### Metric Definitions

| Metric or feature | Definition |
| --- | --- |
| First-EMI default flag | `loan_default = 1` for a default on the first EMI; `0` otherwise |
| First-EMI default rate | Defaulted loans / total loans × 100 |
| Segment default rate | First-EMI defaults within a segment / all loans within that segment × 100 |
| Total disbursement | Sum of `disbursed_amount` across loans; converted to crore using ÷ 10,000,000 |
| Average loan amount | Mean of `disbursed_amount` |
| LTV groups | 0–60%, 60–70%, 70–80%, 80–90%, 90–100% |
| Primary / secondary overdue accounts | Number of defaulted primary / co-applicant-or-guarantor-linked accounts at disbursement |
| Recent delinquency | Defaulted accounts in the preceding six months |
| Recent borrowing | Newly opened accounts in the preceding six months; **not** the same as delinquency |
| Loan size quartiles | Four approximately equal-sized loan groups based on `disbursed_amount` |
| No Bureau History | Bureau history unavailable; kept separate from scored risk categories |

**Interpretation limits:** The dataset does not provide realized loss, recovery, or borrower income information. It therefore cannot establish actual credit losses or debt-to-income ratios. The analysis identifies associations and does **not** train or validate a loan-default prediction model.

## Repository Files

Place these files in the repository root, with the two dashboard preview images in `assets/`, for the links below to work.

| File | Purpose |
| --- | --- |
| [`train.csv`](train.csv) | Labeled vehicle loan dataset used for the analysis |
| [`test.csv`](test.csv) | Unlabeled companion dataset; not used for reported findings |
| [`data_dictionary.csv`](data_dictionary.csv) | Original field definitions |
| [`Loan_defaulter_analysis (1).html`](Loan_defaulter_analysis%20%281%29.html) | Read-only Jupyter notebook export containing SQL/Python analysis and charts |
| [`Loan Default Analysis.pbix`](Loan%20Default%20Analysis.pbix) | Interactive, two-page Power BI dashboard |
| [`assets/loan_portfolio_overview.png`](assets/loan_portfolio_overview.png) | Dashboard Page 1 preview |
| [`assets/credit_risk_default_analysis.png`](assets/credit_risk_default_analysis.png) | Dashboard Page 2 preview |
| [`Loan_Default_Credit_Risk_Analysis_Report.pdf`](Loan_Default_Credit_Risk_Analysis_Report.pdf) | Detailed analytical report |
| [`Loan_Default_Credit_Risk_Analysis_Report.docx`](Loan_Default_Credit_Risk_Analysis_Report.docx) | Editable version of the report |
| `loan_default_cleaned.csv` *(if exported)* | Cleaned and feature-engineered dataset for Power BI |
| `Loan_defaulter_analysis.ipynb` *(if added)* | Executable notebook; preferred for reproducing the analysis |

## Run the Project

### 1. Install dependencies

Use Python 3 and a local MySQL server:

```bash
python -m pip install pandas numpy matplotlib seaborn sqlalchemy pymysql notebook
```

Power BI Desktop is required to open the `.pbix` dashboard.

### 2. Initialize MySQL

In MySQL Workbench, create the database:

```sql
CREATE DATABASE IF NOT EXISTS loan_default_analysis;
```

Import **`train.csv`** into this database as a table named **`loan`**, retaining the original column names and the `loan_default` target. Verify the row count:

```sql
SELECT COUNT(*) AS total_loans FROM loan_default_analysis.loan;
-- Expected: 233154
```

### 3. Run the analysis

Launch Jupyter from the project directory:

```bash
python -m notebook
```

Open the executable analysis notebook (`.ipynb`) if it is included in your repository. The supplied **`Loan_defaulter_analysis (1).html`** is an HTML export for **viewing** the analysis, not for executing cells.

Configure the MySQL connection in your local notebook for your own server and credentials. **Do not commit database passwords** to GitHub. The notebook queries `SELECT * FROM loan`, prepares the loan data, calculates segment findings, and creates the charts. Export the final prepared dataset as `loan_default_cleaned.csv` if needed for Power BI.

### 4. Open the Power BI dashboard

Open **`Loan Default Analysis.pbix`** in Power BI Desktop. If the Power BI data source references a different local machine, update it to the cleaned CSV or applicable local connection before refreshing.

Use **State, Employment Type, and Disbursement Date** slicers to investigate changes in portfolio metrics and risk-segment rates across both report pages.

## Recommended Business Actions

- **Review higher-LTV lending:** Examine underwriting and collateral policies for the 70–90% LTV bands, accounting for borrower mix and sufficient sample size.
- **Prioritize credit-history verification:** Review applicants with previous primary-account defaults and repeated recent delinquency alongside other underwriting information.
- **Investigate frequent inquiries:** Examine the **3+ inquiry segment** for elevated first-EMI defaults; avoid treating inquiries as proof of financial distress.
- **Strengthen thin-file assessment:** Develop separate review criteria for the **116,950 loans with no bureau history**, without equating missing credit information with poor creditworthiness.
- **Monitor segments and geography:** Compare default rates and underlying loan volumes across loan-size bands, branches, and state IDs; use consistent cohort definitions before drawing operational conclusions.

Any proposed policy change should be evaluated on comparable borrower cohorts, approval volume, and subsequent repayment outcomes rather than on unadjusted default-rate differences alone.

## Author

**Swayam Dalal**  
Data Analytics & Business Intelligence
