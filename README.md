# Indian Road Accident Risk Analysis — Dashboard README

## Overview
This workbook analyzes 20,000 simulated road accident records from eight Indian cities to surface patterns in accident severity, causes, timing, weather, and location risk. It contains three sheets that work together: a raw data table, a set of pivot tables, and a visual dashboard built from those pivots.

## File Structure

| Sheet | Purpose |
|---|---|
| **indian_roads_dataset** | Raw, record-level data — one row per accident (20,000 rows × 27 columns) |
| **pivot_table** | Pivot tables and summary aggregations that feed the dashboard charts |
| **Dashboard** | Visual summary page: KPI cards, slicers, and 7 charts |

## 1. `indian_roads_dataset` sheet (raw data)

Each row is one accident record. Key columns:

| Column | Description |
|---|---|
| `accident_id` | Unique record ID |
| `city`, `state` | Location of the accident |
| `latitude`, `longitude` | GPS coordinates |
| `date`, `time`, `hour` | When the accident occurred |
| `day_of_week`, `is_weekend` | Day-level context |
| `month`, `month_no` | Month name / number |
| `time_bucket` | Grouped time of day (Midnight, Morning, Afternoon, Evening) |
| `road_type` | highway / urban / rural |
| `lanes`, `traffic_signal` | Road infrastructure at the site |
| `weather`, `visibility`, `temperature` | Environmental conditions |
| `traffic_density` | low / medium / high |
| `cause` | Primary accident cause (weather, distraction, overspeeding, drunk driving, poor road) |
| `accident_severity` | fatal / major / minor |
| `vehicles_involved`, `casualties` | Impact of the accident |
| `is_peak_hour`, `festival` | Special-condition flags |
| `risk_score` | Computed risk value (0–1) for the record |

This sheet is the single source of truth — every chart on the Dashboard is ultimately derived from it via the pivot tables.

## 2. `pivot_table` sheet

Contains the aggregated tables that power each dashboard chart, including:
- Accident Severity Distribution (fatal / major / minor counts)
- Monthly Accident Trend (accidents by month)
- Top Accident Causes (accident count by cause)
- Accidents by Traffic Density
- Accidents by Time of Day
- Accidents by Weather × Severity (stacked)
- Top 8 High-Risk Cities (by average risk score)

If you refresh or edit the raw data, refresh these pivot tables (right-click → Refresh, or Data → Refresh All) so the Dashboard updates.

## 3. `Dashboard` sheet

### KPI Cards (top row)
- **Total Accidents:** 20,000
- **Total Casualties:** 34,529
- **Fatal Accidents:** 2,987
- **Average Risk Score:** 0.4376

### Slicers (filter controls)
Four slicers let you filter every chart on the dashboard interactively:
- `city` — filter by one or more cities
- `accident_severity` — fatal / major / minor
- `weather` — clear / fog / rain
- `road_type` — highway / rural / urban

### Charts
1. **Monthly Accident Trend** — line chart of total accidents by month (Jan–Dec)
2. **Accident Severity Distribution** — donut chart of fatal/major/minor share
3. **Top Accident Causes** — horizontal bar chart ranking causes (weather, poor road, overspeeding, drunk driving, distraction) by accident count
4. **Accidents by Traffic Density** — bar chart comparing low/medium/high traffic density
5. **Accidents by Time of Day** — bar chart across Midnight/Morning/Afternoon/Evening buckets
6. **Accidents by Weather (stacked by severity)** — stacked bar showing fatal/major/minor split for clear, rain, and fog conditions
7. **Top 8 High-Risk Cities** — bar chart ranking cities by average risk score (Chandigarh highest, Mumbai lowest of the top 8)

## How to Use This Dashboard
1. Open the **Dashboard** sheet — this is the main view.
2. Use the four **slicers** to filter by city, severity, weather, or road type; all charts update together.
3. To dig into individual records behind any chart, go to the **indian_roads_dataset** sheet and filter/sort as needed.
4. To change what a chart shows, edit the underlying table on **pivot_table**, then refresh.

## Notes / Assumptions
- `risk_score` is a pre-computed field in the raw data (not derived within this workbook); treat it as a given input.
- The dataset appears to be simulated/synthetic (uniform-looking distributions across causes, cities, etc.) rather than an official government accident report — use it for practice/analysis purposes rather than as an authoritative real-world source.
- Slicers are linked to the pivot tables; adding new raw data rows requires updating the pivot table's source range before it will appear in slicer options.

## Companion Files
- `indian_roads_dataset.pdf` — a static, print-friendly export of the Dashboard sheet (same KPIs and charts, non-interactive).
