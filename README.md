# shadowsentinel

[![Live Demo](https://img.shields.io/badge/🚀_Live_Demo-Visit-blue?style=for-the-badge)](https://mayank-dev-15.github.io/shadowsentinel-demo)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![Language](https://img.shields.io/badge/Language-Python-green)

AI-Powered Network Intrusion Detection System with real-time packet analysis, ML anomaly detection, and MITRE ATT&CK mapping.

`security` `ids` `machine-learning` `network` `mitre-attack`

---

## ✨ Features

- Real-time packet capture and analysis
- ML anomaly detection using Isolation Forest
- MITRE ATT&CK technique mapping (10+ techniques)
- Alert generation with severity levels
- FastAPI REST API
- React dashboard with live updates
- WebSocket for real-time alerts
- SQLite storage for packets and alerts
- Simulated packet capture engine

---

## 🚀 Live Demo

**[View Demo →](https://mayank-dev-15.github.io/shadowsentinel-demo)**

The demo is hosted on GitHub Pages. No installation needed — just click and explore.

---

## 🛠️ Tech Stack

- Python 3.11+
- FastAPI
- React
- scikit-learn
- Isolation Forest
- SQLite
- MITRE ATT&CK
- Docker

---

## 📦 Installation

```bash
git clone https://github.com/mayank-dev-15/shadowsentinel.git
cd shadowsentinel
```

```bash
cd shadowsentinel
pip install -r requirements.txt
cd backend && uvicorn app.main:app --reload
# In another terminal
cd frontend && npm install && npm start
# Or use Docker
docker-compose up
```

---

## 💡 Usage

- Start the backend: `uvicorn app.main:app --reload`
- Start the frontend: `npm start`
- Dashboard at `http://localhost:3000`
- API docs at `http://localhost:8000/docs`
- The system generates simulated traffic with occasional anomalies

---

## 📁 Project Structure

```
shadowsentinel/
├── README.md          # This file
├── Demo.md            # Demo documentation
├── LICENSE            # MIT License
└── ...                # Source files
```

---

## 🤝 Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request.

---

## 📄 License

This project is licensed under the MIT License.

---

## 🔗 Links

- **Live Demo:** [https://mayank-dev-15.github.io/shadowsentinel-demo](https://mayank-dev-15.github.io/shadowsentinel-demo)
- **Source Code:** [github.com/mayank-dev-15/shadowsentinel](https://github.com/mayank-dev-15/shadowsentinel)
- **Issues:** [github.com/mayank-dev-15/shadowsentinel/issues](https://github.com/mayank-dev-15/shadowsentinel/issues)
- **Releases:** [github.com/mayank-dev-15/shadowsentinel/releases](https://github.com/mayank-dev-15/shadowsentinel/releases)
- **Demo Docs:** [Demo.md](https://github.com/mayank-dev-15/shadowsentinel/blob/main/Demo.md)

---

*Built with ❤️ by [Mayank Basena](https://github.com/mayank-dev-15) · 15 · GSoC 2027 Aspirant*

---

## ⚠️ Attribution & Credit Notice

This project is created and maintained by **Mayank Basena** ([@mayank-dev-15](https://github.com/mayank-dev-15)).

If you fork, use, modify, or derive work from this repository, **you must give proper credit** to the original author. This includes:

- Keeping this attribution section intact in any fork or derivative work
- Crediting **Mayank Basena** in your project's README or documentation
- Linking back to the original repository

**Failure to provide proper credit is a violation of the spirit of open source and may result in a DMCA takedown request.**

> *"No AI. No Shortcuts."* — Mayank Basena
