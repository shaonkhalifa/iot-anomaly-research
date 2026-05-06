# Chapter 3: Methodology and Design

## 3.1 Overview of the Proposed System
The proposed system follows a modular architecture designed to handle batch processing of IoT sensor data. The workflow is divided into three main phases: Data Acquisition & Preprocessing, Model Inference, and Result Visualization.

## 3.2 The 9-Stage Data Cleaning Pipeline
To ensure high data quality, a robust 9-stage cleaning and preprocessing pipeline was implemented in Python. This pipeline ensures that the machine learning models receive consistent and valid data.

1.  Ensuring required columns (e.g., `LogTime`, `LogFloatValue`) exist.
2.  Converting timestamps to datetime objects and sensor values to appropriate numeric types.
3.  Removing or imputing rows with critical missing values.
4.  Eliminating redundant records based on unique sensor/timestamp combinations.
5.  Checking if values fall within realistic physical ranges (e.g., humidity between 0-100%).
6.  Unlike global outlier detection, this stage computes Interquartile Range (IQR) fences for each specific `LogType` group. This ensures that a temperature reading is compared only against other temperature readings, preventing false positives caused by differing scales across sensor types.
7.  Feature Engineering including:
    - Computing the difference between `ServerTime` and `LogTime`.
    - Extracting the hour of the day to capture diurnal patterns.
8.  Scaling features (using StandardScaler) to ensure the models are not biased toward columns with larger numerical ranges.
9.  One-hot encoding categorical variables like `LogTypeID` to make them usable by the algorithms.

## 3.3 Model Training and Selection
The system utilizes three unsupervised learning algorithms to provide a comparative view of the data. 

### 3.3.1 Training Strategy
Since true labels (Anomaly/Normal) are often unavailable, the models are trained in an unsupervised manner on the provided dataset. The models learn the "normal" density of the data and assign an anomaly score to each record. 

### 3.3.2 Algorithm Parameters
- **Isolation Forest**: This model isolates anomalies instead of profiling normal data. We set the `contamination` parameter to 0.05, which indicates that we expect roughly 5% of the sensor readings to be abnormal.
- **One-Class SVM**: This model draws a boundary around the normal data using an RBF (Radial Basis Function) kernel to capture complex, non-linear patterns. The `nu` parameter is set to 0.05 to control the strictness of the boundary.
- **K-Means**: This model groups similar data points into clusters. We set $k=3$ to represent the distinct types of sensors, and any reading far from these clusters is flagged as an anomaly.

## 3.4 Diagnostic Metric: Network Delay
A key innovation in this methodology is the inclusion of "Net Delay" as a diagnostic metric. By calculating the delay between the device logging time and the server reception time, the system can identify potential network congestion or gateway issues. This data is surfaced alongside the anomaly predictions to give a full picture of system performance.
