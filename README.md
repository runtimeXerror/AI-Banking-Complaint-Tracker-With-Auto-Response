# TrustDesk — AI Complaint Intelligence System
<img width="1911" height="922" alt="image" src="https://github.com/user-attachments/assets/2c655d9d-f6b0-4947-8ed6-4434d610d125" />
<img width="1890" height="916" alt="image" src="https://github.com/user-attachments/assets/37e98370-5877-41ec-8468-47eb5496cde7" />


Full-stack complaint management platform with:
- FastAPI backend + SQLite database
- HuggingFace NLP (sentiment analysis)
- Anthropic Claude GenAI (response drafting)
- Auto-acknowledgement draft on every new complaint
- Real-time dashboard with charts
- Command palette (⌘K)
- JWT authentication
- Insight Engine (complaint clustering)

---

## Quick Start (5 minutes)

### 1. Install dependencies
```bash
pip install fastapi uvicorn sqlalchemy python-jose[cryptography] passlib[bcrypt] anthropic python-multipart
```

### 2. (Optional) Install ML libraries for real NLP
```bash
pip install transformers torch scikit-learn
```

### 3. Add your API key
Open `main.py` and replace:
```python
ANTHROPIC_API_KEY = "sk-ant-YOUR_KEY_HERE"
```
with your actual Anthropic API key. If you skip this, it will use template responses.

### 4. Run the server
```bash
python main.py
```

### 5. Open the app
- **App:**      http://localhost:8000
- **API Docs:** http://localhost:8000/api/docs

---

## Default Login Credentials

| Email | Password | Role |
|-------|----------|------|
| arjun@sbi.com  | password | Admin      |
| priya@sbi.com  | password | Supervisor |
| rahul@sbi.com  | password | Agent      |
| sneha@sbi.com  | password | Agent      |

---

## Auto-Acknowledgement Feature

Every new complaint triggers an instant acknowledgement containing:
- Unique Ticket ID (e.g., TD-2026-0008)
- Customer name, product, channel, timestamp
- Assurance message that a team member is assigned
- Instructions to track complaint status

In production, this would be delivered via:
- SMS (Twilio)
- Email (SendGrid/SMTP)
- WhatsApp Business API

---

## API Endpoints

### Auth
- `POST /api/auth/login`     — Login, returns JWT token
- `POST /api/auth/register`  — Create new agent

### Complaints
- `POST   /api/complaints`              — Create complaint (triggers auto-draft)
- `GET    /api/complaints`              — List all (supports ?status=&severity=&search=)
- `GET    /api/complaints/{ticket_id}`  — Get single complaint
- `PATCH  /api/complaints/{ticket_id}`  — Update status/agent/severity
- `POST   /api/complaints/{ticket_id}/resolve`   — Mark resolved
- `POST   /api/complaints/{ticket_id}/escalate`  — Escalate to critical
- `POST   /api/complaints/{ticket_id}/notes`     — Add internal note

### AI
- `POST /api/ai/draft`                  — Generate AI response (3 tones)
- `GET  /api/ai/auto-draft/{ticket_id}` — Get auto-acknowledgement for ticket

### Analytics
- `GET /api/analytics/summary`       — Stats: open, resolved, avg time
- `GET /api/analytics/by-category`   — Complaints per product
- `GET /api/analytics/by-channel`    — Complaints per channel
- `GET /api/analytics/by-sentiment`  — Sentiment breakdown
- `GET /api/analytics/volume-trend`  — 7-day volume

### Insights
- `GET /api/insights/clusters`       — KMeans complaint clustering

---

## Project Structure

```
trustdesk/
├── main.py          ← Complete backend (FastAPI + SQLite + NLP + GenAI)
├── frontend.html    ← Complete frontend (served at http://localhost:8000)
├── requirements.txt ← Python dependencies
├── README.md        ← This file
└── trustdesk.db     ← SQLite database (auto-created on first run)
```

---

## For Production Deployment

| Component | Free Option |
|-----------|-------------|
| Backend   | Railway.app or Render.com |
| Database  | Supabase (Postgres) |
| Frontend  | Vercel or Netlify |
| ML Models | HuggingFace Inference API |
| GenAI     | Anthropic Claude API |
| SMS       | Twilio (auto-draft delivery) |
| Email     | SendGrid |

---

## Tech Stack

- **Backend:** Python · FastAPI · SQLAlchemy · SQLite
- **Auth:** JWT · bcrypt
- **NLP:** HuggingFace Transformers (twitter-roberta-base-sentiment)
- **GenAI:** Anthropic Claude Sonnet
- **Clustering:** scikit-learn KMeans · TF-IDF
- **Frontend:** Vanilla JS · Chart.js · DM Sans + Fraunces fonts
- **Charts:** Chart.js 4.4

---

Built for PSBs Hackathon 2026 · PS-05 · TrustDesk Team




