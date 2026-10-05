# EDA on India's COVID-19 Data

Mini project for **Module 1: Python for Data Science** (Data Science & ML Training Series).
The notebook `module1.ipynb` cleans India's state-wise COVID-19 case records and explores them with
Pandas, Matplotlib, and Seaborn, then adds a look at the national vaccination rollout.

## What this project covers

- Loading data directly from public CSV URLs
- Cleaning messy real-world data (column names, data types, inconsistent state names, duplicates)
- Summarising with `groupby` and `pivot_table`
- Building national and state-level metrics (recovery rate, death rate, daily new cases)
- Visualising trends, rankings, relationships, and distributions

## Datasets

| Dataset | Source | Used for |
|---|---|---|
| State-wise COVID-19 cases | [imdevskp/covid-19-india-data](https://github.com/imdevskp/covid-19-india-data) (`complete.csv`) | Cases, deaths, recoveries by state/UT and date |
| India vaccination data | [Our World in Data](https://github.com/owid/covid-19-data) (`vaccinations/country_data/India.csv`) | Total doses and fully vaccinated people over time |

Both files are read live from `raw.githubusercontent.com`, so an internet connection is required.

## Setup

```bash
# 1. Create and activate a virtual environment
python -m venv venv
source venv/bin/activate        # macOS / Linux
venv\Scripts\activate           # Windows

# 2. Install dependencies
pip install numpy pandas matplotlib seaborn jupyter

# 3. Launch Jupyter and open the notebook
jupyter notebook module1.ipynb
```

Then run all cells from top to bottom.

## Notebook walkthrough

1. **Setup:** imports, Seaborn theme, display options.
2. **Load data:** reads the cases and vaccination CSVs and prints their shapes.
3. **Inspect:** checks dtypes, missing values, and the list of unique state/UT names.
4. **Clean:**
   - renames columns to snake_case (`date`, `state`, `lat`, `long`, `confirmed`, `deaths`, `cured`, `new_cases`, `new_deaths`, `new_recovered`)
   - converts `date` to datetime and fixes numeric types
   - standardises state names (for example `Telengana` and `Telangana***` become `Telangana`)
   - drops duplicate `(date, state)` rows
   - adds an `active` cases column (confirmed − deaths − cured)
5. **National summary:** aggregates by date and computes recovery rate, death rate, and daily new confirmed cases.
6. **Headline numbers:** prints total confirmed, recovered, and deaths as of the latest date.
7. **State analysis:** ranks states by confirmed cases and builds a top-10 table with recovery and death rates.
8. **Monthly pivot:** new cases per month for the top 5 states.
9. **Visualisations** (below).

## Visualisations

| # | Chart | What it shows |
|---|---|---|
| 1 | Line chart | National cumulative confirmed, recovered, and deaths over time |
| 2 | Bar chart | Daily new confirmed cases (the waves) |
| 3 | Horizontal bar (Seaborn) | Top 10 states by total confirmed cases |
| 4 | Multi-line chart | Confirmed-case trend for the top 5 states |
| 5 | Bubble scatter | Recovery rate vs death rate by state, sized by case count |
| 6 | Boxplot | Spread of daily new cases by month |
| 7 | Line chart | India's vaccination progress (total doses and fully vaccinated) |

## Project structure

```
.
├── module1.ipynb     # the analysis notebook
└── README.md
```

## Notes

- Results depend on the latest state of the source CSVs; if a repository changes its columns or file path,
  the loading or renaming cells may need adjusting.
- The column rename step assumes the cases file has exactly 10 columns in the order listed above.
- The vaccination chart title says 2021–2024; check it against the actual date range in your downloaded data.

## Related material

- Module 1 Handbook: *Python for Data Science, A 5-Hour Study Plan*
- Module 1 Practice Notebook (IPL match dataset)
