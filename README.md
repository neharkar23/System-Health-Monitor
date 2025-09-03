System Health Monitoring 

A full-stack solution to monitor, ingest, and visualize machine health data.
Built with FastAPI, SQLite, and a lightweight utility agent, with a simple dashboard for visualization.

Features:

1. Backend (FastAPI + SQLite)

    REST API for machine health ingestion and retrieval
    
    Auto-generated interactive API docs at /docs
    
    CSV export endpoint for reporting

2. Utility Agent (Python)

    Cross-platform (Windows/macOS/Linux)
    
    Collects system info (disk encryption, updates, antivirus, sleep settings)
    
    Authenticated POST to backend with deduplication
    
    Configurable interval for continuous monitoring

3. Frontend (HTML/JS)

    Lightweight dashboard to view all registered machines
    
    Fetches data dynamically from backend API



Architecture

[Utility Agent] → [FastAPI Backend] → [SQLite Database] → [Frontend Dashboard]


Utility Agent: Collects machine health data

Backend: FastAPI server to ingest, validate, and serve data

Database: SQLite for persistence

Frontend: Displays machine status and allows export


Project Structure

Siddhi-Solsphere-AI/
backend/ FastAPI + SQLite server
utility/ Machine health collection agent
frontend/ Simple dashboard (HTML/JS)
docker-compose.yml
README.md




Quick Start

1. Backend Setup

    cd backend
    python -m venv .venv
    .venv\Scripts\activate (Windows)
    source .venv/bin/activate (Linux/Mac)
    
    pip install -r requirements.txt
    uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload

    Backend will be available at:
    API Docs → http://localhost:8000/docs
    
    Machines List → http://localhost:8000/api/v1/machines

2. Frontend Setup

    cd frontend
    npm install
    npm run dev
    
    Open http://localhost:5173

3. Utility Agent

    cd utility
    python -m venv .venv
    .venv\Scripts\activate (Windows)
    source .venv/bin/activate (Linux/Mac)
    
    pip install -r requirements.txt
    
    One-time ingestion
    python -m utility.main --once --api http://localhost:8000
     --token devtoken
    
    Continuous ingestion every 15–60 min
    python -m utility.main --daemon --api http://localhost:8000
     --token devtoken --min 15 --max 60


API Endpoints

    Ingest Machine Data → POST /api/v1/ingest
    Agent sends system health info
    
    Fetch Machines → GET /api/v1/machines
    Returns list of all registered machines in JSON
    
    Export CSV → GET /api/v1/machines.csv
    Returns machine health data in CSV format
    
    Interactive API docs are available at: http://localhost:8000/docs



Example Workflow

    Start backend → uvicorn app.main:app --reload
    
    Start frontend → npm run dev
    
    Run utility → python -m utility.main --once --api http://localhost:8000
     --token devtoken
    
    See new machine appear in dashboard
    
    Export data anytime → http://localhost:8000/api/v1/machines.csv



Tech Stack

    Backend: FastAPI, SQLAlchemy, SQLite
    Utility Agent: Python (cross-platform, system libraries)
    Frontend: HTML, Vanilla JS (lightweight)
    Infrastructure: Docker Compose for containerized setup
