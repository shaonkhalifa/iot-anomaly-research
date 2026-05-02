# Chapter 3: Methodology and Design

## 3.1 Overview of the Proposed System
The proposed system follows a modular architecture designed to handle batch processing of IoT sensor data. The workflow is divided into three main phases: Data Acquisition & Preprocessing, Model Inference, and Result Visualization.

## 3.2 The 9-Stage Data Cleaning Pipeline
To ensure high data quality, a robust 9-stage cleaning and preprocessing pipeline was implemented in Python. This pipeline ensures that the machine learning models receive consistent and valid data.

1.  **Initial Validation**: Ensuring required columns (e.g., `LogTime`, `LogFloatValue`) exist.
2.  **Type Conversion**: Converting timestamps to datetime objects and sensor values to appropriate numeric types.
3.  **Missing Value Handling**: Removing or imputing rows with critical missing values.
4.  **Duplicate Removal**: Eliminating redundant records based on unique sensor/timestamp combinations.
5.  **Domain Validation**: Checking if values fall within realistic physical ranges (e.g., humidity between 0-100%).
6.  **IQR Outlier Flagging**: Using the Interquartile Range (IQR) method to flag statistical outliers in `LogFloatValue` for each sensor type.
7.  **Feature Engineering**:
    - **Time Delay Calculation**: Computing the difference between `ServerTime` and `LogTime`.
    - **Temporal Features**: Extracting the hour of the day to capture diurnal patterns.
8.  **Normalization**: Scaling features (using StandardScaler) to ensure the models are not biased toward columns with larger numerical ranges.
9.  **Categorical Encoding**: One-hot encoding categorical variables like `LogTypeID` to make them usable by the algorithms.

## 3.3 Model Training and Selection
The system utilizes three unsupervised learning algorithms to provide a comparative view of the data. 

### 3.3.1 Training Strategy
Since true labels (Anomaly/Normal) are often unavailable, the models are trained in an unsupervised manner on the provided dataset. The models learn the "normal" density of the data and assign an anomaly score to each record. 

### 3.3.2 Algorithm Parameters
- **Isolation Forest**: Set with a `contamination` parameter representing the expected proportion of anomalies in the dataset.
- **One-Class SVM**: Configured with an RBF kernel to capture non-linear decision boundaries.
- **K-Means**: Trained with *k* clusters based on the distinct sensor types identified in the data.

## 3.4 Diagnostic Metric: Network Delay
A key innovation in this methodology is the inclusion of "Net Delay" as a diagnostic metric. By calculating the delay between the device logging time and the server reception time, the system can identify potential network congestion or gateway issues. This data is surfaced alongside the anomaly predictions to give a full picture of system performance.
