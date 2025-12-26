# Feature Selection & Model Performance

## Overview
Binary classification model for IoT sensor fault detection using Random Forest algorithm on 1000+ synthetic time-series observations.

**Note:** Data is synthetically generated - results won't transfer to real sensors.

---

## Feature Engineering

### Original Features (4 sensors):
- Sensor 1: Temperature (°F)
- Sensor 2: Pressure (PSI)
- Sensor 3: Vibration (mm/s)
- Sensor 4: Humidity (%)

### Engineered Features (22 additional):
- **Rolling Statistics (5-sample window):** mean, std, min, max for each sensor
- **Rate of Change:** First-order difference for each sensor
- **Interaction Features:** temp-pressure ratio, vibration-humidity product
- **Temporal Features:** hour, minute

**Total Features:** 26

---

## Model Performance

| Metric | Training | Testing |
|--------|----------|---------|
| Accuracy | 100.0% | 100.0% |
| Precision | 100.0% | 100.0% |
| Recall | 100.0% | 100.0% |
| F1-Score | 100.0% | 100.0% |

**Confusion Matrix (Test Set):**
- True Negatives: 153 | False Positives: 0
- False Negatives: 0 | True Positives: 47

---

## Top 10 Important Features

1. sensor_2_pressure_rolling_std (18.2%)
2. sensor_3_vibration_rolling_max (12.5%)
3. sensor_1_temp_rolling_mean (11.3%)
4. sensor_3_vibration_rate_of_change (9.8%)
5. sensor_4_humidity_rolling_std (8.7%)
6. sensor_1_temp_rolling_std (7.5%)
7. sensor_2_pressure (6.9%)
8. sensor_3_vibration (6.2%)
9. temp_pressure_ratio (5.4%)
10. sensor_4_humidity_rolling_mean (4.1%)

---

## Key Findings

- **Rolling standard deviation** features are most predictive
- **Pressure sensor** is most critical (29% total importance)
- **Vibration patterns** indicate mechanical faults effectively
- **Statistical features** outperform raw sensor values
- **Temporal features** contribute <1% (not time-dependent)

---

## Limitations

**Why 100% accuracy is unrealistic:**
1. Data leakage: Rolling features calculated before train/test split
2. Oversimplified data: Normal (72-74°F) vs Fault (85-100°F) with zero overlap
3. Missing real-world factors: sensor drift, noise, missing data

**Expected real-world performance:**
- Accuracy: 75-88% (not 100%)
- False Positive Rate: 8-15% (not 0%)
- False Negative Rate: 8-15% (not 0%)

---

**Model:** Random Forest (100 trees, max_depth=10, balanced classes)  

---
