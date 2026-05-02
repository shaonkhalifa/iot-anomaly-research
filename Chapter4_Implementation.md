# Chapter 4: System Implementation

## 4.1 System Architecture
The system is built using a three-tier decoupled architecture to ensure scalability and maintainability.

### 4.1.1 Frontend: Angular Presentation Layer
The frontend is developed using Angular, providing a responsive and interactive dashboard. 
- **Data Visualization**: Uses Chart.js to display anomaly distributions and sensor trends.
- **Data Export**: Implements the SheetJS library to generate proper `.xlsx` files for offline analysis.
- **State Management**: Handles file uploads and model selection dynamically.

### 4.1.2 Backend: .NET Core Service Layer
The backend is built with .NET Core (C#), serving as a robust API gateway.
- **Request Proxying**: Receives sensor data from the frontend and forwards it to the specialized ML service.
- **Typed Models**: Ensures data integrity by using strictly typed C# classes (e.g., `PredictionResult`) for all internal data movement.
- **Model Orchestration**: Manages the routing between different detection requests.

### 4.1.3 ML Service: Python Flask Analytics Layer
The machine learning logic resides in a high-performance Python service using the Flask framework.
- **Scikit-Learn Integration**: Uses the `sklearn` library for Isolation Forest, SVM, and K-Means.
- **Pandas Pipeline**: Implements the 9-stage cleaning logic using the Pandas library for efficient data manipulation.
- **JSON REST API**: Provides endpoints for single predictions, batch uploads, and multi-model comparisons.

## 4.2 Key Features Implementation

### 4.2.1 Real-time Comparison
A "Compare All Models" feature allows users to run the same dataset through all three algorithms simultaneously. This allows the user to see which models are more conservative or aggressive in their detection.

### 4.2.2 Network Delay Severity
The system calculates `time_delay_sec` and applies a severity classification in the UI:
- **Green (Normal)**: Delay ≤ 5 seconds.
- **Amber (Warning)**: Delay between 5 and 30 seconds.
- **Red (Critical)**: Delay > 30 seconds (pulsing animation in the dashboard).

### 4.2.3 Metadata Preservation
A major implementation challenge was ensuring that original IoT metadata (like `RmsStationId` and `NodeId`) was preserved throughout the ML pipeline. This was achieved by merging the ML results back with the original dataframes based on index, ensuring the final dashboard displays human-readable "Device IDs" rather than just row numbers.
