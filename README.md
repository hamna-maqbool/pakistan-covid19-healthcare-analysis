🎯 Project Objective
This project answers critical healthcare questions using real-world COVID-19 data:

Which wave was the deadliest in Pakistan?
How did vaccination coverage grow over time?
What was the Week-over-Week case growth at any point?
How do daily cases compare against the 7-day rolling average?
What percentage of Pakistan's population got fully vaccinated?


🔄 Complete Project Workflow
Step 1 — Data Extraction

Source: Our World in Data (live public dataset)
Data loaded directly via URL using pd.read_csv() — no manual download needed
Raw dataset: 300,000+ rows, 67 columns, 200+ countries

Step 2 — Data Filtering

Filtered only Pakistan rows from the global dataset
Reset index for clean sequential numbering
Result: 1,200+ rows of Pakistan-specific daily data

Step 3 — Data Cleaning (Python / Pandas)

Converted date column to proper datetime format
Sorted data chronologically (oldest to newest)
Selected only 10 relevant columns out of 67
Missing values handled:

new_cases, new_deaths → filled with 0
total_cases, total_deaths, total_vaccinations → forward filled (ffill)
positive_rate, hosp_patients → linear interpolation


Clipped all negative values to 0

Step 4 — Feature Engineering

7-Day Rolling Average → cases_7day_avg, deaths_7day_avg
Case Fatality Rate (CFR%) → total_deaths / total_cases × 100
Vaccination Coverage % → people_fully_vaccinated / population × 100
Wave Classification → Each date labeled with its COVID wave:

Wave 1: Feb–Jun 2020 (Original strain)
Wave 2: Jul–Nov 2020 (Original strain)
Wave 3: Dec 2020–Apr 2021 (Alpha/Beta)
Wave 4: May–Oct 2021 (Delta — deadliest)
Wave 5: Nov 2021–Mar 2022 (Omicron)
Post-Peak: Apr 2022 onwards


Date columns → year, month_name added for Power BI grouping

Step 5 — Exploratory Data Analysis (EDA)
Generated 4 verification charts using Matplotlib:

Daily new cases + 7-day average overlay
Daily deaths + 7-day average overlay
Cumulative vaccination progress
Total cases per wave (bar chart)

Step 6 — Data Modeling in Power BI (Star Schema)
Date Table (1) ──────── pakistan_covid_clean (*) ──────── Wave Table (1)

Fact Table: pakistan_covid_clean — daily COVID metrics
Date Dimension: Custom DAX CALENDAR() table with Year, Month, Quarter, Week, Weekend flag
Wave Dimension: DATATABLE() with wave name, variant, severity, start/end dates
Relationships: Many-to-One (*:1), Single cross-filter direction

Step 7 — Advanced DAX Measures (7 Measures)
MeasureDAX Functions UsedDescriptionTotal CasesCALCULATE, MAXLatest total with date context7-Day Avg CasesDATESINPERIOD, AVERAGERolling 7-day windowCase Fatality Rate %DIVIDE, ROUNDDeaths ÷ Cases safelyWoW Growth Rate %DATESINPERIOD, SWITCH(TRUE())Weekly comparison with status labelVaccination Coverage %DIVIDE, SWITCH(TRUE())Coverage with threshold labelsPeak Cases AnalysisMAXX, ALLPeak detection across full historyWave Severity ScoreMAXX, VALUES, ALLEXCEPTRelative severity 1–10 per wave
Step 8 — Interactive Power BI Dashboard (4 Pages)
Page 1 — Overview

Total Cases KPI (2M+), CFR (1.94%), Peak Cases, Vaccination Coverage (59.6%)
Daily New Cases Line Chart (2020–2024)
Deaths per Wave Bar Chart
Vaccination by Year Donut Chart

Page 2 — Cases Analysis

Daily Cases + 7-Day Average dual Line Chart
Monthly Cases Trend Column Chart
Week-over-Week Growth Rate Card
Wave Filter Slicer

Page 3 — Vaccinations

Vaccination Progress Area Chart
Total Vaccinations KPI (307M+)
Vaccination by Year Donut Chart

Page 4 — Wave Analysis

Cases per Wave Bar Chart
Deaths Timeline by Wave Line Chart
Wave Severity Score Card
Wave Selector Slicer

Dashboard Features:

Custom dark theme (JSON theme file)
Navigation buttons with custom icons per page
Custom COVID-19 logo in header
Interactive slicers for wave filtering
Dynamic DAX measures responding to all filters


📁 Project Files
FileDescriptionREADME.mdProject documentationcovid19_pakistan_cleaning.pyComplete Python data cleaning scriptpakistan_covid_clean.csvFinal cleaned datasetPakistan_COVID19_Dashboard.pbixPower BI dashboard filedashboard_preview.pngDashboard screenshotcovid19_verification.pngEDA verification chartscovid19_logo.pngCustom project logo

📈 Key Findings
MetricValueTotal Confirmed Cases2,000,000+Total Deaths30,656Case Fatality Rate1.94%Peak Single Day Cases7,142Total Vaccination Doses307 Million+Vaccination Coverage59.6%Deadliest WaveWave 4 — DeltaHighest Cases WaveWave 5 — OmicronAnalysis PeriodFeb 2020 – Dec 2024

🚀 How to Run
Python Script
bashpip install pandas matplotlib numpy
python covid19_pakistan_cleaning.py
Power BI Dashboard

Download Power BI Desktop (free) from microsoft.com
Open Pakistan_COVID19_Dashboard.pbix
Click Refresh to load latest data
Use navigation buttons to explore all 4 pages


🛠️ Tech Stack
TechnologyPurposePython 3.9+Data cleaning & EDAPandasData manipulationMatplotlibVerification chartsNumPyNumerical operationsJupyter NotebookDevelopment environmentPower BI DesktopDashboard & modelingDAXCalculated measures

🌐 Data Source
Our World in Data — COVID-19 Dataset

URL: https://ourworldindata.org/coronavirus
Coverage: 200+ countries, Feb 2020 – present
Pakistan rows: 1,200+ daily records


💡 Skills Demonstrated
✅ Real-world data extraction from public API
✅ Professional data cleaning (missing values, outliers, type conversion)
✅ Feature engineering (rolling averages, ratios, wave classification)
✅ Exploratory Data Analysis with Matplotlib
✅ Star Schema data modeling in Power BI
✅ Advanced DAX measures (DATESINPERIOD, SWITCH, MAXX, ALLEXCEPT)
✅ Interactive 4-page dashboard design
✅ Custom theme, navigation, and branding
✅ Healthcare domain knowledge
✅ End-to-end project documentation
