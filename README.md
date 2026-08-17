# CubeSat Monitoring

A real-time CubeSat monitoring system that analyzes simulated telemetry and detects abnormal spacecraft behavior.
It uses an Isolation Forest model for anomaly detection and a rule-based system to identify the affected subsystem.

## Features

* Real-time telemetry simulation
* ML-based anomaly detection
* Automatic subsystem fault identification
* Multiple simulated spacecraft fault scenarios
* Real-time monitoring dashboard
* Interactive 3D CubeSat visualization

## Machine Learning

An **Isolation Forest** model is used to detect anomalies in CubeSat telemetry.

The model uses telemetry data along with **20-sample rolling means** for temperature, signal strength, and packet loss.

## Fault Scenarios

| Scenario        | Simulated Fault                                        |
| --------------- | ------------------------------------------------------ |
| `thermal`       | Increasing spacecraft temperature                      |
| `power`         | Battery voltage, current and solar power abnormalities |
| `communication` | Reduced signal strength and increased packet loss      |
| `attitude`      | Abnormal gyroscope readings                            |

## Run Locally

### 1. Clone

```bash
git clone https://github.com/0xMrNight/cubesat-monitoring.git
cd cubesat-monitoring
```

### 2. Backend

```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload
```

### 3. Frontend

Open a new terminal:

```bash
cd frontend
npm install
npm run dev
```

Open the URL shown by Vite.

### 4. Run the Simulator

Open another terminal:

```bash
cd backend
python simulator.py
```

To test a fault scenario:

```bash
python simulator.py --fault thermal
```
