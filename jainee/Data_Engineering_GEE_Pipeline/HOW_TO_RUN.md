# How to Run the Satellite Project

## Prerequisites
- Python 3.x installed
- Node.js installed

---

## Step 1 — Start the Backend (FastAPI)

Open a terminal and run:

```bash
cd backend
venv\Scripts\uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

Backend will be available at: **http://localhost:8000**  
API docs (Swagger UI): **http://localhost:8000/docs**

---

## Step 2 — Start the Frontend (React + Vite)

Open a **new terminal** and run:

```bash
cd frontend
cmd /c "npm run dev"
```

Frontend will be available at: **http://localhost:5173** (or next free port like 5175)

---

## URLs Summary

| Service     | URL                              |
|-------------|----------------------------------|
| Frontend    | http://localhost:5173            |
| Backend API | http://localhost:8000            |
| API Docs    | http://localhost:8000/docs       |
| Health Check| http://localhost:8000/api/v1/health |

---

## Notes

- **No database needed** — the app uses pre-fetched JSON data in the `data/` folder.
- The `backend/venv/` and `frontend/node_modules/` folders are already set up — no need to reinstall unless deleted.
- Both terminals must stay open while using the app.

---

## If Dependencies Are Missing (first-time / reinstall)

```bash
# Backend
cd backend
python -m venv venv
venv\Scripts\pip install -r requirements.txt

# Frontend
cd frontend
cmd /c "npm install"
```
