# 🌳 Pollen Radar – Turning Pollen Data into Insights for Health and Business in Sweden <img src="pics/sweden_flag.svg" alt="Sweden flag" height="24">

![Live Dashboard - DASH](https://img.shields.io/badge/Live_Dashboard-DASH-1F4E79?labelColor=1F4E79&style=for-the-badge)
![A/B test design](https://img.shields.io/badge/A%2FB_test_design-2E7D32?style=for-the-badge)
![Data Analysis](https://img.shields.io/badge/Data_Analysis-6A1B9A?style=for-the-badge)

An end-to-end data pipeline that collects hourly pollen, air quality and weather data for six Swedish cities and models it with **dbt** and **DuckDB**. The results feed a live **Dash** dashboard for people with allergies and for businesses.


## 🔗 Live dashboard

https://pollen-radar-sweden.onrender.com

*For loading the dashboard can take 30–60 seconds to wake up.*


## ✨ Features

- Business insights for pharmacies, tourism, outdoor events and retail.
- A/B test designs for retailers: 
    * Pollen alert email
    * Pollen-based banner
    * Campaign timing 
    * In-store placement
    
     Each with a control group, a main metric and a statistical test.
- Pollen alerts by Windows notification, phone push (ntfy) and an in-dashboard traffic light.
- Live pollen view from the Open-Meteo API.
- Data validated against measured Stockholm pollen seasons: season dates match within about one week.

## 💡 Key insights

- Birch season starts ~3 weeks later in the north than in the south.
- Pollen is lowest at 05:00–08:00 in every city.
- Rain halves pollen, but it recovers within 1.5–2 days.
- Pharmacies should stock allergy products by week 13–14 (south) and week 16 (north).
- Pollen-triggered campaigns start on time; a fixed 1 April date is 2–6 weeks too early.

Full analysis: [`notebooks/analysis.ipynb`](notebooks/analysis.ipynb)



## 🛠️ Tech stack

- SQL & [dbt](https://www.getdbt.com/) – data models and quality tests
- [Python](https://www.python.org/) & [pandas](https://pandas.pydata.org/) – data analysis
- [Dash](https://dash.plotly.com/) & [Plotly](https://plotly.com/python/) – interactive dashboard and charts
- [DuckDB](https://duckdb.org/) – analytical database
- [Open-Meteo API](https://open-meteo.com/) – pollen, air quality and weather data
- [Render](https://render.com/) – live dashboard hosting

## 📁 Project structure

- `ingestion/` — APIs → DuckDB raw data
- `dbt/` — staging and marts SQL models, tests
- `dashboard/` — Dash app, charts, alerts, notifications
- `tests/` — pytest suite
- `notebooks/` — data exploration and analysis
- `data_snapshot/` — Parquet snapshot used by the live dashboard

## ⚡ Run locally (optional)

Requirements: [uv](https://docs.astral.sh/uv/) (installs Python and all dependencies).

```bash
uv sync
uv run python dashboard/app.py      # → http://127.0.0.1:8050
```

The dashboard starts with the data saved in `data_snapshot/`. To get the latest data, press **🔄 Update data** in the header: it downloads the new days, rebuilds the tables with dbt and reloads the dashboard. The first time it downloads the full history since 2021 and takes a few minutes.

---

*Data: Open-Meteo (CAMS European air quality model). Pattern information, not medical advice.*
