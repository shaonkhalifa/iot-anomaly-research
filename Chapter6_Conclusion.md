# Chapter 6: Conclusion and Future Work

## 6.1 Conclusion
This research successfully developed an integrated IoT Anomaly Detection System capable of processing complex industrial sensor data. By combining a 9-stage data cleaning pipeline with multiple unsupervised machine learning models, the system provides a high level of accuracy and diagnostic depth. 

The inclusion of metadata like "Network Delay" and "Device ID" transformed the project from a purely mathematical model into a practical industrial tool. The comparative analysis across Isolation Forest, SVM, and K-Means confirmed that no single model is perfect for all scenarios, but providing a unified interface for comparison allows experts to make informed decisions.

## 6.2 Key Achievements
- **Robust Pipeline**: Successfully handled real-world noisy data with automatic cleaning.
- **Visual Insights**: Surfaced critical network health metrics alongside sensor values.
- **System Portability**: Created a decoupled architecture that can easily be adapted for different sensor types.

## 6.3 Future Work
While the current system is effective for batch processing, future iterations could include:
1.  **Streaming Integration**: Implementing Kafka or MQTT listeners for true real-time, record-by-record processing.
2.  **Supervised Refinement**: Allowing users to "Confirm" or "Reject" anomalies in the dashboard to generate a labeled dataset for future supervised learning.
3.  **Edge Deployment**: Deploying the detection logic directly to IoT gateways to reduce network traffic.
