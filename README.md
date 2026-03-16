# Digital Twin for Resource-Constrained Systems (IoT/Embedded Focus)

Overview
This project demonstrates a proof-of-concept **Digital Twin** for thermal state monitoring. It integrates Python simulation with the ThingsBoard IoT platform to implement an **Active Decision Support System (DSS)**. The goal is to move from reactive logging to autonomous, pro-active anomaly management in real-time.

Live Environment Access

| Component | Status | Link |
| :--- | :--- | :--- |
| **Code Simulation** | Live | [**Click to Open & Run in Google Colab**](https://colab.research.google.com/drive/1jDyAVMYbERqm9PCjww491LX7KJYUrJ6O?authuser=0#scrollTo=_8YGMyvOZ_Me) |
| **Live Dashboard (HMI)** | Active | [**Click to View Live ThingsBoard Dashboard**](https://demo.thingsboard.io/dashboards/f7f8f720-d9b2-11f0-aedf-65a2559b1d36) |

 Architecture & Methodology

### 1. Virtual Edge / Simulation Layer (Python/Colab)
* **Stochastic Modeling:** Utilizes Python's `random.gauss` to simulate realistic thermal data, including inherent noise and gradual thermal drift over time.
* **Protocol Implementation:** Uses the **paho-mqtt** library to securely publish telemetry data (JSON payload) to the ThingsBoard MQTT endpoint.

### 2. Cloud Intelligence (ThingsBoard Rule Engine)
* **Active DSS Implementation:** The rule chain is configured to act as an Active Decision Support System, performing logic autonomously without human intervention.
* **Low-Latency Anomaly Detection:** A simultaneous **JavaScript filter** is applied to the incoming data stream to detect critical events (e.g., temperature threshold $\mathbf{>55^\circ C}$) with minimal processing latency.
* **Event Triggering:** Upon detection, the Rule Engine automatically generates a persistent **Critical Alarm** and updates the device's state.

### 3. Validation & Rigor
* **Fault Injection Testing:** The Python simulation includes logic for **Fault Injection** (sudden, controlled temperature spikes) to rigorously test the Rule Engine's robustness and ensure zero false-negatives in alarm creation.
* **End-to-End Validation (E2E):** Confirmed that a simulated fault in the Colab notebook results in an instantaneous state change on the ThingsBoard dashboard and an entry in the Alarm Table.

---
