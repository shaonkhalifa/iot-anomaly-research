# Chapter 2: Literature Review

## 2.1 Overview of IoT Data Challenges
Industrial IoT data is characterized by its high velocity and volume. Researchers have identified several challenges in this domain, primarily data quality and security [1]. Sensor data often contains missing values, duplicates, and outliers. Addressing these issues is the first step in any anomaly detection workflow, as machine learning models are highly sensitive to "dirty" data.

## 2.2 Machine Learning for Anomaly Detection
Anomaly detection (also known as outlier detection) is the process of finding patterns in data that do not conform to expected behavior. In unsupervised learning, the model is not told what is an anomaly; instead, it learns the statistical distribution of "normal" data and flags anything that deviates significantly.

### 2.2.1 Isolation Forest
The Isolation Forest algorithm is highly effective for high-dimensional datasets. Unlike other methods that build a profile of normal points, Isolation Forest explicitly isolates anomalies. It works on the principle that anomalies are "few and far between," making them easier to isolate in a tree structure with fewer splits than normal points [2].

### 2.2.2 One-Class SVM
One-Class Support Vector Machines (SVM) are a variation of the traditional SVM used for novelty detection. The algorithm learns a decision boundary that encompasses the majority of the data points (the "normal" class). Any data point that falls outside this boundary is classified as an anomaly. It is particularly useful for detecting anomalies that do not follow a Gaussian distribution [3].

### 2.2.3 K-Means Clustering
K-Means is a popular clustering algorithm that partitions data into *k* clusters. For anomaly detection, the distance between a data point and its nearest cluster center (centroid) is used as an anomaly score. Points that are far from any cluster center are likely to be anomalies [4].

## 2.3 Preprocessing and Outlier Handling
The Interquartile Range (IQR) method is a common statistical technique for identifying outliers. It calculates the range between the 25th and 75th percentiles. Any data point falling below $Q1 - 1.5 \times IQR$ or above $Q3 + 1.5 \times IQR$ is considered a statistical outlier. In the context of IoT, this is often used as a first-pass cleaning step to remove obviously erroneous sensor readings.

## 2.4 Diagnostic Metadata in IoT
Recent literature suggests that purely statistical analysis of sensor values is often insufficient. Including temporal metadata, such as network delay (the latency between data generation and processing), provides a more comprehensive view of system health. Network delays can sometimes mimic anomalies or indicate underlying infrastructure issues that are as important as the sensor values themselves.

---
### References (Placeholder)
[1] J. Smith et al., "Data Quality in Industrial IoT," Journal of Sensors, 2023.
[2] F. T. Liu et al., "Isolation Forest," IEEE International Conference on Data Mining, 2008.
[3] B. Schölkopf et al., "Estimating the Support of a High-Dimensional Distribution," Neural Computation, 2001.
[4] A. Jain, "Data Clustering: 50 Years Beyond K-Means," Pattern Recognition Letters, 2010.
