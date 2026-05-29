# Project Results Summary

## Agentic AI-Based Dynamic Tariff Optimization for EV Charging Networks
**Open Project 2026 - Society of Business**

---

## Data

| Source | Description |
|--------|-------------|
| **Shenzhen (UrbanEV)** | 8,640 timesteps (5-min intervals) x 247 zones, 30 days Jun-Jul 2022 |
| **ACN-Data (Caltech)** | 14,999 sessions, Caltech campus, Apr-Dec 2018 |

---

## Key EDA Findings

- **System is heavily underutilized**: 60.85% of zone-timesteps below 30% utilization
- **Only 1.02% of zone-timesteps are congested** (>80% utilization)
- **Dynamic pricing zones generate 7.3x more revenue per zone per day** compared to fixed-price zones
- **Price elasticity estimated at -0.83** (inelastic overall)
- **Peak elasticity**: -0.67, **Off-peak**: -1.04

---

## Demand Prediction Results

| Model | RMSE | MAE | R² |
|-------|------|-----|-----|
| **XGBoost** | 0.0863 | 0.0599 | 0.760 |
| Historical Average | 0.0939 | 0.0664 | 0.717 |
| LSTM | 0.1130 | 0.0796 | 0.588 |
| GCN-LSTM | 0.1512 | 0.1159 | 0.267 |

**Best model**: XGBoost (lowest RMSE = 0.0863, highest R² = 0.760)

---

## Pricing Strategy Results

| Strategy | Rev Gain% | Util After | Off-Peak Uplift | Wait Red% |
|----------|-----------|------------|-----------------|-----------|
| Conservative | -0.62% | 0.0202 | 0 | 11.10% |
| **Lerner Index** | **50.50%** | 0.0189 | 3,553 | -54.94% |
| Spatial Coordination | 0.21% | 0.0202 | 250 | 9.05% |

---

## Monitoring Agent Results (20 Episodes)

| Metric | Value |
|--------|-------|
| Wait Time Reduction | 38.96% |
| Customer Response Rate | 26.43% |
| Pricing Efficiency (start) | 15.00 Rs/kWh |
| Pricing Efficiency (end) | 16.97 Rs/kWh |
| Final α | 0.538 |
| Final β | 2.000 |
| Final spatial_w | 0.30 |

---

## ACN Integration

| Metric | Value |
|--------|-------|
| Baseline revenue | ₹2,025,420 |
| Dynamic revenue | ₹1,799,300 |
| Revenue change | -11.16% |
| Peak/off-peak shift | 1,551 kWh moved |

---

## Business Impact

- **For Indian market**: 50.5% revenue gain possible with Lerner Index pricing
- But requires careful demand management (wait times increase by 54.94%)
- **Spatial coordination offers balanced approach**: 0.21% gain with 9% wait reduction
- Self-improving agent reduces surge aggressiveness over time
- Off-peak discounts (β=2.0) stimulate 3,553 additional low-utilization sessions

---

## Limitations

- Data from Shenzhen (China) and Caltech (US), applied to Indian context
- Low baseline congestion limits surge pricing impact
- Elasticity estimates have low R² (0.16) - demand is influenced by many factors beyond price
- Causal claims avoided - correlational analysis only
- Queue proxy is an approximation, not actual measured wait times
- ACN data from single site limits generalizability

---

## Files Produced

| Category | Count | Details |
|----------|-------|---------|
| Visualization PNGs | 19 | plot01-12 (EDA), final_*.png (results) |
| Metric CSVs | 6 | eda_statistics, demand_prediction_metrics, pricing_metrics, monitoring_metrics, acn_pricing_metrics, zone_elasticities |
| Numpy data files | 5 | utilization_rate, capacity, dynamic_prices, adjacency_matrix, distance_matrix |
| Python source scripts | 4 | data_pipeline.py, demand_agent.py, pricing_agent.py, monitoring_agent.py |
| Master notebook | 1 | notebooks/master_notebook.ipynb |
