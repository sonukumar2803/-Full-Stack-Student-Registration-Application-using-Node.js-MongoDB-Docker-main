# Student Registration (Dockerized Full Stack)

## What you get
- **Frontend**: React + Vite, built and served by **Nginx**
- **Backend**: Node.js + Express
- **Database**: PostgreSQL
- **Single Port**: Nginx serves the frontend and proxies **/api** to the backend, so the whole site runs on **http://localhost:8080**

## Quick start
```bash
cd student-registration-docker
cp .env.example .env   # if needed
docker compose build
docker compose up
# Open http://localhost:8080
```

> Default DB credentials are in `.env`. Change them for production.

## Endpoints
- `GET /api/health` – check server & DB
- `POST /api/students` – body: `{ fullName, email, course, dob }`
- `GET /api/students` – list recent students

## Data
Server creates a `students` table automatically on start.

### CSV export
On each successful registration the backend will also append a row to `students.csv` at the repository root. This file can be opened directly to review registrations made via the web form or other clients.

If you want to append a sample row locally without running the full stack, run in the `backend` folder:

```
npm run append-sample "Full Name" "email@example.com" "Course" 2000-01-01
```


## One-port setup
Nginx serves static frontend and reverse-proxies `/api` to `backend:5000`. Only the Nginx service is exposed (`8080:80`).

## Dev tips
- To run just backend locally: `npm i` in `backend` and `node src/index.js` with env vars.
- To run frontend locally: `npm i` in `frontend` and `npm run dev`.
- In Docker, the multi-stage `nginx/Dockerfile` builds the frontend then serves it.
