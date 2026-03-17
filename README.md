# VelaHire - AI Career Co-Pilot

Full-stack AI-powered job application platform with Multi-Agent architecture.

## Architecture

```
VelaHire/
├── backend/                    # Python FastAPI backend
│   ├── app/
│   │   ├── agents/             # Multi-Agent system (6 AI agents + orchestrator)
│   │   ├── adapters/           # Platform adapters (Workday, Greenhouse, Lever, iCIMS)
│   │   ├── api/                # REST API endpoints
│   │   ├── core/               # Config, security, database
│   │   ├── middleware/         # Auth, rate limiting
│   │   ├── models/             # SQLAlchemy models
│   │   ├── schemas/            # Pydantic schemas
│   │   ├── services/           # Business logic services
│   │   ├── tasks/              # Celery async tasks
│   │   └── utils/              # Encryption, validation, anti-detection
│   ├── alembic/                # Database migrations
│   └── tests/                  # Backend tests
├── frontend/                   # Next.js 14 frontend
│   └── src/
│       ├── app/                # App Router pages
│       │   ├── (auth)/         # Login, Register
│       │   └── dashboard/      # Dashboard, Jobs, Applications, Resume, Interview, Analytics, Settings
│       ├── components/         # Reusable components
│       │   ├── ui/             # shadcn/ui components
│       │   ├── layout/         # Sidebar, Navbar
│       │   ├── dashboard/      # Stats, Funnel, Recent Applications
│       │   ├── jobs/           # Job Card, Match Analysis
│       │   └── resume/         # Upload Zone, Score Breakdown, Career Path
│       └── lib/                # Utilities, API client, Zustand store
├── docker-compose.yml          # Full dev environment
├── Makefile                    # Common commands
└── .github/workflows/ci.yml   # CI pipeline
```

## Multi-Agent System

| Agent | Role |
|-------|------|
| **ProfileAgent** | Resume parsing, profile building, ATS scoring |
| **ScoutAgent** | Job discovery, matching, market analysis |
| **WriterAgent** | Cover letter, resume tailoring, open Q&A |
| **ApplyAgent** | Automated form filling, OTP handling, submission |
| **MonitorAgent** | Email monitoring, status tracking, weekly reports |
| **CoachAgent** | Interview prep, mock interviews, career coaching |

## Tech Stack

- **Frontend**: Next.js 14, TypeScript, TailwindCSS, Recharts, Zustand
- **Backend**: FastAPI, SQLAlchemy, Alembic, Celery
- **AI**: OpenAI GPT-4o, Anthropic Claude, LangGraph
- **Database**: PostgreSQL, Redis, Qdrant (vector search)
- **Automation**: Playwright (browser), RabbitMQ (task queue)
- **Infrastructure**: Docker, GitHub Actions CI

## Quick Start

```bash
# Clone and setup
cp .env.example .env

# Start all services
make docker-up

# Or run individually:
# Backend
cd backend && pip install -r requirements.txt && uvicorn app.main:app --reload

# Frontend
cd frontend && npm install && npm run dev
```

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/v1/auth/register` | User registration |
| POST | `/api/v1/auth/login` | User login |
| POST | `/api/v1/resume/upload` | Upload & parse resume |
| GET | `/api/v1/resume/score/{id}` | ATS score breakdown |
| GET | `/api/v1/jobs/match` | Get matched jobs |
| POST | `/api/v1/jobs/{id}/tailor` | Generate tailored content |
| POST | `/api/v1/applications/apply/{id}` | Auto-apply to job |
| GET | `/api/v1/dashboard/overview` | Dashboard data |
| POST | `/api/v1/interview/prep/{id}` | Interview prep materials |
| GET | `/api/v1/salary/insight/{id}` | Salary intelligence |
