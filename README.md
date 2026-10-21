# SMART SERVICE FINDER 🚑🏥

> **Real-Time Ambulance-to-Hospital Facility Matching & Emergency Dispatch System**

Smart Service Finder enables frontline ambulances to identify a suitable nearby hospital before reaching the hospital. The system evaluates live hospital facilities, ICU bed vacancies, high-flow oxygen supplies, blood bank reserves, on-duty specialists, and road transit distance—transmitting an instant emergency alert to the receiving hospital's trauma desk so staff can prepare before the patient arrives.

---

## 🌟 Key Features

1. **Frontline Ambulance Rapid Triage:**
   - Log vitals: Pulse, Blood Pressure, SpO2 (Oxygen Saturation), Consciousness (GCS).
   - Triage levels: 🔴 Immediate (Red), 🟡 Urgent (Yellow), 🟢 Delayed (Green).
   - Specify critical resource requirements: ICU bed, high-flow oxygen, ventilator, emergency blood type, specialists (Cardiac, Neuro, Pediatric, Burn, Orthopedic).

2. **Automated Algorithmic Hospital Scoring:**
   - Evaluates nearby hospitals using the Haversine formula for road distance and estimated arrival time (ETA).
   - Generates a **Compatibility Match Score (0–100%)** based on real-time resource readiness.
   - Flags facility deficiencies (e.g., CT scanner down, no pediatric ICU) to prevent diverted arrivals.

3. **9-Step Emergency Coordination Workflow:**
   1. Ambulance enters/obtains patient requirements.
   2. System identifies nearby suitable hospitals.
   3. System compares hospital facilities.
   4. System recommends the most suitable hospital.
   5. Ambulance selects hospital.
   6. Hospital receives an emergency alert with audio/visual alarm.
   7. Hospital confirms availability & preps trauma bay.
   8. Ambulance receives confirmation with assigned bay & standby doctor.
   9. Hospital prepares for arrival & transit handoff is completed.

4. **Bi-Directional Real-Time WebSockets:**
   - Sub-second notification broadcast between moving ambulances and hospital emergency desks.
   - Built-in Web Audio API emergency chime for receiving ER terminals.

5. **Live Hospital ER Resource Manager:**
   - One-click adjustments for Available General Beds and ICU Beds.
   - Oxygen inventory status tracker (High, Moderate, Critical, Empty).
   - Blood bank availability toggle and hospital emergency status (Active, Busy, Critical Only, Divert).

6. **Dedicated Admin Governance Console:**
   - Real-time regional telemetry overview (bed and ICU occupancy rates, average ER response times).
   - Hospital verification queue (approve new hospitals with 1 click).
   - User account and role management.
   - Live Emergency Alert Audit Feed.

7. **SmartCare AI Assistant:**
   - Interactive floating assistant guiding users through platform navigation and emergency protocols.
   - Built-in clinical non-diagnostic guardrails.

---

## 🏗️ Tech Stack

- **Frontend:** React 19, Tailwind CSS v4, Lucide Icons, Web Audio API Synthesizer
- **Backend:** Node.js, Express.js, REST APIs, WebSockets (`ws`)
- **Database:** Supabase / PostgreSQL (Schema with 9 tables, indexes, constraints) + Zero-dependency JSON/Memory persistence fallback
- **Authentication:** Role-Based Access Control (`patient`, `ambulance`, `hospital`, `admin`), JWT tokens, bcrypt password hashing
- **Deployment:** Docker, Docker Compose, AWS-ready (App Runner, ECS Fargate, EC2, RDS)

---

## 👥 Roles & Portals

| Role | Portal / Dashboard | Capabilities |
| :--- | :--- | :--- |
| **Ambulance / EMS** | Paramedic Console | Rapid patient triage, live hospital matching, 1-click alert transmission, live bay status tracking. |
| **Hospital ER** | Trauma Desk Console | Incoming acoustic/visual emergency alerts, Accept/Divert requests, live bed and oxygen telemetry management. |
| **Chief Admin** | Dedicated Admin Portal | Network metrics, approve new hospitals, manage users, audit live emergency requests. |
| **Patient / Citizen** | Public Portal | Nearest hospital search, emergency hotlines (911/108), regional hospital readiness indicators. |

---

## ⚡ Quick Start Guide

### Prerequisites
- Node.js 18+ (tested on Node v22)
- npm 9+

### 1. Installation
Clone the repository and install all dependencies:
```bash
# Install root, server, and client dependencies
npm run install:all
```

### 2. Environment Configuration
Copy `.env.example` in `server/`:
```bash
cd server
cp .env.example .env
```
Default configuration:
```env
PORT=5000
NODE_ENV=development
JWT_SECRET=smart_service_finder_jwt_secure_key_2026

# Admin Credentials (Configurable via environment as requested)
ADMIN_EMAIL=YOUR_ADMIN_EMAIL@gmail.com
ADMIN_PASSWORD=Admin@SecurePass2026!

# Supabase / PostgreSQL connection (optional: app runs out-of-the-box without external DB)
DATABASE_URL=
USE_LOCAL_STORAGE=true
```

### 3. Start the Application
```bash
# Option A: Start production full-stack server (Builds React and serves on port 5000)
npm run build
npm start

# Option B: Run concurrent dev servers (Frontend at :5173, Backend at :5000)
# Terminal 1:
npm run server
# Terminal 2:
npm run client
```

Open your browser at:
- **Application URL:** [http://localhost:5000](http://localhost:5000) (or `http://localhost:5173` in Vite dev mode)
- **API Health Check:** [http://localhost:5000/api/health](http://localhost:5000/api/health)

---

## 🔑 Demo Login Accounts

Quick 1-click credentials buttons are built directly into the login screen:

| Role | Email | Password | Details |
| :--- | :--- | :--- | :--- |
| **Chief Admin** | `iswaryakakanaboyina@gmail.com` | `Admin@SecurePass2026!` | Admin: **kakanaboyina venkata siva lakshmi ishwarya** ([#/admin-login](http://localhost:5000/#/admin-login)) |
| **Ambulance Crew** | `paramedic.davis@ems.org` | `Password@123` | Call-Sign: `MEDIC-402` |
| **Hospital ER Staff**| `triage@metrocentral.hospital.org`| `Password@123` | Metro Central Trauma Center |
| **Patient User** | `citizen.alex@example.com` | `Password@123` | Public Citizen Portal |

---

## 🗄️ Database Tables (Supabase / PostgreSQL)

The complete SQL schema is located at `server/src/database/schema.sql`:

1. `users`: Credentials, role-based access, verification flags.
2. `hospitals`: Geo-coordinates, trauma ratings, emergency phone, available beds, ICU counts, oxygen stock.
3. `hospital_facilities`: Diagnostic and specialty services breakdown (Cath Lab, PICU, MRI, etc.).
4. `ambulance_requests`: Patient vitals, triage levels (Red/Yellow/Green), and critical resource requests.
5. `emergency_alerts`: High-priority pre-hospital alert beacons transmitted to receiving ER desks.
6. `hospital_responses`: Acceptance confirmation, assigned resuscitation bay, standby doctor, and response times.
7. `notifications`: Alert history and read status.
8. `admin_users`: Elevated permissions and department assignments.
9. `request_history`: Closed mission audit logs and patient handover durations.

---

## 🤖 SmartCare AI Assistant

Located as a floating assistant on every page:
- Answers queries on searching hospitals, triage color priority meanings, dispatch workflows, and facility capacity updating.
- **Safety Guarantee:** Programmed with clinical guardrails—strictly guides on platform usage and does not replace medical diagnosis.

---

## ☁️ Deployment

- **Docker:** Run `docker compose up --build`
- **AWS:** Detailed step-by-step instructions for AWS App Runner, ECS Fargate, ALB, EC2, and RDS are available in [`AWS_DEPLOYMENT.md`](./AWS_DEPLOYMENT.md).

---

## ⚖️ Clinical Disclaimer

Smart Service Finder is an emergency medical facility-matching and communication orchestration platform. It is **NOT** an automated diagnostic medical device and does not make clinical triage judgments without human verification.
