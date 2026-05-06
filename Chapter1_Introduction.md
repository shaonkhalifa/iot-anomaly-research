# Chapter 1: Introduction

## 1.1 Background
The Internet of Things (IoT) has revolutionized industrial monitoring by allowing for the real-time collection and analysis of data from a vast array of sensors. In industrial environments, sensors are used to monitor critical parameters such as temperature, humidity, energy consumption, and vibration. As these systems scale, the volume of data generated grows exponentially, making manual monitoring impossible.

The reliability of these systems depends on the ability to distinguish between "normal" operational data and "anomalies." Anomalies can indicate several critical issues, including hardware malfunctions, security breaches, or unexpected environmental changes. Detecting these events early is essential for maintaining system health and preventing costly downtime.

## 1.2 Problem Statement
Despite the benefits of IoT, detecting anomalies in sensor data remains a significant challenge. Real-world IoT data is often "noisy" due to network latency, sensor calibration errors, and environmental interference. In many cases, what appears to be an anomaly is simply an outlier caused by a temporary network delay or a specific operational mode.

Furthermore, traditional threshold-based systems (e.g., triggering an alarm if temperature > 50°C) are often too rigid. They fail to account for the context of the data, such as the specific sensor type or the time of day. There is a clear need for more advanced, unsupervised machine learning techniques that can adapt to different data patterns without requiring labeled "anomaly" datasets, which are rarely available in real-world scenarios.

## 1.3 Objectives
The primary goal of this research is to develop a robust, end-to-end IoT Anomaly Detection System that can process raw industrial sensor data and provide actionable insights. The specific objectives are:

1.  To create a 9-stage preprocessing workflow to clean, validate, and normalize raw sensor data before analysis.
2.  To implement and compare three distinct machine learning algorithms—Isolation Forest, One-Class SVM, and K-Means—to identify anomalies.
3.  To enhance the detection results with critical metadata such as "Network Delay" (the time difference between device logging and server reception) and sensor-specific warnings.
4.  To create a professional visualization dashboard for data analysts to upload datasets, visualize results, and export findings for offline reporting.

## 1.4 Scope of the Work
This project focuses on unsupervised anomaly detection using historical and real-time batches of sensor data. The system is designed as a three-tier architecture:
- Processing CSV and Excel files containing industrial sensor readings.
- A .NET backend and a Python-based machine learning service for inference.
- An Angular-based frontend for interactive data exploration.
