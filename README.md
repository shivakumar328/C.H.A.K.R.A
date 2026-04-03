# CHAKRA

[![Platform](https://img.shields.io/badge/platform-Windows-0078D6?logo=windows&logoColor=white)](https://www.microsoft.com/windows)
[![Backend](https://img.shields.io/badge/backend-FastAPI-009688?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![Frontend](https://img.shields.io/badge/frontend-React-61DAFB?logo=react&logoColor=black)](https://react.dev/)
[![LLM](https://img.shields.io/badge/LLM-Ollama-000000)](https://ollama.com/)
[![DB](https://img.shields.io/badge/database-PostgreSQL-4169E1?logo=postgresql&logoColor=white)](https://www.postgresql.org/)

CHAKRA is a cyber operations dashboard with a FastAPI backend, WebSocket streaming, a React frontend, recon and scan agents, defense monitoring, and a pluggable tool registry.

This project is intended for authorized security work only. Use it only on systems you own or have written permission to assess.

## Quick Navigation

- [One-Command Path](#one-command-path)
- [Full Interactive Setup](#full-interactive-setup)
- [Downloads](#downloads)
- [Project Structure](#project-structure)
- [Start Backend and Frontend](#start-backend-and-frontend)
- [Health and Verification](#health-and-verification)
- [Troubleshooting](#troubleshooting)

## One-Command Path

If tools are already installed, use this fast path:

```powershell
# from repo root
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install fastapi uvicorn psutil psycopg2-binary ollama
ollama pull phi3:mini
cd dashboard\frontend\chakra-ui
npm install
```

Then start services in separate terminals:

```powershell
# terminal 1 (repo root)
python run.py
```

```powershell
# terminal 2 (frontend)
cd dashboard\frontend\chakra-ui
npm start
```

## Downloads

### Required

- Git: https://git-scm.com/download/win
- Python 3.10+: https://www.python.org/downloads/windows/
- Node.js 18+: https://nodejs.org/en/download
- PostgreSQL: https://www.postgresql.org/download/windows/
- Ollama: https://ollama.com/download/windows
- VS Code: https://code.visualstudio.com/Download

### Optional Security Tools

- Nmap: https://nmap.org/download.html
- Gobuster: https://github.com/OJ/gobuster/releases
- SQLmap: https://sqlmap.org
- Nikto: https://github.com/sullo/nikto
- THC Hydra: https://github.com/vanhauser-thc/thc-hydra
- TheHarvester: https://github.com/laramies/theHarvester
- Whois: often easiest via WSL or package managers on Windows

## Full Interactive Setup

Use the checklist below and expand each step as needed.

- [ ] Step 1: Install Ollama and verify
- [ ] Step 2: Pull model
- [ ] Step 3: Install Python and Node.js
- [ ] Step 4: Install PostgreSQL and create DB
- [ ] Step 5: Clone repo and install dependencies
- [ ] Step 6: Configure settings
- [ ] Step 7: Start backend and frontend

<details>
<summary><strong>Step 1 - Install Ollama and verify</strong></summary>

Download: https://ollama.com/download/windows

```powershell
ollama --version
ollama serve
```

Keep this running if you are not using `python main.py`.

</details>

<details>
<summary><strong>Step 2 - Pull CHAKRA model</strong></summary>

Default model in `config/settings.json` is `phi3:mini`.

```powershell
ollama pull phi3:mini
ollama list
```

</details>

<details>
<summary><strong>Step 3 - Install Python and Node.js</strong></summary>

Python: https://www.python.org/downloads/windows/

```powershell
python --version
pip --version
```

Node.js: https://nodejs.org/en/download

```powershell
node --version
npm --version
```

</details>

<details>
<summary><strong>Step 4 - Install PostgreSQL and create database</strong></summary>

Download: https://www.postgresql.org/download/windows/

```powershell
psql --version
```

Create DB and user:

```sql
CREATE USER chakra_user WITH PASSWORD 'your_strong_password_here';
CREATE DATABASE chakra_db OWNER chakra_user;
GRANT ALL PRIVILEGES ON DATABASE chakra_db TO chakra_user;
```

</details>

<details>
<summary><strong>Step 5 - Clone repo and install dependencies</strong></summary>

```powershell
git clone <your-github-repository-url>
cd CHAKRA

python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install fastapi uvicorn psutil psycopg2-binary ollama
```

If PowerShell blocks activation:

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Frontend deps:

```powershell
cd dashboard\frontend\chakra-ui
npm install
```

</details>

<details>
<summary><strong>Step 6 - Configure project settings</strong></summary>

Edit `config/settings.json` and set:

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
<summary><strong>Step 7 - Start backend and frontend</strong></summary>

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

If backend is remote/custom:

```powershell
$env:REACT_APP_API_BASE="http://localhost:8000"
npm start
```

</details>

## Start Backend and Frontend

### Backend options

- `python run.py` -> starts FastAPI backend on port 8000
- `python main.py` -> starts Ollama serve and backend

### Frontend

```powershell
cd dashboard\frontend\chakra-ui
npm start
```

App URL: http://localhost:3000

## Health and Verification

Run:

```powershell
Invoke-RestMethod http://localhost:8000/health
```

Expect a JSON response containing `CHAKRA ONLINE`.

Quick checks:

- Frontend opens at http://localhost:3000
- Ollama is running and model exists
- PostgreSQL credentials in `config/settings.json` are valid
- Plugins page shows installed tools as ready

## Optional Plugin Tool Validation

```powershell
nmap --version
whois --version
gobuster --help
sqlmap --version
nikto -Version
hydra -h
```

If a tool is missing, install it and restart backend.

## Project Structure

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

- Chat not connecting: check `ollama serve` and model pull.
- DB errors: verify PostgreSQL service and settings credentials.
- Tools unavailable: install binaries and restart backend.
- Frontend API issues: verify `REACT_APP_API_BASE` and backend port 8000.

## License

MIT
