<div align="center">

<br/>

```
╔══════════════════════════════════════════════════════════════╗
║                                                              ║
║        🏥  SMART PATIENT HEALTH MONITORING SYSTEM           ║
║                   Edge AI · Flask · MySQL                    ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
```

<br/>

[![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Flask](https://img.shields.io/badge/Flask-3.0-000000?style=for-the-badge&logo=flask&logoColor=white)](https://flask.palletsprojects.com)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://mysql.com)
[![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-ML-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)](https://scikit-learn.org)
[![Edge AI](https://img.shields.io/badge/Edge%20AI-Edge%20Impulse-00A67E?style=for-the-badge)](https://edgeimpulse.com)
[![License](https://img.shields.io/badge/License-Academic-purple?style=for-the-badge)](LICENSE)

<br/>

> **A full-stack healthcare monitoring platform** combining edge computing, on-device AI inference,  
> real-time doctor alerts, role-based dashboards, PDF reports, and ESP32/Arduino integration.

<br/>

**Developed by Aniket Nihal · 2026**

---

</div>

## 📋 Table of Contents

| | Section |
|---|---|
| 🔭 | [Overview](#-overview) |
| ✨ | [Key Features](#-key-features) |
| 🏗️ | [Full Architecture](#-full-architecture) |
| 🔄 | [System Workflow](#-system-workflow) |
| 🗄️ | [Database Design](#-database-design) |
| 🤖 | [AI & Edge Intelligence](#-ai--edge-intelligence) |
| 🛠️ | [Technology Stack](#-technology-stack) |
| 📁 | [Project Structure](#-project-structure) |
| 🚀 | [Installation & Setup](#-installation--setup) |
| 🔌 | [Edge Impulse Integration](#-edge-impulse-integration) |
| 📡 | [API Reference](#-api-reference) |
| 🧪 | [Testing](#-testing) |
| 🔮 | [Future Scope](#-future-scope) |

---

## 🔭 Overview

The **Smart Patient Health Monitoring System** is a full-stack healthcare web application that monitors patient vitals in real time using **edge AI**, a **server-side ML model**, and **role-based dashboards** for patients, doctors, and admins.

```
Vitals Monitored:  Heart Rate · Body Temperature · SpO₂ · Blood Pressure · Glucose
```

### Health Classification

| Status | Color | Meaning |
|---|---|---|
| ✅ `Normal` | 🟢 Green | Patient vitals are within safe range |
| ⚠️ `Warning` | 🟡 Yellow | Vitals need doctor attention |
| 🚨 `Critical` | 🔴 Red | Immediate medical attention required |

---

## ✨ Key Features

<table>
<tr>
<td width="50%">

**🔐 Authentication & Security**
- Patient · Doctor · Admin roles
- bcrypt password hashing
- Flask session management
- `.env` credential isolation
- Edge device token auth

</td>
<td width="50%">

**📊 Dashboards**
- Patient: vitals, history, charts, alerts
- Doctor: assigned patients, active alerts
- Admin: user management, system stats
- Real-time health status display

</td>
</tr>
<tr>
<td width="50%">

**🤖 AI Prediction**
- Random Forest classifier (Scikit-learn)
- On-device Edge Impulse inference
- Rule-based safety override layer
- Most-critical-status-wins combiner

</td>
<td width="50%">

**📡 Edge Computing**
- Sensor simulation & buffering
- Noise filtering & aggregation
- ESP32 / Arduino ready API
- Demo mode without hardware

</td>
</tr>
<tr>
<td width="50%">

**🔔 Smart Alerts**
- Auto warning/critical alerts
- Doctor notification system
- Email alert utility
- Alert history tracking

</td>
<td width="50%">

**📄 Reports**
- PDF generation with ReportLab
- Full health history export
- Seminar-ready deliverables
- LinkedIn post image export

</td>
</tr>
</table>

---

## 🏗️ Full Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                          USER LAYER                                  │
│                                                                      │
│    ┌─────────────┐      ┌─────────────┐      ┌─────────────┐       │
│    │   Patient   │      │    Doctor   │      │    Admin    │       │
│    │  Dashboard  │      │   Alerts    │      │   Control   │       │
│    └──────┬──────┘      └──────┬──────┘      └──────┬──────┘       │
└───────────┼─────────────────────┼─────────────────────┼─────────────┘
            │                     │                     │
            └─────────────────────┼─────────────────────┘
                                  │
                                  ▼
┌─────────────────────────────────────────────────────────────────────┐
│                       FLASK APPLICATION LAYER                        │
│                                                                      │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐           │
│  │   Auth   │  │ Patient  │  │  Doctor  │  │  Admin   │           │
│  │  Routes  │  │  Routes  │  │  Routes  │  │  Routes  │           │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘           │
│                                                    ┌──────────┐     │
│                                                    │ Edge API │     │
│                                                    │ /vitals  │     │
│                                                    └────┬─────┘     │
└─────────────────────────────────────────────────────────┼───────────┘
         │                                               │
         │                        ┌──────────────────────┘
         │                        │
         ▼                        ▼
┌──────────────────┐   ┌──────────────────────────────────────────────┐
│  EDGE DEVICE     │   │           AI + INTELLIGENCE LAYER             │
│  LAYER           │   │                                               │
│                  │   │  ┌─────────────┐    ┌─────────────────────┐  │
│ ┌──────────────┐ │   │  │  Payload    │    │   Rule Safety       │  │
│ │Health Sensors│ │   │  │ Normalizer  │───▶│   Check             │  │
│ │HR · SpO₂    │ │   │  │Field mapping│    │Extreme vitals gate  │  │
│ │Temp · BP    │ │   │  └──────┬──────┘    └──────────┬──────────┘  │
│ └──────┬───────┘ │   │         │                       │             │
│        │         │   │         ▼                       ▼             │
│ ┌──────▼───────┐ │   │  ┌─────────────┐    ┌──────────────────┐    │
│ │  ESP32 /     │ │   │  │   Random    │    │  Prediction      │    │
│ │  Arduino     │─┼──▶│  │   Forest    │───▶│  Combiner        │    │
│ └──────┬───────┘ │   │  │  Classifier │    │ Most serious     │    │
│        │         │   │  │health_model │    │    wins          │    │
│ ┌──────▼───────┐ │   │  │    .pkl     │    └──────────────────┘    │
│ │Edge Impulse  │─┼──▶│  └─────────────┘                            │
│ │Normal/Warn/  │ │   │                                               │
│ │Critical label│ │   └───────────────────────────────────────────────┘
│ └──────────────┘ │                         │
└──────────────────┘                         │
                                             ▼
┌─────────────────────────────────────────────────────────────────────┐
│                        MYSQL DATABASE LAYER                          │
│                                                                      │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐                          │
│  │  users   │  │ doctors  │  │ patients │                          │
│  │credentials│  │profile · │  │profile · │                          │
│  │  roles   │  │specialty │  │doctor_id │                          │
│  └──────────┘  └──────────┘  └──────────┘                          │
│                                                                      │
│  ┌──────────────┐  ┌──────────┐  ┌──────────┐                      │
│  │health_records│  │  alerts  │  │ reports  │                      │
│  │vitals+status │  │warn/crit │  │PDF meta  │                      │
│  │edge · manual │  │doctor_id │  │  data    │                      │
│  └──────────────┘  └──────────┘  └──────────┘                      │
└─────────────────────────────────────────────────────────────────────┘
                                             │
                                             ▼
┌─────────────────────────────────────────────────────────────────────┐
│                    OUTPUT + NOTIFICATION LAYER                        │
│                                                                      │
│   ┌──────────────┐  ┌──────────────┐  ┌────────────────────────┐   │
│   │    Live      │  │    Email     │  │      PDF Reports       │   │
│   │  Dashboards  │  │    Alerts    │  │  ReportLab · History   │   │
│   │Patient/Doctor│  │ Warn/Critical│  │  Seminar Deliverables  │   │
│   │  /Admin      │  │  to Doctor   │  │  LinkedIn Post Image   │   │
│   └──────────────┘  └──────────────┘  └────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 🔄 System Workflow

```
  Health Sensor
       │
       │  collect HR, SpO₂, Temperature, BP, Glucose
       ▼
  ESP32 / Arduino
       │
       │  run Edge Impulse model on-device
       ▼
  Edge Impulse Label  ──────────────────────────────────────────────┐
  Normal / Warning / Critical                                        │
       │                                                             │
       │  POST /api/edge/vitals  (X-Edge-Token required)            │
       ▼                                                             │
  Flask Edge API                                                     │
       │                                                             │
       │  validate token + payload                                   │
       ▼                                                             │
  Payload Normalizer                                                 │
       │                                                             │
       ├──────────────────────────┐                                 │
       ▼                          ▼                                 │
  Rule Safety Check         Random Forest ML                       │
  (extreme vitals)          (health_model.pkl)                     │
       │                          │                                 │
       └──────────────────────────┘                                 │
                      │                                             │
                      ▼                                             │
             Prediction Combiner  ◄────────────────────────────────┘
             Most serious status wins
                      │
          ┌───────────┴───────────┐
          ▼                       ▼
     Save to DB             Create Alert?
  health_records            (if Warning
                            or Critical)
          │                       │
          ▼                       ▼
    Patient history         Doctor dashboard
    updated                 alert activated
```

---

## 🗄️ Database Design

```
┌──────────────────────────────────────────────────────────────┐
│                        SCHEMA OVERVIEW                        │
└──────────────────────────────────────────────────────────────┘

users                          doctors
──────────────────────         ──────────────────────
id          INT PK             id            INT PK
name        VARCHAR            user_id       INT FK → users.id
email       VARCHAR UNIQUE     specialization VARCHAR
password    VARCHAR (bcrypt)   license_no    VARCHAR
role        ENUM(patient,      created_at    TIMESTAMP
            doctor,admin)
created_at  TIMESTAMP

patients                       health_records
──────────────────────         ──────────────────────
id          INT PK             id            INT PK
user_id     INT FK → users.id  patient_id    INT FK → patients.id
doctor_id   INT FK → doctors   heart_rate    FLOAT
age         INT                spo2          FLOAT
gender      VARCHAR            temperature   FLOAT
blood_group VARCHAR            bp_systolic   INT
created_at  TIMESTAMP          bp_diastolic  INT
                               glucose       FLOAT
alerts                         health_status ENUM(Normal,
──────────────────────                       Warning,Critical)
id          INT PK             source        ENUM(manual,
patient_id  INT FK → patients              simulated,edge)
doctor_id   INT FK → doctors   device_id     VARCHAR
alert_type  ENUM(Warning,      created_at    TIMESTAMP
            Critical)
message     TEXT               reports
is_read     BOOLEAN            ──────────────────────
created_at  TIMESTAMP          id            INT PK
                               patient_id    INT FK → patients
                               file_path     VARCHAR
                               created_at    TIMESTAMP
```

Schema file: `database/schema.sql`

---

## 🤖 AI & Edge Intelligence

### On-Device — Edge Impulse (ESP32 / Arduino)

```
Sensors ──▶ Feature Extraction ──▶ Edge Impulse Model ──▶ Label + Confidence
              (HR, SpO₂, Temp)       (TFLite / EON)          0.0 – 1.0
```

- Trained and deployed via [Edge Impulse Studio](https://studio.edgeimpulse.com)
- Runs entirely on the microcontroller — no cloud dependency
- Returns `{ "label": "Warning", "confidence": 0.91 }`

### Server-Side — Random Forest Classifier

```python
Features: [heart_rate, spo2, temperature, bp_systolic, bp_diastolic, glucose]
Model:     RandomForestClassifier (Scikit-learn)
Output:    Normal | Warning | Critical
File:      ai/health_model.pkl
```

### Prediction Combiner Logic

```
edge_result  = "Warning"    (confidence: 0.91)
server_result = "Normal"    (ML prediction)
rule_result   = "Normal"    (no extreme vitals)

Final = max(edge, server, rule) by severity
Final = "Warning"  ✅
```

> **The most serious status always wins** — safety is the priority.

---

## 🛠️ Technology Stack

| Layer | Technology | Purpose |
|---|---|---|
| Frontend | HTML5 · CSS3 · JavaScript · Bootstrap 5 | Responsive dashboards |
| Backend | Python 3.11+ · Flask 3.0 | Routing · Business logic |
| Database | MySQL 8.0 | Persistent data storage |
| ML Model | Scikit-learn · Pandas · NumPy · Joblib | Health classification |
| Edge AI | Edge Impulse · ESP32 / Arduino | On-device inference |
| PDF | ReportLab | Health report generation |
| Security | bcrypt · Flask sessions · `.env` | Auth + credential safety |
| Deployment | Gunicorn · Procfile | Production server |

---

## 📁 Project Structure

```
smart_health_monitering/
│
├── app.py                          # Application entry point
├── config.py                       # Config + env loading
├── requirements.txt
├── Procfile                        # Gunicorn deployment
├── .env.example
│
├── ai/
│   ├── train_model.py              # Train Random Forest
│   ├── predict.py                  # Prediction helper
│   └── health_model.pkl            # Trained model artifact
│
├── database/
│   └── schema.sql                  # Full DB schema + seed data
│
├── edge/
│   ├── edge_processor.py           # Sensor buffering + aggregation
│   ├── sensor_simulator.py         # Simulated vitals generator
│   ├── edge_impulse.py             # Edge Impulse integration
│   └── send_demo_reading.py        # Hardware-free demo script
│
├── models/
│   ├── user_model.py
│   ├── patient_model.py
│   └── doctor_model.py
│
├── routes/
│   ├── auth.py                     # Login · Register · Logout
│   ├── patient.py                  # Patient dashboard + records
│   ├── doctor.py                   # Doctor dashboard + alerts
│   ├── admin.py                    # User management
│   ├── pdf_report.py               # PDF generation
│   └── edge_api.py                 # /api/edge/* endpoints
│
├── templates/                      # Jinja2 HTML templates
│   ├── index.html
│   ├── login.html
│   ├── register.html
│   ├── patient_dashboard.html
│   ├── doctor_dashboard.html
│   ├── admin_dashboard.html
│   └── reports.html
│
├── static/
│   ├── css/
│   └── js/
│
├── docs/
│   ├── EDGE_IMPULSE_SETUP.md
│   ├── ER_diagram.png
│   └── DFD.png
│
└── seminar_deliverables/
    ├── SmartHealth_Seminar_Presentation.pptx
    ├── SmartHealth_Seminar_Presentation.pdf
    ├── Edge_Impulse_Features_Step_By_Step.pdf
    └── SmartHealth_LinkedIn_Post_Image.png
```

---

## 🚀 Installation & Setup

### Prerequisites

- Python 3.11+
- MySQL 8.0
- pip

---

### Step 1 — Clone the repository

```bash
git clone https://github.com/your-username/smart-health-monitoring.git
cd smart-health-monitoring
```

### Step 2 — Create virtual environment

```powershell
# Windows PowerShell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

```bash
# macOS / Linux
python3 -m venv .venv
source .venv/bin/activate
```

### Step 3 — Install dependencies

```bash
pip install -r requirements.txt
```

### Step 4 — Configure environment

```bash
cp .env.example .env
```

Edit `.env`:

```env
SECRET_KEY=your-secret-key-here
DB_HOST=localhost
DB_PORT=3306
DB_USER=your_mysql_user
DB_PASSWORD=your_mysql_password
DB_NAME=smart_health_db
EDGE_DEVICE_TOKEN=smarthealth-edge-demo-token
```

### Step 5 — Create database

```bash
mysql -u your_mysql_user -p < database/schema.sql
```

### Step 6 — Train the ML model

```bash
python ai/train_model.py
```

### Step 7 — Run the app

```bash
python app.py
```

Open → **http://127.0.0.1:5000**

---

## 🔑 Demo Login Credentials

| Role | Email | Password |
|---|---|---|
| 🛡️ Admin | `admin@smarthealth.com` | `helloworld` |
| 🩺 Doctor | `doctor@smarthealth.com` | `helloworld` |
| 🧑 Patient | `patient@smarthealth.com` | `helloworld` |

> Credentials are seeded via `database/schema.sql`

---

## 🔌 Edge Impulse Integration

### Purpose

Edge Impulse deploys a lightweight TFLite/EON model directly onto the ESP32 or Arduino, enabling **on-device health classification** without requiring an internet connection during inference.

### Device Flow

```
1. Sensors collect HR, SpO₂, Temperature
2. Edge Impulse model classifies on-device → Normal / Warning / Critical
3. ESP32 sends JSON + token to POST /api/edge/vitals
4. Flask validates token and payload
5. Server runs rule check + ML as safety net
6. MySQL stores health record
7. Warning/Critical → doctor alert created
```

### Setup Guide

```
docs/EDGE_IMPULSE_SETUP.md
```

### Demo Without Hardware

```bash
# Normal reading
python edge/send_demo_reading.py --patient-id 1 --mode normal

# Warning reading
python edge/send_demo_reading.py --patient-id 1 --mode warning

# Critical reading
python edge/send_demo_reading.py --patient-id 1 --mode critical
```

---

## 📡 API Reference

### Health Check

```http
GET /api/edge/health
```

```json
{ "status": "ok", "timestamp": "2026-01-01T00:00:00Z" }
```

---

### Send Live Vitals

```http
POST /api/edge/vitals
Content-Type: application/json
X-Edge-Token: smarthealth-edge-demo-token
```

**Request body:**

```json
{
  "patient_id": 1,
  "device_id": "esp32-health-band-01",
  "heart_rate": 96,
  "spo2": 94,
  "temperature": 38.2,
  "bp_systolic": 130,
  "bp_diastolic": 86,
  "glucose": 110,
  "edge_impulse": {
    "label": "Warning",
    "confidence": 0.91
  }
}
```

**Response — success:**

```json
{
  "status": "success",
  "health_status": "Warning",
  "record_id": 42,
  "alert_created": true
}
```

**Response — error:**

```json
{
  "status": "error",
  "message": "Invalid or missing edge token"
}
```

---

## 🧪 Testing

### Run test suite

```bash
pip install pytest
python -m pytest tests/test_system.py -v
```

### Compile verification

```bash
python -m compileall app.py routes edge models ai tests
```

### Manual API test (curl)

```bash
curl -X POST http://localhost:5000/api/edge/vitals \
  -H "Content-Type: application/json" \
  -H "X-Edge-Token: smarthealth-edge-demo-token" \
  -d '{
    "patient_id": 1,
    "device_id": "test-device",
    "heart_rate": 110,
    "spo2": 91,
    "temperature": 39.1,
    "bp_systolic": 145,
    "bp_diastolic": 95,
    "glucose": 180,
    "edge_impulse": { "label": "Critical", "confidence": 0.97 }
  }'
```

---

## 🔮 Future Scope

| Feature | Description |
|---|---|
| 📟 Real ESP32 firmware | Production-ready sensor firmware with Edge Impulse classifier |
| ⚡ WebSocket dashboards | Live push updates without page refresh |
| 📱 Mobile app | Patient mobile application (React Native / Flutter) |
| 💬 SMS / WhatsApp alerts | Multi-channel doctor notification |
| ☁️ Cloud deployment | Managed MySQL on AWS RDS / GCP Cloud SQL |
| 📅 Appointment scheduling | Doctor-patient appointment system |
| 💓 ECG monitoring | Electrocardiogram waveform tracking |
| 🤸 Fall detection | Accelerometer-based fall alert via edge device |
| 🧠 Advanced ML | LSTM time-series prediction for trend analysis |

---

## 👨‍💻 Author

<div align="center">

**Aniket Nihal**

*Smart Patient Health Monitoring System using Edge Computing*  
*Year: 2026*

</div>

---

## 📄 License

This project is developed for **academic and learning purposes**.

---

<div align="center">

```
Built with  Flask · Scikit-learn · Edge Impulse · MySQL · ReportLab
```

⭐ **Star this repo if you found it useful!** ⭐

</div>
