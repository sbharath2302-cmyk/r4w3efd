# CubeSat Monitoring

A real-time CubeSat monitoring system that analyzes simulated spacecraft telemetry and detects abnormal behavior.
It uses an Isolation Forest machine learning model for anomaly detection and a rule-based system to identify the affected subsystem.
The results are displayed through an interactive web dashboard with a 3D CubeSat visualization.

## Features

* Real-time CubeSat telemetry simulation
* Isolation Forest-based anomaly detection
* 20-sample rolling means for temperature, signal strength, and packet loss
* Automatic subsystem fault identification
* Thermal, power, communication, and attitude fault simulation
* Real-time mission health monitoring dashboard
* Interactive 3D CubeSat visualization

## Machine Learning

The system uses a pre-trained **Isolation Forest** model to detect anomalous telemetry.

The model uses **12 features**, including:

* Battery voltage
* Battery current
* Solar power
* Temperature
* Temperature rolling mean
* Signal strength
* Signal strength rolling mean
* Packet loss
* Packet loss rolling mean
* Gyroscope X
* Gyroscope Y
* Gyroscope Z

The three rolling means are calculated over the most recent **20 telemetry samples**.

The Isolation Forest produces an anomaly score:

```text
Score < 0  →  Anomaly
Score ≥ 0  →  Normal
```

After an anomaly is detected, the rule engine analyzes the telemetry to determine the most likely affected subsystem.

## Fault Scenarios

The telemetry simulator can generate four different fault scenarios:

| Fault         | Simulated behavior                                                 |
| ------------- | ------------------------------------------------------------------ |
| Thermal       | Increasing spacecraft temperature                                  |
| Power         | Decreasing battery voltage and solar power with increasing current |
| Communication | Decreasing signal strength and increasing packet loss              |
| Attitude      | Increasing gyroscope values indicating abnormal rotation           |

### Run a fault scenario

From the `backend` folder:

```bash
python simulator.py --fault thermal
```

Available scenarios:

```bash
python simulator.py --fault thermal
python simulator.py --fault power
python simulator.py --fault communication
python simulator.py --fault attitude
```

To run the simulator under normal conditions:

```bash
python simulator.py
```

## How to Run

### 1. Clone the repository

```bash
git clone https://github.com/0xMrNight/cubesat-monitoring.git
cd cubesat-monitoring
```

### 2. Set up the backend

Open a terminal and go to the backend folder:

```bash
cd backend
```

Install the Python dependencies:

```bash
pip install -r requirements.txt
```

The ML model also requires the packages used to load and process the saved model:

```bash
pip install numpy joblib scikit-learn
```

Start the FastAPI server:

```bash
uvicorn main:app --reload
```

Keep this terminal running.

### 3. Start the frontend

Open a **new terminal** in the project folder:

```bash
cd frontend
```

Install the frontend dependencies:

```bash
npm install
```

Start the development server:

```bash
npm run dev
```

Vite will provide a local URL in the terminal. Open that URL in your browser.

### 4. Start the telemetry simulator

Open another terminal:

```bash
cd backend
python simulator.py
```

The simulator will continuously send telemetry to the backend.

To test a fault:

```bash
python simulator.py --fault thermal
```

The dashboard will receive the telemetry, run the anomaly detection model, and display the detected condition.
