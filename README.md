# IoT Sensor Fault Detection Model

A machine learning demonstration project for detecting faults in time-series sensor data.

---

## IMPORTANT: THIS PROJECT USES DUMMY DATA

**The sensor_data.csv file contains SYNTHETIC DATA, not real sensor measurements.**

This data was artificially generated using Python's random number generators. The model's performance metrics are artificially inflated and **WILL NOT work** on real IoT sensor data.

### Why This Matters:

- **Perfect accuracy (100%)** shown here is unrealistic
- **Zero false positives/negatives** will not happen in real deployments
- **Data patterns are too simple** - real sensors have noise, drift, and overlapping values
- **Real-world accuracy** would be 75-85%, not 95%+

---

## About The Data

### Dummy Data Characteristics:
- **Source:** Programmatically generated using `numpy.random.uniform()`
- **Records:** 1000+ synthetic observations
- **Normal readings:** Temperature 72-74°F, Pressure 101-102 PSI
- **Fault readings:** Temperature 85-100°F, Pressure 105-120 PSI
- **Problem:** No overlap between normal and fault - makes classification trivial

### Real IoT Data Would Have:
- Measurement noise and sensor drift
- Overlapping ranges between normal and fault conditions
- Missing data points from network failures
- Gradual equipment degradation
- Multiple fault types
- Environmental factors affecting readings

---

## Why This Won't Work in Production

### Issue 1: Data Leakage
Rolling window features are calculated on the entire dataset before train/test split, causing the model to "see" test data during training.

### Issue 2: Oversimplified Patterns
Real sensors don't have perfect separation between normal (72-74°F) and fault (85-100°F). In reality:
- Normal operation: 70-90°F (varies by load)
- Fault conditions: 85-120°F (overlaps with normal)
- A reading of 87°F could be normal or faulty

### Issue 3: No Real-World Complexity
Missing challenges like:
- Sensor calibration drift over time
- Network latency and dropped packets
- Multiple simultaneous sensor failures
- Context-dependent fault thresholds
- False alarm costs vs missed fault costs

---

## Project Structure

```
iot sensor/
├── sensor_data.csv              # DUMMY DATA - synthetic records
├── iot_fault_detection.ipynb    # Machine learning notebook
├── requirements.txt             # Python dependencies
└── README.md                   # This file
```

---

## Technologies

- **Python 3.8+**
- **Pandas** - Data manipulation
- **NumPy** - Numerical operations
- **Scikit-Learn** - Machine learning
- **Matplotlib & Seaborn** - Visualization
- **Jupyter Notebook** - Interactive development

---

## Installation

```bash
# Install dependencies
pip install -r requirements.txt

# Launch Jupyter Notebook
jupyter notebook iot_fault_detection.ipynb
```

---

## Model Performance (On Dummy Data)

### Reported Metrics:
- Accuracy: ~100% (Unrealistic)
- Precision: ~100% (Too perfect)
- Recall: ~100% (Red flag)
- False Positives: 0 (Won't happen in reality)
- False Negatives: 0 (Indicates data leakage)

### Expected Real-World Performance:
- Accuracy: 75-88%
- Precision: 70-85%
- Recall: 85-92%
- False Positive Rate: 8-15%
- False Negative Rate: 8-15%

---

## Workflow

1. **Load Data** - Import synthetic CSV file
2. **Explore** - Visualize sensor readings
3. **Preprocess** - Handle outliers and missing values
4. **Feature Engineering** - Create rolling statistics
5. **Train Model** - Random Forest classifier
6. **Evaluate** - Calculate performance metrics
7. **Save Model** - Export trained model

---

## Features Used

### Original Sensors:
- Sensor 1: Temperature (°F)
- Sensor 2: Pressure (PSI)
- Sensor 3: Vibration (mm/s)
- Sensor 4: Humidity (%)

### Engineered Features:
- Rolling mean (5-sample window)
- Rolling standard deviation
- Rolling min/max
- Rate of change
- Temperature-pressure ratio
- Time-based features (hour, minute)

---

## Model Configuration

- **Algorithm:** Random Forest Classifier
- **Estimators:** 100 trees
- **Max Depth:** 10
- **Class Weight:** Balanced
- **Train/Test Split:** 80/20

---

## Use Cases

### Good For:
- Learning ML workflow basics
- Understanding time-series features
- Practicing data visualization
- Educational demonstrations

### Not Good For:
- Production deployment
- Real equipment monitoring
- Critical safety systems
- Actual fault detection

---

## Key Limitations

1. **Synthetic data** doesn't represent real sensor behavior
2. **Data leakage** in feature engineering inflates metrics
3. **No sensor drift** or calibration issues modeled
4. **Binary classification** only - real systems have multiple fault types
5. **Perfect temporal spacing** - real systems have delays and missing data
6. **No cost modeling** - false alarms vs missed faults have different impacts

---

## For Real Implementation

### What You Need:

1. **Real Data Collection**
   - 6-12 months of actual sensor measurements
   - Documented maintenance events
   - Multiple equipment units

2. **Fix Data Leakage**
   - Split data first, then calculate features
   - Use time-series cross-validation
   - Prevent future information leakage

3. **Realistic Evaluation**
   - Use walk-forward validation
   - Test on unseen equipment
   - Calculate confidence intervals

4. **Production Architecture**
   - Real-time data ingestion pipeline
   - Model monitoring for drift
   - Automated retraining
   - Alert routing system

5. **Business Integration**
   - Tune thresholds based on costs
   - Integrate with maintenance schedules
   - Provide explainable predictions

---

## Learning Objectives

### What This Teaches:
- Basic ML project structure
- Feature engineering concepts
- Model training process
- Evaluation metrics

---
