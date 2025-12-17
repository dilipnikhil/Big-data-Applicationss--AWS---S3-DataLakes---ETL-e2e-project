# PROJECT folder overview

This README summarizes the contents of `PROJECT.zip/PROJECT` under `FA24_ BIG DATA APPLICATIONS_ 12555`.

## Structure
- `Additional_Feature_Eng.ipynb` — notebook for feature engineering steps.
- `Pyspark and SQL.ipynb` — notebook covering PySpark + SQL processing.
- `manifest file for Quicksight.json` — QuickSight import/manifest configuration.
- `Report-Dilip.pdf` — written project report.
- `Presentation.pptx` — slide deck.
- `QuickSight -PDF.pdf` — exported QuickSight visuals.
- `Sequence Diagram.png` — data/processing flow diagram.
- `ScreenShots-AWS/` — AWS setup and QuickSight screenshots.
- `Video - Presentation.mp4` — recorded presentation.
- `Processed_Files/`
  - `Aggregated Files/` — derived CSVs: average_vol, avg_close_by_signal, avg_high_low_by_month, daily_volatility, daily_volume, highest_volatility, monthly_avg_close, monthly_high_low, monthly_volume, month_over_month.
  - `bitcoin_processed.csv` — cleaned/processed base dataset.

## Project summary (data engineering view)
- **Dataset:** Kaggle Bitcoin trades, 1-minute granularity (6.7M rows; ts, open/high/low/close, volume). Goal: predict daily closing price after aggregation and technical features (MA/EMA, momentum, ROC).
- **Pipeline:** Raw → S3; PySpark ingest/clean (nulls, ts→datetime, year/month/day), daily aggregates, metrics (monthly avg close, volume, top-volume days, highs/lows, volatility); write processed + aggregates back to S3.
- **SQL insights (Spark SQL):** Highest avg-volume days; MoM average close; top 5 volatility days; avg close by signal; monthly highs/lows.
- **Modeling (SageMaker Autopilot):** Trained on day-level aggregates; best RMSE ~21.5, MAE ~9.0; low latency (~0.3s). Column naming hygiene mattered.
- **Visuals (QuickSight):** Price peaks/trends, volume spikes, low price vs signal, signal distribution; manifest used to load from S3.
- **Flow (see diagram):** Kaggle → S3 (raw) → PySpark process → S3 (processed/aggregates) → SageMaker AutoML → QuickSight dashboards.

## How to use
1. Unzip `PROJECT.zip`.
2. Review data outputs in `Processed_Files/` first to understand available aggregates.
3. Open notebooks (`Additional_Feature_Eng.ipynb`, `Pyspark and SQL.ipynb`) for code and processing steps (requires Python/PySpark environment).
4. Consult `Report-Dilip.pdf` and `Presentation.pptx` for project narrative and results; `QuickSight -PDF.pdf` for dashboard snapshots.
5. Use `Sequence Diagram.png` and `ScreenShots-AWS/` to reproduce the AWS/QuickSight setup.

