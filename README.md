# 🛡️ ShadowSentinel — Network Intrusion Detection System

<div align="center">

[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://reactjs.org/)
[![Machine Learning](https://img.shields.io/badge/ML-Anomaly%20Detection-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)](https://en.wikipedia.org/wiki/Anomaly_detection)
[![Security](https://img.shields.io/badge/Cybersecurity-IDS%2FIPS-1a1a2e?style=for-the-badge&logo=kalilinux&logoColor=white)](https://en.wikipedia.org/wiki/Intrusion_detection_system)
[![MITRE ATT&CK](https://img.shields.io/badge/MITRE-ATT%26CK-000000?style=for-the-badge&logo=mitre&logoColor=red)](https://attack.mitre.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

**AI-powered Network Intrusion Detection System — real-time packet analysis, ML anomaly detection, and MITRE ATT&CK mapping.**

[Features](#-features) · [Architecture](#-architecture) · [Installation](#-installation) · [API](#-api-endpoints)

</div>

---

## What Is ShadowSentinel?

ShadowSentinel is a full-stack **Network Intrusion Detection System (IDS)** that combines traditional signature-based detection with modern **machine learning anomaly detection**. It captures network traffic in real time, classifies threats using a trained ML model, maps them to the **MITRE ATT&CK framework**, and presents everything through a clean React dashboard.

Built for security researchers, students, and anyone who wants to understand what's happening on their network — not just block it, but **comprehend** it.

---

## ✨ Features

- **📡 Real-time Packet Capture** — Live network traffic analysis using raw sockets / libpcap
- **🤖 ML Anomaly Detection** — Isolation Forest model trained on network flow features to detect zero-day attacks
- **📋 Signature-Based Detection** — Rule engine matching known attack patterns (Snort-compatible rules)
- **🗺️ MITRE ATT&CK Mapping** — Every alert is mapped to the relevant MITRE ATT&CK technique and tactic
- **📊 React Dashboard** — Real-time alert feed, traffic visualization, threat timeline, and statistics
- **🔔 Alerting** — Configurable webhook notifications (Slack, Discord, custom endpoints)
- **📈 Traffic Analytics** — Protocol distribution, top talkers, bandwidth usage over time
- **🔍 Deep Packet Inspection** — Extract and analyze HTTP headers, DNS queries, TLS handshakes
- **📤 PCAP Export** — Export suspicious traffic captures for offline analysis in Wireshark
- **🔐 REST API** — Full programmatic access to alerts, stats, and configuration

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    ShadowSentinel                        │
├──────────────────────┬──────────────────────────────────┤
│   Backend (Python)   │      Frontend (React)            │
│                      │                                  │
│  ┌────────────────┐  │  ┌──────────────────────────┐   │
│  │  Packet Capture │  │  │    React Dashboard       │   │
│  │  Engine         │  │  │                          │   │
│  └───────┬────────┘  │  │  ┌────────┐ ┌──────────┐ │   │
│          │           │  │  │ Alerts │ │ Traffic  │ │   │
│  ┌───────▼────────┐  │  │  │ Feed   │ │ Charts   │ │   │
│  │  Feature        │  │  │  └────────┘ └──────────┘ │   │
│  │  Extraction     │  │  │  ┌────────┐ ┌──────────┐ │   │
│  └───────┬────────┘  │  │  │ MITRE  │ │ Timeline │ │   │
│          │           │  │  │ Matrix │ │ View     │ │   │
│  ┌───────▼────────┐  │  │  └────────┘ └──────────┘ │   │
│  │  Detection      │  │  └──────────────────────────┘   │
│  │  Pipeline       │  │                                  │
│  │  ┌────────────┐ │  │  Served via FastAPI static files │
│  │  │ ML Model   │ │  │  or Vite dev server              │
│  │  │ (Isolation │ │  │                                  │
│  │  │  Forest)   │ │  │                                  │
│  │  └────────────┘ │  │                                  │
│  │  ┌────────────┐ │  │                                  │
│  │  │ Signature  │ │  │                                  │
│  │  │ Engine     │ │  │                                  │
│  │  └────────────┘ │  │                                  │
│  └───────┬────────┘  │                                  │
│          │           │                                  │
│  ┌───────▼────────┐  │                                  │
│  │  MITRE ATT&CK   │  │                                  │
│  │  Mapper         │  │                                  │
│  └───────┬────────┘  │                                  │
│          │           │                                  │
│  ┌───────▼────────┐  │                                  │
│  │  FastAPI        │  │                                  │
│  │  REST Server    │◄─┼─── WebSocket (real-time alerts)  │
│  └────────────────┘  │                                  │
│                      │                                  │
│  ┌────────────────┐  │                                  │
│  │  SQLite /       │  │                                  │
│  │  PostgreSQL     │  │                                  │
│  └────────────────┘  │                                  │
└──────────────────────┴──────────────────────────────────┘
```

### Project Structure

```
shadowsentinel/
├── backend/
│   ├── main.py                  # FastAPI app entry point
│   ├── config.py                # Configuration management
│   ├── capture/
│   │   ├── __init__.py
│   │   ├── engine.py            # Packet capture engine (pcap/raw sockets)
│   │   └── parser.py            # Protocol parser (Ethernet, IP, TCP, UDP, HTTP, DNS)
│   ├── detection/
│   │   ├── __init__.py
│   │   ├── ml_model.py          # Isolation Forest anomaly detection
│   │   ├── signature.py         # Rule-based signature matching
│   │   └── pipeline.py          # Detection orchestration pipeline
│   ├── mitre/
│   │   ├── __init__.py
│   │   ├── mapper.py            # Alert → MITRE ATT&CK technique mapping
│   │   └── tactics.json         # MITRE ATT&CK tactics and techniques data
│   ├── api/
│   │   ├── __init__.py
│   │   ├── routes/
│   │   │   ├── alerts.py        # Alert CRUD endpoints
│   │   │   ├── stats.py         # Statistics endpoints
│   │   │   ├── capture.py       # Capture control endpoints
│   │   │   └── config.py        # Configuration endpoints
│   │   └── websocket.py         # Real-time alert WebSocket
│   ├── models/
│   │   ├── __init__.py
│   │   ├── alert.py             # Alert database model
│   │   └── flow.py              # Network flow database model
│   ├── database.py              # Database connection and session management
│   └── requirements.txt
├── frontend/
│   ├── src/
│   │   ├── App.jsx
│   │   ├── components/
│   │   │   ├── AlertFeed.jsx       # Real-time alert list
│   │   │   ├── TrafficChart.jsx    # Protocol/bandwidth charts
│   │   │   ├── MitreMatrix.jsx     # MITRE ATT&CK heat map
│   │   │   ├── TimelineView.jsx    # Threat timeline
│   │   │   └── StatsPanel.jsx      # Summary statistics
│   │   ├── services/
│   │   │   └── api.js              # API client
│   │   └── styles/
│   │       └── dashboard.css
│   ├── package.json
│   └── vite.config.py
├── ml/
│   ├── train.py                 # Model training script
│   ├── features.py              # Feature extraction from network flows
│   └── model.pkl                # Serialized Isolation Forest model
├── rules/
│   └── custom.rules             # Custom Snort-compatible detection rules
├── README.md
└── docker-compose.yml
```

---

## 🤖 ML Anomaly Detection

ShadowSentinel uses an **Isolation Forest** algorithm trained on network flow features to detect anomalous traffic that doesn't match any known signature.

### Features Used

| Feature | Description |
|---------|-------------|
| `duration` | Flow duration in seconds |
| `protocol` | Protocol type (TCP=6, UDP=17, ICMP=1) |
| `src_bytes` | Bytes sent from source to destination |
| `dst_bytes` | Bytes sent from destination to source |
| `packet_count` | Total packets in the flow |
| `avg_packet_size` | Mean packet size in the flow |
| `tcp_flags` | Aggregated TCP flags (SYN, ACK, RST, etc.) |
| `dst_port` | Destination port number |

### Training

The model is trained on the **CICIDS2017** dataset (or your own captured traffic):

```bash
python ml/train.py --data data/cicids2017.csv --output ml/model.pkl
```

Anomalies are flagged when the model's anomaly score exceeds the configurable threshold (default: `-0.5`).

---

## 🗺️ MITRE ATT&CK Mapping

Every alert is automatically mapped to the relevant MITRE ATT&CK technique:

| Alert Type | MITRE Technique | Tactic |
|------------|----------------|--------|
| Port Scan | T1046 — Network Service Discovery | Discovery |
| Brute Force | T1110 — Brute Force | Credential Access |
| DDoS | T1498 — Network Denial of Service | Impact |
| DNS Tunneling | T1071.004 — DNS | Command and Control |
| SQL Injection | T1190 — Exploit Public-Facing Application | Initial Access |
| XSS | T1189 — Drive-by Compromise | Initial Access |
| Data Exfiltration | T1041 — Exfiltration Over C2 Channel | Exfiltration |
| Malware C2 | T1071 — Application Layer Protocol | Command and Control |

The dashboard displays an interactive **MITRE ATT&CK heat map** showing which techniques have been observed on your network.

---

## 🚀 Installation

### Prerequisites

- **Python 3.10+**
- **Node.js 18+**
- **pip** and **npm**

### Backend Setup

```bash
git clone https://github.com/mayank-dev-15/shadowsentinel.git
cd shadowsentinel/backend

# Create virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Initialize database
python -c "from database import init_db; init_db()"

# Train the ML model (optional — a pre-trained model is included)
python ../ml/train.py --data ../data/sample.csv --output ../ml/model.pkl
```

### Frontend Setup

```bash
cd ../frontend
npm install
npm run build
```

### Run

```bash
# From the backend directory
uvicorn main:app --host 0.0.0.0 --port 8000
```

Open `http://localhost:8000` in your browser.

### Docker (Alternative)

```bash
docker-compose up --build
```

---

## 📖 Usage

1. **Start the backend**: `uvicorn main:app --reload`
2. **Access the dashboard**: Open `http://localhost:8000`
3. **Start packet capture**: Click "Start Capture" in the dashboard or call the API:
   ```bash
   curl -X POST http://localhost:8000/api/capture/start \
     -H "Content-Type: application/json" \
     -d '{"interface": "eth0", "filter": "tcp"}'
   ```
4. **Monitor alerts**: The alert feed updates in real time via WebSocket
5. **Review MITRE mapping**: Click any alert to see the mapped ATT&CK technique and recommended mitigations

---

## 📡 API Endpoints

### Alerts

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/alerts` | List all alerts (paginated) |
| `GET` | `/api/alerts/{id}` | Get alert details |
| `GET` | `/api/alerts/recent?limit=20` | Get recent alerts |
| `DELETE` | `/api/alerts/{id}` | Delete an alert |
| `PATCH` | `/api/alerts/{id}` | Update alert status (acknowledged, resolved) |

### Statistics

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/stats/overview` | Dashboard overview stats |
| `GET` | `/api/stats/protocols` | Protocol distribution |
| `GET` | `/api/stats/talkers` | Top talkers by traffic volume |
| `GET` | `/api/stats/timeline` | Alert count over time |
| `GET` | `/api/stats/mitre` | MITRE ATT&CK technique counts |

### Capture Control

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/capture/start` | Start packet capture |
| `POST` | `/api/capture/stop` | Stop packet capture |
| `GET` | `/api/capture/status` | Get capture status |
| `POST` | `/api/capture/export` | Export suspicious PCAP |

### WebSocket

| Endpoint | Description |
|----------|-------------|
| `ws://localhost:8000/ws/alerts` | Real-time alert stream |

---

## 📸 Screenshots

> *Dashboard preview — real-time alert feed with MITRE ATT&CK mapping and traffic analytics.*

```
┌─────────────────────────────────────────────────────────────┐
│  🛡️ ShadowSentinel                    [Start] [Stop] [⚙️]  │
├──────────────┬──────────────────────────────────────────────┤
│  ALERTS (12) │  MITRE ATT&CK Matrix                        │
│              │                                              │
│  🔴 Port Scan│  ██ Discovery    ██ Credential Access       │
│  🔴 Brute F. │  ██ Lateral Mov. ░░ Exfiltration            │
│  🟡 DNS Tunn.│  ██ C2           ░░ Impact                  │
│  🟡 Anomaly  │                                              │
│  🔴 SQL Inj. │  TRAFFIC ANALYTICS                          │
│              │  TCP: 67%  ██░░░░░░░░                        │
│              │  UDP: 23%  █░░░░░░░░░                        │
│              │  ICMP: 5%  ░░░░░░░░░░                        │
│              │  Other: 5% ░░░░░░░░░░                        │
└──────────────┴──────────────────────────────────────────────┘
```

---

## 📄 License

This project is open source under the [MIT License](https://opensource.org/licenses/MIT).

---

<div align="center">

🛡️ *"The best defense is understanding the offense."*

**⭐ Star this repo if ShadowSentinel helped you see the shadows on your network.**

</div>
