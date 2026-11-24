# Attend AI – AI-Powered Attendance Verification System

> **“Verify. Recognize. Record.”**  
> An intelligent, deep-learning powered biometric attendance verification and management platform with anti-proxy liveness detection, real-time analytics dashboards, and institutional reporting.

---

## 📌 1. Project Overview

Manual roll-call and paper-based attendance systems are time-consuming, prone to human error, and vulnerable to proxy attendance where students mark presence on behalf of absent peers. Educational faculties routinely spend 10–15% of classroom time administering paper records.

**AttendAI** automates attendance by capturing the student's live face via camera, computing normalized 128-dimensional invariant biometric feature vectors, and matching them against registered embeddings using high-speed cosine similarity. With integrated multi-stage Anti-Proxy Liveness Verification (detecting eye blinks and optical flow motion), AttendAI records attendance in milliseconds with precise timestamps and confidence telemetry.

---

## ✨ 2. Key Features

- **AI Facial Recognition Engine**: 128-dimensional facial representation embeddings with cosine distance calculation.
- **Anti-Proxy Liveness Shield**: Multi-stage verification (`Face Match → Liveness Check → Attendance Verified`) to prevent spoofing via printed photos or phone screens.
- **Multi-Angle Biometric Registration**: Guided capture for Front, Left, and Right angles with real-time illumination and blur quality scoring.
- **Admin & Faculty Dashboard**: Comprehensive metrics including Total Students (60), Present (48), Absent (12), Attendance Rate (80%), and interactive Recharts visualizations (Daily Area trends, Weekly Bars, Department comparisons, and Eligibility tiers).
- **Attendance Management & Export**: Search, date range filtering, department filters, status filters, and one-click **CSV** and **Formatted Printable PDF** report generation.
- **Student Biometric Profiles**: Profile photos, attendance history calendars, attendance rate progress rings, and examination eligibility indicators (75% cutoff).
- **AI Verification Audit Trail**: Granular logs storing timestamps, student identifiers, confidence scores, threshold comparisons, and outcome badges (`Verified`, `Failed`, `Unknown Face`).
- **Interactive Demo Mode**: Out-of-the-box simulation engine that allows testing and demonstration without external cloud database dependencies.

---

## 🏗️ 3. System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    React + Vite Frontend                    │
│    (Tailwind CSS, TypeScript, Canvas Face HUD, Web Audio)   │
└──────────────┬──────────────────────────────┬───────────────┘
               │                              │
      REST API Requests               Webcam Stream + HUD
               │                              │
┌──────────────▼──────────────┐               │
│   Node.js / Express Backend │               │
│   - Authentication & JWT    │               │
│   - Student Database CRUD   │               │
│   - Attendance Verification │               │
│   - Analytics & Reporting   │               │
└──────────────┬──────────────┘               │
               │                              │
        ┌──────┴──────────────┐               │
        │                     │               │
┌───────▼─────────────┐ ┌─────▼───────────────▼──────────────┐
│  Database Layer     │ │       Python AI Microservice       │
│  - Supabase / SQL   │ │  - OpenCV Face Localization        │
│  - In-Memory Mock   │ │  - 128D Feature Embedding Engine   │
│    Data Fallback    │ │  - Prototype Optical Liveness      │
└─────────────────────┘ └────────────────────────────────────┘
```

---

## 🛠️ 4. Technology Stack

| Layer | Technologies |
|---|---|
| **Frontend** | React.js 18/19, TypeScript, Vite, Tailwind CSS, Lucide React, Recharts, Canvas-Confetti |
| **Backend** | Node.js, Express.js, JWT, BcryptJS, CORS, Morgan |
| **AI / Computer Vision** | Python 3.10+, OpenCV (`cv2`), NumPy, SciPy (Spatial Vector Distances), Flask |
| **Database** | Supabase (PostgreSQL) with built-in persistent fallback store |

---

## 📂 5. Project Directory Structure

```text
Mini project/
├── frontend/                     # React + TypeScript + Vite UI
│   ├── public/
│   │   └── favicon.svg           # AI face scan branding favicon
│   ├── src/
│   │   ├── components/           # Navbar, Sidebar, CameraFeed, StatCard, Badge, Modal, PrivacyBanner
│   │   ├── pages/                # Home, Login, Dashboard, Register, Verify, Records, Profile, Logs, Reports, Settings, About
│   │   ├── services/             # api.ts, demoService.ts, faceEngine.ts, exportUtils.ts
│   │   ├── types/                # TypeScript interfaces and model definitions
│   │   ├── App.tsx               # Main routing & state container
│   │   ├── main.tsx
│   │   └── index.css             # Tailwind styling and neon glow effects
│   ├── package.json
│   └── vite.config.ts
│
├── backend/                      # Node.js + Express REST API Server
│   ├── controllers/              # authController, studentController, attendanceController, aiController
│   ├── routes/                   # authRoutes, studentRoutes, attendanceRoutes, aiRoutes
│   ├── middleware/               # authMiddleware (JWT), errorHandler
│   ├── services/                 # supabaseClient.js, mockDatabase.js, aiServiceConnector.js
│   ├── package.json
│   ├── .env.example
│   └── server.js
│
├── ai-service/                   # Python AI & Computer Vision Microservice
│   ├── face_detection.py         # OpenCV Haar/DNN face localization & image sharpness
│   ├── face_recognition.py      # 128D spatial embedding extraction & cosine similarity
│   ├── liveness.py               # Eye blink and optical motion anti-proxy detection
│   ├── app.py                    # Flask REST API endpoints
│   ├── requirements.txt
│   └── README.md
│
├── database/
│   └── schema.sql                # Complete PostgreSQL / Supabase schema & initial seed data
│
└── README.md                     # Comprehensive documentation & Expo guide
```

---

## 🚀 6. Installation & Execution Guide

### Prerequisites
- **Node.js**: v18.0.0 or higher
- **Python**: v3.9 or higher
- **NPM**: v9.0.0 or higher

---

### Step 1: Run Frontend (React + Vite)
```bash
cd frontend
npm install
npm run dev
```
Open **`http://localhost:5173`** in your browser.

---

### Step 2: Run Backend API (Node.js + Express)
```bash
cd backend
npm install
npm start
```
The API server will launch on **`http://localhost:5000`** with `/health` endpoint available.

---

### Step 3: (Optional) Run Python AI Microservice
```bash
cd ai-service
# Create and activate virtual environment
python -m venv venv
# On Windows:
venv\Scripts\activate
# On Linux/macOS:
source venv/bin/activate

pip install -r requirements.txt
python app.py
```
The Python AI service will run on **`http://127.0.0.1:8000`**.

> **Note**: If the Python service is not running, the Node backend and React frontend will automatically use the built-in mathematical vector similarity engine without interrupting the demonstration!

---

## 🔑 7. Default Demo Accounts

| Role | Email | Password |
|---|---|---|
| **Administrator** | `admin@attendai.edu` | `admin123` |
| **Faculty Teacher** | `teacher@attendai.edu` | `teacher123` |

*A 1-Click Demo Login button is also directly available on the Login screen for immediate presentation access.*

---

## 📡 8. REST API Reference

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/auth/login` | Authenticates faculty/admin and returns JWT token |
| `GET` | `/api/auth/me` | Retrieves current session user details |
| `POST` | `/api/students/register` | Registers new student with 128D face embedding |
| `GET` | `/api/students` | Lists registered students with search & department filters |
| `GET` | `/api/students/:id` | Returns individual student profile & attendance history |
| `POST` | `/api/attendance/verify` | Executes live facial recognition and marks attendance |
| `GET` | `/api/attendance` | Returns filterable attendance logs |
| `GET` | `/api/attendance/report` | Returns aggregated metrics and daily/weekly trend series |
| `GET` | `/api/attendance/logs` | Returns cryptographic AI verification audit history |
| `POST` | `/api/ai/recognize` | Python computer vision face recognition endpoint |
| `POST` | `/api/ai/liveness` | Optical flow & blink liveness verification endpoint |
| `GET` | `/api/ai/status` | Heartbeat & service connectivity telemetry |

---

## 🔒 9. Security & Biometric Privacy

1. **Irreversible Vector Embeddings**: Facial images are processed into mathematical floating-point vectors from which raw facial images cannot be reverse-engineered.
2. **Password Security**: Password credentials are hashed using `bcrypt` with salt rounds.
3. **Role-Based Authorization**: Administrative and faculty actions are safeguarded with JSON Web Tokens (JWT).
4. **Audit Trails**: Every verification attempt (whether passed, failed, or unknown) is permanently recorded in the audit log for institutional integrity.

---

## 🎓 10. College Expo / Mini-Project Presentation Tips

1. **Start with the Problem**: Highlight how traditional attendance wastes 15% of class time and allows proxy check-ins.
2. **Demonstrate Registration**: Show the 3-angle facial capture (Front, Left, Right) and mention the 128D mathematical vector generation.
3. **Demonstrate Live Attendance**:
   - Verify a registered student (e.g., Harish Kumar) to show the `✓ Attendance Verified` badge, confidence score, and audio chime.
   - Toggle **Test Unknown Face** to show how proxy attempts with confidence below the 85% threshold trigger the `⚠ Student Not Recognized` safety block.
4. **Show Analytics & Reports**: Present the Recharts attendance trend graphs, department breakdowns, and export a sample **Printable PDF** report.

---

## 📜 License
Developed for Academic Mini-Project & College Expo Demonstration. Built with educational AI architecture best practices.
