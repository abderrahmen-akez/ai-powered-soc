# 🤖 AI-Powered Next-Generation SOC

**Academic project (in progress) — TEK-UP University, SSIR**

Design of an automated SOC pipeline:
**Wazuh** collects and correlates security events, a **Machine Learning scoring service**
(Random Forest + Isolation Forest, trained on the CIC-IDS2017 dataset) enriches alerts with a
risk score and a verdict, and **Shuffle** (SOAR) automates the response by creating cases in
**TheHive** and triggering actions on the **pfSense** firewall through its API.

> ⚠️ Educational project built in an isolated lab environment. No production traffic or confidential data.

## ✨ Features

- 📥 **SIEM / XDR** — Wazuh single-node deployment (manager, indexer, dashboard) with Docker Compose
- 🖥️ **Containerized agents** — 2 lightweight Wazuh agents (Ubuntu, 128 MB each) on the same Docker network
- 🧠 **ML scoring** — Random Forest (supervised, trained on CIC-IDS2017, ~2.5 M flows) + Isolation Forest (anomaly detection), served through a FastAPI endpoint (`/score` → `risk_score`, `anomaly`, `verdict`)
- 🔁 **SOAR automation** — Shuffle workflow (webhook trigger → automated response actions)
- 📋 **Case management** — alerts pushed to TheHive as investigation cases
- 🧱 **Active response** — pfSense firewall actions via its API
- 🧪 **Validation** — attack simulation tests through the scoring API

## 🧰 Architecture

```
 [ Wazuh agents x2 ] ──► [ Wazuh manager / indexer / dashboard ]
                                                    │
                                                    ▼
                                        [ ML scoring API (FastAPI) ]
                                          Random Forest + Isolation Forest
                                                    │
                                                    ▼
                                          [ Shuffle (SOAR) webhook ]
                                                    │
                              ┌─────────────────────┴──────────────┐
                              ▼                                    ▼
                       [ TheHive cases ]                  [ pfSense API actions ]
```

*(see `docs/architecture.md` and `screenshots/`)*

## 🛠️ Tech stack

| Layer | Tools |
|---|---|
| SIEM / XDR | Wazuh (manager, indexer, dashboard), Docker Compose |
| Machine Learning | scikit-learn (Random Forest, Isolation Forest), pandas, joblib — dataset: CIC-IDS2017 |
| Scoring API | FastAPI, uvicorn |
| SOAR | Shuffle |
| Case management | TheHive |
| Firewall | pfSense (REST API) |
| Lab | Docker on Windows, PowerShell |

## 🚀 Getting started

> Work in progress — the repo is filled in as the project advances.

1. Deploy the Wazuh single-node stack: `docker compose up -d` (manager, indexer, dashboard)
2. Start the 2 containerized agents on the same Docker network
3. Train the models on CIC-IDS2017 (`train_models.py`) → `models/*.joblib`
4. Build & run the scoring API: `docker compose -f docker-compose.scoring.yml up -d --build`
5. Test a scoring request: `curl -X POST http://localhost:8000/score -H "Content-Type: application/json" -d @test_attack.json`
6. Start Shuffle and validate the webhook workflow

## 📁 Repository structure

```
ai-powered-soc/
├── docs/            # architecture, deployment guide, validation checklist
├── screenshots/     # proof: Wazuh dashboard, scoring API output, Shuffle workflow, TheHive cases
├── models/          # trained models (random_forest.joblib, isolation_forest.joblib, columns.json)
├── scoring_api/     # FastAPI scoring service (Dockerfile, requirements.txt)
└── README.md
```

## 🗺️ Roadmap

- [x] Wazuh single-node deployment (Docker Compose) + 2 containerized agents
- [x] ML model training on CIC-IDS2017 (Random Forest + Isolation Forest)
- [x] FastAPI scoring service (risk score, anomaly flag, verdict)
- [x] Shuffle webhook workflow validated
- [ ] End-to-end integration: Wazuh alerts → scoring → TheHive cases + pfSense response
- [ ] Detection & validation report

## 👤 Author

**Abderrahmen Akkez** — engineering student, Information Systems & Network Security (SSIR)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/abderrahmen-akkez)
[![Gmail](https://img.shields.io/badge/Email-abderrahmen.akkez%40gmail.com-D14836?logo=gmail&logoColor=white)](mailto:abderrahmen.akkez@gmail.com)
