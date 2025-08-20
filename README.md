# Citizen Portal Deploy Repo

This repository contains the **production deployment setup** of the Citizen Portal App using Docker Compose.

## Production Mode

### Prerequisites

- Docker
- Docker Compose

### Build and Start Containers

1. Clone all three repositories (**frontend**, **backend**, and **deploy**) into the **same parent folder**:

   ```bash
   git clone <frontend-repo-url>
   git clone <backend-repo-url>
   git clone <deploy-repo-url>
   cd <deploy-repo-folder>
   ```

2. Build and start containers:

   ```bash
   docker-compose up --build
   ```

3. Seed the backend with a default admin user:

   ```bash
   npm run admin:seed:docker
   ```

   - This runs: `docker exec -it citizen-backend node dist/scripts/seedAdmin.js`
   - Default credentials: username: `admin` | password: `admin123!`
   - You can change these credentials later in the app.

4. Access the app in your browser:

   ```
   http://localhost:80 or http://localhost:8080
   ```
