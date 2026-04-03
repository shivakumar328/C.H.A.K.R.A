<h1 align="center">CHAKRA</h1>

![CHAKRA Banner](https://capsule-render.vercel.app/api?type=waving&height=180&section=header&text=CHAKRA%20v1.0&fontColor=00ff88&color=0:030b06,100:062518&fontAlign=50&fontAlignY=40)

![CHAKRA Fallback Banner](https://img.shields.io/badge/CHAKRA-v1.0-00ff88?style=for-the-badge&labelColor=071510&color=00ff88)

<p align="center">
  <a href="https://www.microsoft.com/windows"><img src="https://img.shields.io/badge/Windows-00ff88?style=for-the-badge&logo=windows&logoColor=black" alt="Windows" /></a>
  <a href="https://fastapi.tiangolo.com/"><img src="https://img.shields.io/badge/FastAPI-00ffa0?style=for-the-badge&logo=fastapi&logoColor=black" alt="FastAPI" /></a>
  <a href="https://react.dev/"><img src="https://img.shields.io/badge/React-39ff14?style=for-the-badge&logo=react&logoColor=black" alt="React" /></a>
  <a href="https://ollama.com/"><img src="https://img.shields.io/badge/Ollama-111111?style=for-the-badge" alt="Ollama" /></a>
  <a href="https://www.postgresql.org/"><img src="https://img.shields.io/badge/PostgreSQL-00ff88?style=for-the-badge&logo=postgresql&logoColor=black" alt="PostgreSQL" /></a>
</p>

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Share+Tech+Mono&size=20&duration=2200&pause=700&color=00FF88&center=true&vCenter=true&width=850&lines=Real-time+Cyber+Ops+Dashboard;FastAPI+%2B+WebSockets+%2B+React+%2B+Ollama;Recon+%7C+Scan+%7C+Defense+%7C+Plugin+Arsenal" alt="Typing Banner" />
</p>

> AUTHORIZED USE ONLY: Run CHAKRA only on systems you own or where you have explicit written permission.

## Command Deck

- [Live Quickstart](#live-quickstart)
- [Mission Paths](#mission-paths)
- [Downloads and Toolchain](#downloads-and-toolchain)
- [Interactive Setup Console](#interactive-setup-console)
- [Launch and Verify](#launch-and-verify)
- [Plugin Arsenal Check](#plugin-arsenal-check)
- [Project Topology](#project-topology)
- [Troubleshooting](#troubleshooting)

## Live Quickstart

<p>
  <img src="https://img.shields.io/badge/Estimated%20Time-5%20to%2010%20min-00ff88?style=flat-square" alt="time" />
  <img src="https://img.shields.io/badge/Mode-Operator%20Fast%20Path-0bffcc?style=flat-square" alt="mode" />
</p>

```powershell
# terminal 1 (repo root)
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install fastapi uvicorn psutil psycopg2-binary ollama
ollama pull phi3:mini
python run.py
```

```powershell
# terminal 2 (frontend)
cd dashboard\frontend\chakra-ui
npm install
npm start
```

Open http://localhost:3000

## Mission Paths

<table>
  <tr>
    <td width="33%" valign="top">
      <h3>Path A: Speed Run</h3>
      <p>Already familiar with Python, Node, and PostgreSQL.</p>
      <ul>
        <li>Use Live Quickstart</li>
        <li>Skip directly to Launch and Verify</li>
      </ul>
    </td>
    <td width="33%" valign="top">
      <h3>Path B: Full Install</h3>
      <p>Fresh machine setup from zero.</p>
      <ul>
        <li>Follow all checkpoints in order</li>
        <li>Recommended for first-time users</li>
      </ul>
    </td>
    <td width="33%" valign="top">
      <h3>Path C: Toolsmith</h3>
      <p>Install optional recon tools and validate plugins.</p>
      <ul>
        <li>Run Plugin Arsenal Check</li>
        <li>Tune tools in tools/tools.json</li>
      </ul>
    </td>
  </tr>
</table>

## Downloads and Toolchain

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
- Whois: easiest through WSL or package managers on Windows

## Interactive Setup Console

Mark your progress as you complete each mission.

- [ ] Install Ollama and verify command line
- [ ] Pull model used by CHAKRA
- [ ] Install Python, Node.js, PostgreSQL
- [ ] Create database and user
- [ ] Clone repo and install dependencies
- [ ] Configure settings
- [ ] Start backend and frontend

<details>
<summary><strong>Checkpoint 1: Install Ollama</strong></summary>

Download: https://ollama.com/download/windows

```powershell
ollama --version
ollama serve
```

If you run python main.py later, CHAKRA starts Ollama automatically.

</details>

<details>
<summary><strong>Checkpoint 2: Pull CHAKRA model</strong></summary>

Default model in config/settings.json is phi3:mini.

```powershell
ollama pull phi3:mini
ollama list
```

</details>

<details>
<summary><strong>Checkpoint 3: Install runtimes</strong></summary>

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
<summary><strong>Checkpoint 4: Create PostgreSQL database</strong></summary>

Run in psql as admin:

```sql
CREATE USER chakra_user WITH PASSWORD 'your_strong_password_here';
CREATE DATABASE chakra_db OWNER chakra_user;
GRANT ALL PRIVILEGES ON DATABASE chakra_db TO chakra_user;
```

</details>

<details>
<summary><strong>Checkpoint 5: Clone and install dependencies</strong></summary>

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

Frontend install:

```powershell
cd dashboard\frontend\chakra-ui
npm install
```

</details>

<details>
<summary><strong>Checkpoint 6: Configure settings</strong></summary>

Edit config/settings.json and set:

- db_host
- db_port
- db_name
- db_user
- db_password
- ollama_host
- primary_model
- fallback_model

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
<summary><strong>Checkpoint 7: Launch stack</strong></summary>

Backend only:

```powershell
python run.py
```

Backend plus Ollama:

```powershell
python main.py
```

Frontend in a new terminal:

```powershell
cd dashboard\frontend\chakra-ui
npm start
```

If backend host changes:

```powershell
$env:REACT_APP_API_BASE="http://localhost:8000"
npm start
```

</details>

<details>
<summary><strong>Advanced Terminal Blocks</strong></summary>

<details>
<summary>Health endpoint probe</summary>

```powershell
Invoke-RestMethod http://localhost:8000/health
```

</details>

<details>
<summary>Frontend production build</summary>

```powershell
cd dashboard\frontend\chakra-ui
npm run build
```

</details>

<details>
<summary>Backend service mode with reload</summary>

```powershell
$env:CHAKRA_RELOAD="1"
python run.py
```

</details>

</details>

## Launch and Verify

### Backend modes

- python run.py -> FastAPI backend on port 8000
- python main.py -> starts Ollama plus backend

### Frontend

- URL: http://localhost:3000
- Start command: npm start in dashboard/frontend/chakra-ui

### Verification checklist

- [ ] Backend responds at http://localhost:8000/health
- [ ] Frontend opens at http://localhost:3000
- [ ] Ollama model phi3:mini appears in ollama list
- [ ] Database tables are created on first backend start
- [ ] Plugin panel shows available tools

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

- main.py starts Ollama and backend
- run.py starts backend only
- dashboard/backend/main.py hosts API and WebSocket routes
- dashboard/frontend/chakra-ui contains React UI
- agents holds recon, scan, defense logic
- core holds LLM engine, memory, tool registry
- alerts contains toast and email alert modules
- config contains settings and scope
- data contains engagements, evidence, reports
- intelligence stores threat intel references
- tools/tools.json defines plugin registry

## Troubleshooting

<details>
<summary><strong>Chat does not stream</strong></summary>

- Ensure Ollama is running.
- Ensure model exists: ollama list.
- Confirm backend logs show no Ollama errors.

</details>

<details>
<summary><strong>Database connection fails</strong></summary>

- Check PostgreSQL service status.
- Verify config/settings.json credentials.
- Validate db_name and db_user in psql.

</details>

<details>
<summary><strong>Plugins show unavailable</strong></summary>

- Install missing binaries.
- Ensure tool commands resolve in PATH.
- Restart backend after installation.

</details>

<details>
<summary><strong>Frontend cannot reach backend</strong></summary>

- Set REACT_APP_API_BASE before npm start.
- Verify backend is listening on port 8000.
- Check browser console network errors.

</details>

## License

MIT
