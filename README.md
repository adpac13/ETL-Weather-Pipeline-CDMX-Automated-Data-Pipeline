# ETL-Weather-Pipeline-CDMX-Automated-Data-Pipeline
An automated ETL pipeline that extracts real-time weather data from a REST API, transforms it into an analytical format, loads it to SQLite, and generates a daily Excel report fully automated with Windows Task Scheduler.

## Business Objective

Build a fully automated ETL pipeline that:
- Extracts **real-time weather data** from a public REST API
- Transforms raw JSON into an **analytical format**
- Loads clean data into a **SQLite database**
- Generates a **daily Excel report** automatically
- Runs every day at **6:00 AM** without manual intervention

## Pipeline Architecture

### 1. Extract
- Source: [Open-Meteo API](https://open-meteo.com/) — free, no API key required
- Location: Ciudad de México (lat: 19.4326, lon: -99.1332)
- Data: 30 days of daily weather metrics

### 2. Transform
- Converted date strings to datetime format
- Engineered 3 new columns: `avg_temp`, `range_temp`, `rain_day`
- Handled NaN values in precipitation

### 3. Load
- Loaded clean dataframe to SQLite table `clima_diario`
- 37 records · 8 columns

### 4. Report
- Auto-generated Excel with 4 sheets and professional styling
- Filename includes timestamp: `reporte_clima_YYYYMMDD_HHMM.xlsx`

### 5. Automation
- Scheduled with Windows Task Scheduler
- Runs daily at 6:00 AM
- Zero manual intervention required

---

## Key Findings (May — June 2026)

**1. May was significantly hotter than June**
The 5 hottest days all occurred in May, with a peak of 30.4°C on May 16th — before the rainy season began in earnest.

**2. June marks a clear transition to rainy season**
86% of days in the analysis period had rainfall (32 out of 37 days), with the rainiest days concentrated in early June — peaking at 21.9mm on June 4th.

**3. Rainfall and temperature are inversely correlated**
As precipitation increased in June, average daily temperature dropped noticeably — from ~23°C in May to ~18°C in early June.

**4. Total accumulated precipitation: 218.1mm in 37 days**
This level of rainfall has direct business implications for industries like retail, logistics, and agriculture operating in CDMX.

---

## Visualizations

### Daily Temperature Range
![Daily Temperature Range](visualizations/clima_temperatura.png)

### Daily Precipitation
![Daily Precipitation](visualizations/clima_precipitacion.png)

### Avg Temperature vs Precipitation
![Avg Temperature vs Precipitation](visualizations/clima_temp_vs_precipitacion.png)

---

## How to Run

1. Clone this repository
2. Install dependencies:
```bash
pip install pandas requests openpyxl matplotlib seaborn
```
3. Run the automated script:
```bash
python etl_clima.py
```
4. Or open `notebooks/03_etl_api.ipynb` and run cell by cell
5. Report will be saved automatically in the `reports/` folder

---

## Automate with Task Scheduler (Windows)

1. Open Task Scheduler → Create Basic Task
2. **Program:** `C:\Users\PC\anaconda3\python.exe`
3. **Arguments:** `"path\to\etl_clima.py"`
4. **Frequency:** Daily at 6:00 AM
