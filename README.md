# CubeSat Monitoring

A real-time CubeSat monitoring system that analyzes simulated telemetry and detects abnormal spacecraft behavior.
It uses an Isolation Forest model for anomaly detection and a rule-based system to identify the affected subsystem.

## Features

* Real-time telemetry simulation
* ML-based anomaly detection
* Automatic subsystem fault identification
* Thermal, power, communication and attitude fault simulation
* Real-time monitoring dashboard
* Interactive 3D CubeSat visualization

## Machine Learning

An **Isolation Forest** model is used to detect anomalies in CubeSat telemetry.

The model uses 12 telemetry features, including three 20-sample rolling means for:

* Temperature
* Signal strength
* Packet loss

## Fault Scenarios

The simulator supports:

* **Thermal** — abnormal temperature
* **Power** — battery and solar power abnormalities
* **Communication** — signal strength and packet loss abnormalities
* **Attitude** — abnormal gyroscope readings

## Run Locally

### 1. Clone the repository

```bash
git clone https://github.com/0xMrNight/cubesat-monitoring.git
cd cubesat-monitoring
```

### 2. Start the backend

```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload
```

### 3. Start the frontend

Open a new terminal:

```bash
cd frontend
npm install
npm run dev
```

Open the URL shown by Vite in your browser.

### 4. Start the telemetry simulator

Open another terminal:

```bash
cd backend
python simulator.py
```

To test a fault scenario:

```bash
python simulator.py --fault thermal
```

Available options:

```text
thermal
power
communication
attitude
```
