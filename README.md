# 🤖 AI-Powered Next-Generation SOC

**Academic project (in progress) — TEK-UP University, SSIR**

Design and implementation of a **Security Operations Center augmented with AI**:
network telemetry is collected, correlated and visualized, then an AI layer detects
anomalies and automatically triages alerts to reduce analyst noise.

> ⚠️ Educational project built in an isolated lab environment. No production traffic or confidential data.

## ✨ Features

- 📥 **Log collection & correlation** — Suricata (IDS/IPS) + Zeek (NSM) forward events to a central pipeline
- 📊 **Dashboards** — Splunk / Grafana dashboards for network visibility and alert monitoring
- 🧠 **AI triage** — anomaly detection + automated alert enrichment/triage (LLM-assisted summarization of incidents)
- 🧱 **Secure perimeter** — pfSense/OPNsense firewalling, LAN/DMZ segmentation, WireGuard VPN for remote access
- 🧪 **Attack simulation** — controlled test traffic (Kali Linux) to validate detection rules

## 🧰 Architecture

```
 [ LAN / DMZ hosts ] ──► [ Suricata + Zeek ] ──► [ Forwarder ] ──► [ Splunk / Grafana ]
                                                            └──► [ AI triage engine ] ──► [ Alert report ]
```

*(see `docs/architecture.md` and `screenshots/`)*

## 🛠️ Tech stack

| Layer | Tools |
|---|---|
| IDS / NSM | Suricata, Zeek |
| SIEM / Monitoring | Splunk (or Wazuh), Grafana |
| AI / Automation | Python, scikit-learn / local LLM |
| Perimeter | pfSense / OPNsense, WireGuard |
| Lab | VirtualBox / VMware, Kali Linux, Ubuntu Server |

## 🚀 Getting started

> Work in progress — the repo is filled in as the project advances.

1. Deploy the sensor VM (Suricata + Zeek) — see `docs/deployment.md`
2. Configure forwarding to Splunk
3. Run the AI triage engine — `python src/triage.py`

## 📁 Repository structure

```
ai-powered-soc/
├── docs/            # architecture, deployment, detection use-cases
├── screenshots/     # proof: dashboards, alerts, AI triage output
├── src/             # triage / automation scripts (Python)
├── rules/           # Suricata custom rules
└── README.md
```

## 🗺️ Roadmap

- [x] Network design & sensor deployment
- [x] Centralized log collection (Suricata, Zeek → Splunk)
- [x] Dashboards & alert monitoring (Grafana)
- [ ] AI anomaly detection baseline
- [ ] Automated alert triage (LLM-assisted)
- [ ] Detection use-cases library & report generation

## 👤 Author

**Abderrahmen Akkez** — engineering student, Information Systems & Network Security (SSIR)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/abderrahmen-akkez)
