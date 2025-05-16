# second-life-battery-dispatch

##  Project Summary

- Predicts normalized RUL (scaled between 1 and 0) from battery cycle data.
- Implements and compares three supervised models:
  - LSTM (sequence-based)
  - XGBoost (tree-based)
  - Bayesian Ridge Regression (with uncertainty)
- Uses predicted RUL to simulate rule-based dispatch decisions in the 2023–2024 German-Luxembourg (DE-LU) day-ahead electricity market.

##  Features

- `avg_voltage`, `avg_current`, `avg_temperature`, `ambient_temperature`
- `discharge_current` (load profile)
- `cycle_progress` (how far the battery is through its life)
- `delta_capacity` (per-cycle capacity drop)
- `rolling_avg_voltage` (voltage smoothing)
- **Target:** `normalized_RUL`

##  Dispatch Logic

At each hourly timestep:
- **Charge** if price < €30/MWh and renewables are abundant
- **Discharge** if price > €60/MWh and predicted RUL > 0.2
- **Idle** otherwise

A degradation penalty proportional to `(1 - RUL)` is applied during charging and discharging.

##  Repository Contents

- `second_life_battery.ipynb` – Model training and dispatch simulation
- `dispatch_data_DE_LU_2023_2024.csv
