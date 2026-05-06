# Chapter 5: Results and Discussion

## 5.1 Experimental Setup
The system was tested using real-world industrial IoT datasets (e.g., `live_test_2.csv`). The data contained a mix of temperature and energy sensor readings from multiple stations (identified by `RmsStationId`).

## 5.2 Model Performance and Comparison
The "Compare All Models" feature provided significant insights into the behavior of the different algorithms.

| Model | Anomaly Detection Characteristic | Typical Anomaly % |
|-------|----------------------------------|-------------------|
| **Isolation Forest** | Rapidly identifies global outliers. | 2% - 5% |
| **One-Class SVM** | Captures more subtle, non-linear patterns. | 3% - 6% |
| **K-Means** | Groups data into density clusters; distance-based. | 4% - 8% |

Isolation Forest was found to be the most efficient for large batches, while One-Class SVM was better at finding anomalies in data with more complex distributions.

## 5.3 Case Study: Network Delay and Outliers
In the testing phase, several records were flagged as anomalies not because of extreme sensor values, but because of high "Net Delay." For instance, records with a delay of over 120 seconds were visually flagged in red on the dashboard. This allowed the system to identify potential gateway hardware issues that a standard sensor-value monitor would have missed.

Furthermore, the IQR flagging successfully identified records where the `LogFloatValue` was physically possible but statistically improbable for that specific sensor type, adding an extra layer of validation before the machine learning phase.

## 5.4 Dashboard Utility
The implementation of the professional dashboard significantly improved the usability of the results. Key features like the **Device ID badge** and the **Excel Export** allowed for:
1.  Quickly identifying which station (`RmsStationId`) was failing.
2.  Exporting filtered anomaly lists into `.xlsx` format for management reporting.
3.  The use of color-coded badges (Green/Amber/Red) allowed for "at-a-glance" status monitoring of network health.
