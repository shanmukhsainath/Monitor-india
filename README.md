# AirWise India

AirWise India is a full-stack air-quality monitoring platform focused on Indian cities and states. It combines interactive AQI maps, analytics dashboards, role-based workflows, alerts, and an AI chatbot for health and pollution guidance.

## What this project includes

- **Frontend (React + TypeScript + Vite):** dashboards, maps, admin/collector/customer pages, chatbot UI, and theme support.
- **Backend (Node + Express):** AQI APIs, chatbot APIs, alert APIs, station management, and analytics endpoints.
- **Role-oriented flows:** Admin, Collector, and Customer experiences.
- **Mock + AI-assisted data flow:** Core data works locally; chatbot can use OpenAI when configured.

## Tech stack

### Frontend
- React 18
- TypeScript
- Vite 5
- Tailwind CSS
- shadcn/ui + Radix UI
- TanStack Query
- Leaflet + leaflet.heat
- Chart.js + Recharts
- Vitest + Testing Library

### Backend
- Node.js
- Express
- OpenAI SDK
- dotenv
- cors

## Project structure

```text
airwise-india/
├─ src/                     # React app
├─ public/                  # Static assets
├─ server/                  # Express API
│  ├─ data/                 # AQI datasets + knowledge base
│  ├─ services/             # Chat, alerts, map analytics, logging
│  ├─ .env.example
│  └─ index.js
├─ package.json             # Frontend scripts/deps
└─ README.md
```

## Prerequisites

- Node.js 18+ (Node.js 20+ recommended)
- npm (or Bun)

## Local setup

### 1) Install frontend dependencies

```bash
npm install
```

### 2) Install backend dependencies

```bash
cd server
npm install
cd ..
```

### 3) Configure backend environment

Create `server/.env` from `server/.env.example`:

```env
OPENAI_API_KEY=your_openai_api_key_here
PORT=3001
NODE_ENV=development
CORS_ORIGINS=http://localhost:5173,http://localhost:3000
```

> If `OPENAI_API_KEY` is missing, chatbot features still run with fallback behavior.

### 4) Run both apps

Terminal 1 (frontend):

```bash
npm run dev
```

Terminal 2 (backend):

```bash
cd server
npm run dev
```

Default URLs:
- Frontend: `http://localhost:5173`
- Backend: `http://localhost:3001`

## Scripts

### Root (`airwise-india/package.json`)

- `npm run dev` – start Vite dev server
- `npm run build` – production build
- `npm run build:dev` – development-mode build
- `npm run preview` – preview production build
- `npm run lint` – run ESLint
- `npm run test` – run tests once (Vitest)
- `npm run test:watch` – run tests in watch mode

### Server (`airwise-india/server/package.json`)

- `npm run dev` – run backend with watch mode
- `npm start` – run backend in standard mode

## API overview

Base URL: `http://localhost:3001`

### Health + AQI
- `GET /api/health`
- `GET /api/aqi?city=<city>` or `GET /api/aqi?lat=<lat>&lng=<lng>`
- `GET /api/aqi/all`
- `GET /api/aqi/location?lat=<lat>&lng=<lng>`
- `GET /api/health-advice?aqi=<value>`

### Chatbot
- `POST /api/chatbot`
- `GET /api/chatbot/history/:userId`
- `GET /api/admin/chatbot/logs`
- `GET /api/admin/chatbot/stats`

### Alerts
- `POST /api/set-alert`
- `GET /api/alerts`
- `DELETE /api/alerts/:alertId`
- `POST /api/collector/trigger-alert`
- `GET /api/admin/alerts`
- `POST /api/admin/send-alert`
- `GET /api/admin/notifications`

### AQI map + stations + analytics
- `GET /api/aqi-map-data`
- `POST /api/admin/stations`
- `PUT /api/admin/stations/:stationId`
- `DELETE /api/admin/stations/:stationId`
- `GET /api/collector/stations`
- `PUT /api/collector/stations/:stationId`
- `POST /api/collector/stations`
- `GET /api/aqi-history`
- `GET /api/analytics/monthly`
- `GET /api/analytics/top-polluted`
- `GET /api/analytics/summary`

## Frontend API configuration

The frontend service defaults to:

- `http://localhost:3001`

To override, set:

```env
VITE_CHATBOT_API_URL=http://localhost:3001
```

## Deployment notes

- Deploy frontend and backend separately.
- Set CORS origins in backend to your frontend domain(s).
- Provide `OPENAI_API_KEY` in backend environment for full chatbot capability.

## License

This project currently has no explicit license file in the repository.
