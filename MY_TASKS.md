# 🛰️ Member 1 — System Lead + ML Pipeline Owner

## Your Role
You are the **System Lead and ML Pipeline Owner**. You own the machine learning models, backend services, multi-agent orchestration, final integration, and the demo.

## Primary Deliverable
A fully working FastAPI backend where all ML models run correctly, all satellite data is pre-fetched and harmonized, and the multi-agent pipeline produces a real Action Plan from satellite data.

---

## 📁 Your Folder Structure
```
ML_Pipeline_and_System_Lead/
├── backend/                   ← YOUR PRIMARY WORKSPACE
│   ├── app/
│   │   ├── main.py            ← FastAPI app entry point
│   │   ├── config.py          ← Settings
│   │   ├── services/
│   │   │   ├── ml_service.py          ← ⭐ YOUR FILE — Isolation Forest, ARIMA, DBSCAN
│   │   │   ├── action_plan_service.py ← ⭐ YOUR FILE — Action Plan generation
│   │   │   └── ...
│   │   ├── ml/
│   │   │   ├── lstm_predictor.py      ← ⭐ YOUR FILE — PyTorch LSTM + crop score
│   │   │   └── ndvi_lst_regression.py ← ⭐ YOUR FILE — Green Gap regression
│   │   ├── agents/
│   │   │   └── orchestrator.py        ← ⭐ YOUR FILE — Multi-agent coordinator
│   │   └── utils/
│   │       └── geo_helpers.py         ← ⭐ YOUR FILE — IDW harmonization
│   ├── requirements.txt
│   └── .env.example
├── frontend/                  ← Full frontend for integration testing
├── data/                      ← Pre-fetched satellite JSON files
├── notebooks/                 ← Jupyter notebooks for analysis
├── scripts/                   ← Helper scripts
├── HOW_TO_RUN.md              ← Setup instructions
└── MY_TASKS.md                ← This file
```

---

## ⭐ Files You Own
| File | Responsibility |
|------|---------------|
| `backend/app/services/ml_service.py` | Isolation Forest, ARIMA, DBSCAN |
| `backend/app/ml/lstm_predictor.py` | PyTorch LSTM + crop score |
| `backend/app/ml/ndvi_lst_regression.py` | Green Gap regression |
| `backend/app/agents/orchestrator.py` | Multi-agent coordinator |
| `backend/app/utils/geo_helpers.py` | IDW harmonization (co-own with Member 3) |
| `README.md` | How to run the project locally |

---

## 📅 Day-by-Day Tasks

### Day 1 — Foundation
- [ ] Set up the FastAPI project (verify it runs with `uvicorn app.main:app --reload`)
- [ ] Pre-fetch all satellite JSON files for Ahmedabad using GEE scripts (work with Member 3)
- [ ] Run IDW harmonization and save harmonized files in `data/ahmedabad/`
- [ ] Write **stub** ML endpoints returning hardcoded JSON so Member 2 (Frontend) can start building
- [ ] Confirm Member 2 can hit `GET /api/v1/satellite/heatmap/LST` and get data

### Day 2 — Real ML
- [ ] Plug real Isolation Forest into `ml_service.py` — test with Ahmedabad LST data
- [ ] Plug real DBSCAN for hotspot clustering
- [ ] Add ARIMA forecasting for 30-day predictions
- [ ] Wire the multi-agent orchestrator — Data Agent → Analysis Agent → Action Plan Agent
- [ ] Test POST `/api/v1/action-plan/generate` returns a real report with real numbers

### Day 3 — Polish & Demo
- [ ] Fix all integration bugs reported by other members
- [ ] Pre-compute and cache ML results on startup (`ml_results_cache.json`)
- [ ] Update README with full setup instructions
- [ ] Rehearse the 5-step demo flow at least twice
- [ ] Prepare "number tracing" — be able to point to the satellite JSON behind each report number

---

## 🔌 How to Run the Backend
```bash
# 1. Go to the backend folder
cd backend

# 2. Create and activate a virtual environment
python -m venv venv
venv\Scripts\activate      # Windows

# 3. Install dependencies
pip install -r requirements.txt

# 4. Copy and fill in environment variables
copy .env.example .env
# Edit .env with your DB credentials and GEE auth

# 5. Start the server
uvicorn app.main:app --reload --port 8000
```

The API docs auto-generate at: http://localhost:8000/docs

---

## 🔌 How to Run the Frontend (for integration testing)
```bash
cd frontend
npm install
npm run dev
```
Frontend runs at http://localhost:5173

---

## 🤝 Integration Checkpoints
| When | What |
|------|------|
| End of Day 1 | Member 2 (Frontend) can render heatmap from your stub `/api/v1/satellite/heatmap/LST` |
| End of Day 2 | Full end-to-end: Dashboard → Map → Analytics → Action Plan all show real data |

---

## ⚠️ Critical Rules
- **NEVER call GEE at runtime during demo** — all satellite data must be pre-fetched JSON files
- Pre-compute ML results and cache them — demo must respond in under 1 second
- Every number in the Action Plan must trace back to a real satellite JSON value
- Keep `.env` out of Git — it contains secrets

---

## 🌐 API Endpoints You Must Deliver
| Method | Endpoint | Purpose |
|--------|----------|---------|
| GET | `/api/v1/ml/anomalies/{param}` | Isolation Forest anomaly results |
| GET | `/api/v1/ml/trends/{param}` | ARIMA 30-day forecast |
| GET | `/api/v1/ml/hotspots/{param}` | DBSCAN cluster results |
| POST | `/api/v1/action-plan/generate` | Full multi-agent pipeline → Action Plan |

---

## 🚀 GitHub Push Instructions
```bash
# From this folder (ML_Pipeline_and_System_Lead/)
git init
git add .
git commit -m "feat: ML pipeline and system lead — Member 1"
git remote add origin <YOUR_GITHUB_REPO_URL>
git push -u origin main
```

> ⚠️ Make sure `.gitignore` excludes: `venv/`, `__pycache__/`, `.env`, `node_modules/`
