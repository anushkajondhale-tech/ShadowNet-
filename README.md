# ShadowNet-
**ShadowNet** is an AI-powered adaptive cyber deception platform that uses fake SSH, Web, and API services to safely capture attacker behavior. It analyzes activities using AI, assigns risk levels, adapts the deception environment, reconstructs attack timelines, and generates forensic incident reports with structured cyber-law evidence support.
# 🛡️ ShadowNet

### AI-Powered Adaptive Cyber Deception, Threat Intelligence & Digital Forensics

ShadowNet is a controlled cybersecurity platform that creates **deceptive/fake services**, captures attacker interactions, analyses behaviour using AI, adapts the deception environment, and generates **threat intelligence and forensic incident reports**.

> **Core principle:** Deceive → Capture → Analyse → Adapt → Investigate → Report

All attack demonstrations must be performed against **locally controlled or explicitly authorized systems only**.

---

# 1. Vision

Traditional security monitoring primarily focuses on detecting suspicious activity.

ShadowNet adds an additional layer:

```text
                    ┌──────────────────────┐
                    │   Controlled Attacker │
                    │      Simulator        │
                    └──────────┬───────────┘
                               │
                               ▼
                 ┌─────────────────────────┐
                 │   SHADOWNET DECEPTION   │
                 │                         │
                 │ Fake SSH │ Fake Web     │
                 │ Fake API │ Fake Data    │
                 └──────────┬──────────────┘
                            │
                            ▼
                 ┌─────────────────────────┐
                 │    EVENT COLLECTION     │
                 └──────────┬──────────────┘
                            │
                            ▼
                 ┌─────────────────────────┐
                 │   DETECTION ENGINE      │
                 │ Rules + Behaviour       │
                 └──────────┬──────────────┘
                            │
                            ▼
                 ┌─────────────────────────┐
                 │      AI ANALYSIS        │
                 └──────────┬──────────────┘
                            │
               ┌────────────┴────────────┐
               ▼                         ▼
       ┌───────────────┐         ┌────────────────┐
       │ Risk Scoring  │         │ Adaptive       │
       │ + Classification│       │ Deception      │
       └───────┬───────┘         └───────┬────────┘
               │                         │
               └────────────┬────────────┘
                            ▼
                 ┌─────────────────────────┐
                 │   FORENSIC ENGINE       │
                 └──────────┬──────────────┘
                            ▼
                 ┌─────────────────────────┐
                 │ AI INCIDENT REPORT      │
                 └──────────┬──────────────┘
                            ▼
                 ┌─────────────────────────┐
                 │     REACT DASHBOARD     │
                 └─────────────────────────┘
```

---

# 2. Main Features

## 2.1 Adaptive Cyber Deception

ShadowNet provides controlled fake services that appear to be legitimate infrastructure.

### Initial services

* SSH Honeypot
* Web Honeypot
* API Honeypot

The services do **not** provide access to real infrastructure.

They only simulate services and record interactions.

---

## 2.2 SSH Honeypot

Captures events such as:

* Connection attempts
* Failed authentication attempts
* Repeated login behaviour
* Commands entered into the simulated environment
* Session duration
* Source IP
* Timestamp

Example event:

```json
{
  "service": "SSH",
  "event_type": "authentication_attempt",
  "source_ip": "192.168.1.50",
  "metadata": {
    "username": "admin"
  }
}
```

---

# 3. Web Honeypot

A fake web application designed to attract suspicious requests.

Captures:

* Requested paths
* HTTP methods
* Query parameters
* User agent
* Source IP
* Request frequency
* Suspicious patterns

Example:

```text
GET /admin
GET /login
GET /api/users
GET /backup
```

These become security events for analysis.

---

# 4. API Honeypot

A simulated modern API environment.

Example endpoints:

```text
/api/login
/api/users
/api/admin
/api/config
/api/data
```

The API does not expose real sensitive information.

It records suspicious interaction patterns.

---

# 5. Event Collection System

Every interaction generates a normalized security event.

```text
Fake Service
     ↓
Event Collector
     ↓
Validation
     ↓
Normalization
     ↓
Database
     ↓
Detection Engine
```

Normalized event structure:

```json
{
  "event_id": "uuid",
  "timestamp": "ISO-8601",
  "source_ip": "192.168.1.50",
  "source_port": 54321,
  "destination_port": 22,
  "service": "ssh",
  "event_type": "login_attempt",
  "action": "failed_login",
  "severity": "medium",
  "metadata": {}
}
```

---

# 6. Detection Engine

Detection should use a combination of:

### Rule-based detection

Examples:

```text
Multiple failed SSH logins
        ↓
Possible Brute Force

Rapid requests to many ports
        ↓
Possible Reconnaissance

Large number of suspicious URLs
        ↓
Possible Web Scanning
```

### Behaviour analysis

The system also looks at:

* Frequency
* Sequence
* Repetition
* Service switching
* Session behaviour
* Time intervals

This produces a behaviour profile.

---

# 7. AI Analysis Engine

The AI layer should **not be responsible for everything**.

The architecture should be:

```text
Raw Events
    ↓
Deterministic Detection
    ↓
Behaviour Aggregation
    ↓
AI Analysis
    ↓
Explanation + Classification
```

The AI can generate:

* Attack classification
* Behaviour summary
* Risk explanation
* Attack narrative
* Recommended investigation actions

Example:

```text
Threat:
Possible Brute Force

Risk:
HIGH

Reason:
Repeated authentication attempts were observed
from the same source within a short period.

Evidence:
37 failed authentication attempts
over 90 seconds.
```

---

# 8. Risk Scoring

The risk engine combines deterministic signals.

Example conceptual model:

```text
Risk =
    Frequency
  + Severity
  + Behaviour Pattern
  + Service Sensitivity
  + Attack Progression
```

Output:

```text
LOW
MEDIUM
HIGH
CRITICAL
```

The exact scoring weights should be configurable.

Example:

```json
{
  "risk_score": 87,
  "risk_level": "HIGH"
}
```

---

# 9. Adaptive Deception

This is one of ShadowNet's main differentiators.

Instead of having static honeypots:

```text
Attacker
   ↓
Fake SSH
   ↓
Done
```

ShadowNet can react to behaviour:

```text
Attacker scans
      ↓
Recon detected
      ↓
Attacker targets SSH
      ↓
SSH deception activated
      ↓
Attacker probes Web service
      ↓
Web deception activated
      ↓
Behaviour profile updated
```

The adaptive system can change the **fake environment**, not the real system.

Examples:

* Expose another simulated endpoint
* Change fake service responses
* Create a simulated fake resource
* Increase monitoring for a session
* Generate additional deception events

All adaptive behaviour must remain inside the isolated ShadowNet environment.

---

# 10. Attacker Behaviour Profile

For every suspicious session, maintain a profile.

Example:

```json
{
  "session_id": "abc123",
  "source_ip": "192.168.1.50",
  "services_touched": [
    "ssh",
    "web",
    "api"
  ],
  "event_count": 47,
  "first_seen": "...",
  "last_seen": "...",
  "attack_types": [
    "reconnaissance",
    "brute_force"
  ],
  "risk_score": 87
}
```

---

# 11. Digital Forensics Engine

Every event should be usable as evidence for investigation.

The forensic engine reconstructs:

```text
FIRST ACTIVITY
      ↓
RECONNAISSANCE
      ↓
SERVICE INTERACTION
      ↓
AUTHENTICATION ATTEMPTS
      ↓
SUSPICIOUS ACTION
      ↓
SESSION END
```

The dashboard should provide an attack timeline.

Example:

```text
10:31:04  Port scan detected
10:31:09  SSH connection
10:31:12  Failed login
10:31:14  Failed login
10:31:18  Web service accessed
10:31:27  Suspicious API request
10:31:30  Session flagged HIGH
```

---

# 12. AI Forensic Report

ShadowNet generates a structured incident report.

Example:

```text
INCIDENT REPORT

Incident ID:
INC-2026-001

Risk:
HIGH

Source:
192.168.1.50

Affected Deception Services:
SSH, Web

Timeline:
10:31 - Reconnaissance
10:31 - SSH interaction
10:31 - Authentication attempts
10:31 - Web probing

Detected Behaviour:
Brute Force + Service Reconnaissance

Evidence:
47 recorded events

AI Summary:
The observed session demonstrates repeated authentication
attempts combined with service probing behaviour.

Recommended Investigation:
Review the associated event timeline and session logs.
```

---

# 13. Cyber-Law Support Layer

ShadowNet does **not** make legal conclusions.

Instead it organizes technical evidence into a structured incident report.

It can provide:

* Incident category
* Evidence summary
* Event timeline
* Source/session information
* Captured logs
* Investigation notes
* Exportable report

This connects the project to the **Cyber Law** portion of the track without pretending that AI itself determines legal liability.

---

# 14. Frontend

## Technology

* React
* Vite
* Tailwind CSS
* Recharts
* Axios
* WebSocket client

---

# 15. Dashboard

Main dashboard:

```text
┌──────────────────────────────────────────────┐
│ SHADOWNET                    SYSTEM ACTIVE   │
├──────────┬──────────┬──────────┬─────────────┤
│ Threats  │ Events   │ Sessions │ Services    │
│   12     │   348    │    4     │   3/3       │
├──────────┴──────────┴──────────┴─────────────┤
│               LIVE THREAT FEED               │
├──────────────────────────────────────────────┤
│ 🔴 HIGH     Brute Force      192.168.1.50   │
│ 🟠 MEDIUM   Port Scan        192.168.1.72   │
│ 🔴 HIGH     API Anomaly      192.168.1.91   │
├──────────────────────────────────────────────┤
│                 ATTACK TIMELINE              │
└──────────────────────────────────────────────┘
```

---

# 16. Frontend Pages

```text
/dashboard
/threats
/sessions
/events
/services
/forensics
/reports
/settings
```

### Dashboard

Overview of the entire system.

### Threats

List of detected threats.

### Sessions

Attacker/session investigation.

### Events

Raw security events.

### Services

Status of:

* SSH
* Web
* API

### Forensics

Timeline and evidence.

### Reports

Generated incident reports.

---

# 17. Backend

## Technology

* Python 3.11+
* FastAPI
* Pydantic
* SQLAlchemy
* SQLite
* Uvicorn
* WebSockets
* Docker

Optional production upgrade:

* PostgreSQL
* Redis
* Celery

The hackathon prototype should remain lightweight and use SQLite unless scale requires otherwise.

---

# 18. Backend Architecture

```text
FastAPI
│
├── API Layer
│   ├── Events
│   ├── Threats
│   ├── Sessions
│   ├── Services
│   ├── Forensics
│   └── Reports
│
├── Core
│   ├── Detection Engine
│   ├── Risk Engine
│   ├── AI Analyzer
│   ├── Adaptive Deception
│   └── Forensics Engine
│
├── Data Layer
│   ├── SQLAlchemy
│   └── SQLite
│
└── Integration Layer
    ├── Honeypots
    ├── AI Provider
    └── WebSocket
```

---

# 19. API Design

## Events

```http
GET /api/events
GET /api/events/{event_id}
POST /api/events
```

## Threats

```http
GET /api/threats
GET /api/threats/{threat_id}
PATCH /api/threats/{threat_id}
```

## Sessions

```http
GET /api/sessions
GET /api/sessions/{session_id}
```

## Services

```http
GET /api/services
GET /api/services/{service_name}
```

## Forensics

```http
GET /api/forensics/{session_id}/timeline
GET /api/forensics/{session_id}/evidence
```

## Reports

```http
POST /api/reports/{session_id}/generate
GET /api/reports
GET /api/reports/{report_id}
```

## Statistics

```http
GET /api/stats
```

---

# 20. Real-Time Communication

Use WebSockets for the dashboard.

```text
Honeypot
   ↓
Event
   ↓
FastAPI
   ↓
Detection
   ↓
WebSocket
   ↓
React
```

Example:

```text
New HIGH threat detected
        ↓
FastAPI broadcasts event
        ↓
React receives event
        ↓
Dashboard updates immediately
```

---

# 21. Database

SQLite for the prototype.

## Tables

### events

```text
events
├── id
├── timestamp
├── source_ip
├── source_port
├── destination_port
├── service
├── event_type
├── action
├── severity
├── session_id
└── metadata
```

### sessions

```text
sessions
├── id
├── source_ip
├── started_at
├── ended_at
├── risk_score
├── risk_level
└── status
```

### threats

```text
threats
├── id
├── session_id
├── attack_type
├── risk_score
├── risk_level
├── confidence
├── explanation
├── detected_at
└── status
```

### services

```text
services
├── id
├── name
├── type
├── port
├── status
└── configuration
```

### reports

```text
reports
├── id
├── session_id
├── title
├── summary
├── report_data
├── generated_at
└── format
```

---

# 22. SQLAlchemy Models

Recommended relationships:

```text
Session
   │
   ├── Events
   │
   ├── Threats
   │
   └── Reports
```

Conceptually:

```python
Session
 ├── events: List[Event]
 ├── threats: List[Threat]
 └── reports: List[Report]
```

---

# 23. Project Structure

```text
ShadowNet/
│
├── README.md
├── LICENSE
├── .gitignore
├── docker-compose.yml
├── .env.example
│
├── backend/
│   ├── requirements.txt
│   ├── Dockerfile
│   │
│   ├── app/
│   │   ├── main.py
│   │   │
│   │   ├── core/
│   │   │   ├── config.py
│   │   │   ├── security.py
│   │   │   └── logging.py
│   │   │
│   │   ├── db/
│   │   │   ├── database.py
│   │   │   └── session.py
│   │   │
│   │   ├── models/
│   │   │   ├── event.py
│   │   │   ├── session.py
│   │   │   ├── threat.py
│   │   │   ├── service.py
│   │   │   └── report.py
│   │   │
│   │   ├── schemas/
│   │   │   ├── event.py
│   │   │   ├── threat.py
│   │   │   ├── session.py
│   │   │   └── report.py
│   │   │
│   │   ├── api/
│   │   │   ├── events.py
│   │   │   ├── threats.py
│   │   │   ├── sessions.py
│   │   │   ├── services.py
│   │   │   ├── forensics.py
│   │   │   ├── reports.py
│   │   │   └── stats.py
│   │   │
│   │   ├── services/
│   │   │   ├── collector.py
│   │   │   ├── detection.py
│   │   │   ├── risk_engine.py
│   │   │   ├── ai_analyzer.py
│   │   │   ├── adaptive_deception.py
│   │   │   ├── forensics.py
│   │   │   └── report_generator.py
│   │   │
│   │   └── honeypots/
│   │       ├── ssh/
│   │       ├── web/
│   │       └── api/
│   │
│   └── tests/
│       ├── test_events.py
│       ├── test_detection.py
│       ├── test_risk.py
│       └── test_reports.py
│
├── frontend/
│   ├── package.json
│   ├── Dockerfile
│   │
│   └── src/
│       ├── main.jsx
│       ├── App.jsx
│       │
│       ├── components/
│       │   ├── ThreatCard.jsx
│       │   ├── EventTable.jsx
│       │   ├── AttackTimeline.jsx
│       │   ├── RiskBadge.jsx
│       │   ├── ServiceStatus.jsx
│       │   └── ThreatChart.jsx
│       │
│       ├── pages/
│       │   ├── Dashboard.jsx
│       │   ├── Threats.jsx
│       │   ├── Sessions.jsx
│       │   ├── Events.jsx
│       │   ├── Services.jsx
│       │   ├── Forensics.jsx
│       │   └── Reports.jsx
│       │
│       ├── services/
│       │   ├── api.js
│       │   └── websocket.js
│       │
│       └── hooks/
│           └── useThreatStream.js
│
├── simulator/
│   ├── README.md
│   ├── reconnaissance.py
│   ├── ssh_simulator.py
│   ├── web_simulator.py
│   └── api_simulator.py
│
├── docs/
│   ├── architecture.md
│   ├── api.md
│   └── demo.md
│
└── docker/
    ├── ssh-honeypot/
    ├── web-honeypot/
    └── api-honeypot/
```

---

# 24. Docker Architecture

Recommended local setup:

```text
Docker Compose
│
├── backend
│   └── FastAPI
│
├── frontend
│   └── React
│
├── ssh-honeypot
│
├── web-honeypot
│
└── api-honeypot
```

The honeypot containers should be isolated from real host resources.

---

# 25. AI Architecture

The AI system should have clear boundaries.

```text
Security Events
      ↓
Feature Extraction
      ↓
Detection Rules
      ↓
Behaviour Summary
      ↓
LLM / ML Analyzer
      ↓
Structured AI Result
```

The AI output should follow a structured schema:

```json
{
  "attack_type": "brute_force",
  "confidence": 0.91,
  "risk_level": "high",
  "reason": "Repeated authentication attempts...",
  "summary": "..."
}
```

The backend should validate this response before storing it.

---

# 26. AI Provider Abstraction

Do not hard-code the application to one AI provider.

Use:

```text
AIAnalyzer
    │
    ├── OpenAIProvider
    ├── AnthropicProvider
    ├── GeminiProvider
    └── LocalProvider
```

This allows the project to work with available/free or locally hosted models.

API keys must be stored in environment variables.

Never commit API keys to GitHub.

---

# 27. Configuration

Use `.env`:

```env
APP_ENV=development

DATABASE_URL=sqlite:///./data/shadownet.db

AI_PROVIDER=...
AI_API_KEY=...

BACKEND_URL=http://localhost:8000
FRONTEND_URL=http://localhost:5173
```

Provide `.env.example` without real credentials.

---

# 28. Security Requirements

ShadowNet itself must be designed securely.

### Isolation

Honeypots should run in containers.

### No real credentials

Never use real:

* passwords
* API keys
* cloud credentials
* database credentials

### No real sensitive data

Only synthetic/fake data should be exposed.

### No unauthorized targets

The simulator must target only ShadowNet's controlled services.

### Network restrictions

The deception environment should not provide a path into the host's real systems.

---

# 29. Demo Attack Simulator

The simulator creates safe, predefined test scenarios.

Example:

```text
Scenario 1:
Reconnaissance

Scenario 2:
Repeated SSH authentication attempts

Scenario 3:
Web endpoint probing

Scenario 4:
Suspicious API activity

Scenario 5:
Multi-service attack progression
```

The simulator exists exclusively to demonstrate ShadowNet against infrastructure owned/controlled by the team.

---

# 30. End-to-End Demo

The ideal hackathon demonstration:

```text
STEP 1
Start ShadowNet
        ↓
STEP 2
Start attacker simulator
        ↓
STEP 3
Simulator interacts with fake SSH
        ↓
STEP 4
ShadowNet captures events
        ↓
STEP 5
Detection engine identifies behaviour
        ↓
STEP 6
AI analyses the session
        ↓
STEP 7
Risk becomes HIGH
        ↓
STEP 8
Adaptive deception responds
        ↓
STEP 9
Forensic timeline is created
        ↓
STEP 10
AI generates incident report
        ↓
STEP 11
React dashboard shows everything LIVE
```

---

# 31. Recommended Development Order

Do NOT build everything simultaneously.

### Phase 1 — Backend foundation

```text
FastAPI
SQLite
SQLAlchemy
Event model
REST API
```

### Phase 2 — Fake services

```text
SSH
Web
API
```

### Phase 3 — Event pipeline

```text
Honeypots
   ↓
Collector
   ↓
Database
```

### Phase 4 — Detection

```text
Rules
Behaviour aggregation
Risk scoring
```

### Phase 5 — AI

```text
Event summary
AI classification
AI explanation
```

### Phase 6 — Frontend

```text
Dashboard
Threats
Sessions
Events
Timeline
```

### Phase 7 — Adaptive deception

Add controlled environment changes based on detected behaviour.

### Phase 8 — Forensics

Add timeline and evidence views.

### Phase 9 — Reports

Generate structured incident reports.

### Phase 10 — Final integration

Run the complete demo from attacker simulator → report.

---

# 32. MVP vs Advanced Features

## MVP — Must Have

* SSH honeypot
* Web honeypot
* API honeypot
* Event collection
* SQLite
* Detection rules
* Risk scoring
* AI classification/explanation
* React dashboard
* Attack timeline

## Advanced

* Adaptive deception
* Session fingerprinting
* Behaviour clustering
* AI forensic reports
* Cyber-incident report export
* WebSocket live updates
* PDF/JSON evidence export
* Multi-session correlation

Build the MVP first. Only add advanced features after the complete MVP works.

---

# 33. Suggested Technology Stack

| Layer           | Technology                 |
| --------------- | -------------------------- |
| Frontend        | React + Vite               |
| Styling         | Tailwind CSS               |
| Charts          | Recharts                   |
| Backend         | Python + FastAPI           |
| ORM             | SQLAlchemy                 |
| Validation      | Pydantic                   |
| Database        | SQLite                     |
| Real-time       | WebSockets                 |
| Containers      | Docker                     |
| AI              | Provider abstraction + LLM |
| Testing         | Pytest                     |
| API testing     | HTTPX                      |
| Version control | Git + GitHub               |
| Development     | Claude Code                |

---

# 34. Definition of Done

ShadowNet is considered functional when:

* [ ] FastAPI starts successfully
* [ ] React dashboard starts successfully
* [ ] SQLite database is created
* [ ] SSH honeypot records events
* [ ] Web honeypot records events
* [ ] API honeypot records events
* [ ] Events appear in the database
* [ ] Detection engine identifies test scenarios
* [ ] Risk score is generated
* [ ] AI produces structured analysis
* [ ] Threat appears on dashboard
* [ ] Session timeline is generated
* [ ] Adaptive deception can be demonstrated
* [ ] Forensic report can be generated
* [ ] Complete demo works from start to finish

---

# 35. Development Philosophy

ShadowNet should prioritize:

1. **Working prototype over excessive features**
2. **Deterministic security logic before AI**
3. **Isolation and safety**
4. **Simple architecture**
5. **Observable data flow**
6. **Easy debugging**
7. **Clear AI contribution**
8. **Strong live demonstration**

The final product should make the following story immediately visible:

> **An attacker enters our controlled deception environment. ShadowNet observes their behaviour, intelligently analyses it, adapts the deception, reconstructs the incident, and generates actionable threat intelligence and a forensic report.**

---

# 36. Quick Start

### Backend

```bash
cd backend

python -m venv .venv

# Linux/macOS
source .venv/bin/activate

# Windows
.venv\Scripts\activate

pip install -r requirements.txt

uvicorn app.main:app --reload
```

Backend:

```text
http://localhost:8000
```

API documentation:

```text
http://localhost:8000/docs
```

### Frontend

```bash
cd frontend

npm install
npm run dev
```

Frontend:

```text
http://localhost:5173
```

---

# 37. Final Architecture

```text
                         SHADOWNET
                            │
          ┌─────────────────┴─────────────────┐
          │                                   │
     DECEPTION LAYER                     DASHBOARD
          │                                   │
    ┌─────┼─────┐                       React + Vite
    │     │     │                             │
   SSH   WEB   API                            │
    │     │     │                             │
    └─────┼─────┘                             │
          ▼                                   │
     EVENT COLLECTOR                          │
          │                                   │
          ▼                                   │
     NORMALIZATION                            │
          │                                   │
          ▼                                   │
       SQLite                                  │
          │                                   │
          ▼                                   │
   DETECTION ENGINE                            │
          │                                   │
     ┌────┴────┐                              │
     ▼         ▼                              │
 RULES    BEHAVIOUR ANALYSIS                  │
     │         │                              │
     └────┬────┘                              │
          ▼                                   │
      AI ANALYZER ────────────────► WebSocket │
          │                                   │
     ┌────┴────────────┐                      │
     ▼                 ▼                      │
RISK ENGINE     ADAPTIVE DECEPTION             │
     │                 │                       │
     └────────┬────────┘                       │
              ▼                                │
       FORENSIC ENGINE                         │
              │                                │
              ▼                                │
       AI INCIDENT REPORT ─────────────────────┘
```

## ShadowNet

**Deception + Detection + AI + Adaptation + Forensics + Cyber-Law Support**

A controlled cybersecurity research and demonstration platform — **not a tool for attacking or accessing unauthorized systems**.

