# CHAKRA

```text
  _______ _    _          _  _______           
 / ____| |  | |   /\   | |/ /  __ \   /\    
| |    | |__| |  /  \  | ' /| |__) | /  \   
| |    |  __  | / /\ \ |  < |  _  / / /\ \  
| |____| |  | |/ ____ \| . \| | \ \/ ____ \ 
 \_____|_|  |_/_/    \_\_|\_\_|  \_/_/    \_\
```

[![Platform](https://img.shields.io/badge/platform-Windows-00ff88?style=for-the-badge&logo=windows&logoColor=black)](https://www.microsoft.com/windows)
[![Backend](https://img.shields.io/badge/backend-FastAPI-00c77a?style=for-the-badge&logo=fastapi&logoColor=black)](https://fastapi.tiangolo.com/)
[![Frontend](https://img.shields.io/badge/frontend-React-39ff14?style=for-the-badge&logo=react&logoColor=black)](https://react.dev/)
[![LLM](https://img.shields.io/badge/LLM-Ollama-0a0a0a?style=for-the-badge)](https://ollama.com/)
[![DB](https://img.shields.io/badge/database-PostgreSQL-00ff88?style=for-the-badge&logo=postgresql&logoColor=black)](https://www.postgresql.org/)

> Terminal-Grade Cyber Ops Dashboard: FastAPI + WebSockets + React + Ollama + PostgreSQL

CHAKRA is built for authorized security workflows only. Never run recon or scan activity against systems without explicit written permission.

## Neural Console

- [Quickstart in 90 Seconds](#quickstart-in-90-seconds)
- [Downloads and Toolchain](#downloads-and-toolchain)
- [Interactive Mission Setup](#interactive-mission-setup)
- [Launch Sequence](#launch-sequence)
- [Health and Integrity Checks](#health-and-integrity-checks)
- [Plugin Arsenal Check](#plugin-arsenal-check)
- [Project Topology](#project-topology)
- [Troubleshooting](#troubleshooting)

## Quickstart in 90 Seconds

```powershell
# terminal 1 - project root
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install fastapi uvicorn psutil psycopg2-binary ollama
ollama pull phi3:mini
python run.py
```

```powershell
# terminal 2 - frontend
cd dashboard\frontend\chakra-ui
npm install
npm start
```

Open http://localhost:3000

## Downloads and Toolchain

### Required

- Git: https://git-scm.com/download/win
- Python 3.10+: https://www.python.org/downloads/windows/
- Node.js 18+: https://nodejs.org/en/download
- PostgreSQL: https://www.postgresql.org/download/windows/
- Ollama: https://ollama.com/download/windows
- VS Code: https://code.visualstudio.com/Download

### Optional Recon and Security Tools

- Nmap: https://nmap.org/download.html
- Gobuster: https://github.com/OJ/gobuster/releases
- SQLmap: https://sqlmap.org
- Nikto: https://github.com/sullo/nikto
- THC Hydra: https://github.com/vanhauser-thc/thc-hydra
- TheHarvester: https://github.com/laramies/theHarvester
- Whois: easiest via WSL or a Windows package manager

## Interactive Mission Setup

Tick each checkpoint as you complete it.

- [ ] Install Ollama and verify CLI access
- [ ] Pull model used by CHAKRA
- [ ] Install Python + Node.js + PostgreSQL
- [ ] Create PostgreSQL database and user
- [ ] Clone repo and install backend/frontend dependencies
- [ ] Configure settings.json
- [ ] Start backend and frontend

<details>
<summary><strong>Checkpoint 1 - Install Ollama and verify</strong></summary>

Download: https://ollama.com/download/windows

```powershell
ollama --version
ollama serve
```

If you use `python main.py`, CHAKRA starts Ollama automatically.

</details>

<details>
<summary><strong>Checkpoint 2 - Pull model</strong></summary>

Default model in `config/settings.json` is `phi3:mini`.

```powershell
ollama pull phi3:mini
ollama list
```

</details>

<details>
<summary><strong>Checkpoint 3 - Install core runtimes</strong></summary>

Python:

```powershell
python --version
pip --version
```

Node.js:

```powershell
node --version
npm --version
```

PostgreSQL:

```powershell
psql --version
```

</details>

<details>
<summary><strong>Checkpoint 4 - Create database and user</strong></summary>

Run in psql as admin:

```sql
CREATE USER chakra_user WITH PASSWORD 'your_strong_password_here';
CREATE DATABASE chakra_db OWNER chakra_user;
GRANT ALL PRIVILEGES ON DATABASE chakra_db TO chakra_user;
```

</details>

<details>
<summary><strong>Checkpoint 5 - Clone and install dependencies</strong></summary>

```powershell
git clone <your-github-repository-url>
cd CHAKRA

python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install fastapi uvicorn psutil psycopg2-binary ollama
```

If activation is blocked:

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Frontend dependencies:

```powershell
cd dashboard\frontend\chakra-ui
npm install
```

</details>

<details>
<summary><strong>Checkpoint 6 - Configure settings.json</strong></summary>

Edit `config/settings.json`:

- `db_host`
- `db_port`
- `db_name`
- `db_user`
- `db_password`
- `ollama_host`
- `primary_model`
- `fallback_model`

Example:

```json
{
  "db_host": "localhost",
  "db_port": 5432,
  "db_name": "chakra_db",
  "db_user": "chakra_user",
  "db_password": "your_strong_password_here",
  "ollama_host": "http://localhost:11434",
  "primary_model": "phi3:mini",
  "fallback_model": "phi3:mini"
}
```

</details>

<details>
<summary><strong>Checkpoint 7 - Start CHAKRA stack</strong></summary>

Backend only:

```powershell
python run.py
```

Backend + Ollama together:

```powershell
python main.py
```

Frontend (new terminal):

```powershell
cd dashboard\frontend\chakra-ui
npm start
```

Override backend URL if needed:

```powershell
$env:REACT_APP_API_BASE="http://localhost:8000"
npm start
```

</details>

## Launch Sequence

```text
[01] Init virtual environment
[02] Install backend dependencies
[03] Pull Ollama model
[04] Start FastAPI backend
[05] Start React frontend
[06] Validate health endpoint
```

Backend modes:

- `python run.py` -> backend only on port 8000
- `python main.py` -> backend plus Ollama service

Frontend URL: http://localhost:3000

## Health and Integrity Checks

```powershell
Invoke-RestMethod http://localhost:8000/health
```

Expected signal: JSON containing `CHAKRA ONLINE`

Live checks:

- UI reachable at http://localhost:3000
- Ollama service active and model present
- PostgreSQL credentials match settings.json
- Database tables auto-created on first backend boot

## Plugin Arsenal Check

```powershell
nmap --version
whois --version
gobuster --help
sqlmap --version
nikto -Version
hydra -h
```

If a tool is missing, install it and restart backend.

## Project Topology

- `main.py` starts Ollama and backend
- `run.py` starts backend only
- `dashboard/backend/main.py` API and WebSocket routes
- `dashboard/frontend/chakra-ui/` React dashboard
- `agents/` recon, scan, defense logic
- `core/` LLM engine, DB helpers, tool registry
- `alerts/` toast and email alert integrations
- `config/` runtime settings and scope
- `data/` engagements, evidence, reports
- `intelligence/` reference intelligence
- `tools/tools.json` plugin/tool registry

## Troubleshooting

- Chat stuck/disconnected: verify `ollama serve` and model pull.
- DB connection errors: check PostgreSQL service and `config/settings.json`.
- Plugins show unavailable: install binaries and restart backend.
- Frontend cannot reach backend: set `REACT_APP_API_BASE` and verify port 8000.

## License

MIT
