# Citizen Portal Deploy Repo

This repository contains the **deployment setup** for the full Citizen Portal App (frontend + backend + MongoDB).

## Prerequisites

- Node.js 20.x (LTS) or 22.x (Current)
- npm
- Docker
- Docker Compose

## Run in Production Mode (Full App)

### 1. Clone all repositories

Make sure all three repos are cloned into the same parent folder:

```
citizen-portal-backend/
citizen-portal-frontend/
citizen-portal-deploy/
```

### 2. Build the frontend and backend locally

Since the Dockerfiles copy the `dist/` folders, you need to build them first:

```bash
# Backend
cd citizen-portal-backend
npm install
npm run build

# Frontend
cd ../citizen-portal-frontend
npm install
npm run build
```

### 3. Start the full stack with Docker Compose

From the deploy repo:

```bash
cd ../citizen-portal-deploy
docker compose up --build
```

This will start:

- **MongoDB** (with persistent volume `mongodb_data`)
- **Backend** (Node.js, served at port 5000)
- **Frontend** (served by Nginx at port 80 or 5173 depending on config)

### 4. Seed the database with a default admin user

After the containers are up and running, open a **new terminal** and navigate to the backend repo:

```bash
cd ../citizen-portal-backend
```

Run the following command to seed the database with a default admin user:

```bash
npm run admin:seed:docker
```

This will execute inside the backend container:

```bash
docker exec -it citizen-backend node dist/scripts/seedAdmin.js
```

Default credentials:

- **username:** `admin`
- **password:** `admin123!`

You can change these credentials later inside the app.

### 5. Access the app

- Frontend → `http://localhost:5173`
- Backend → `http://localhost:5000`

You can now log in with the seeded admin account.
