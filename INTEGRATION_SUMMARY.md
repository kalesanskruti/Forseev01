# FORSEE Integration & Deployment Guide

## ✅ Integration Status: COMPLETE

The **FORSEE** platform is fully integrated, connecting the React frontend with the FastAPI backend, PostgreSQL database, and Redis cache.

### 🚀 Quick Start (Submission Mode)

To run the entire verified stack:

1.  **Ensure Docker Desktop is Running** (Restart if necessary).
2.  **Build & Launch**:
    ```bash
    docker-compose up --build -d
    ```
3.  **Access the Application**:
    *   **Frontend**: [http://localhost:3000](http://localhost:3000)
    *   **Backend API Docs**: [http://localhost:8000/docs](http://localhost:8000/docs)

---

### 🔗 Architecture & Integration Details

The project is structured as a unified microservices architecture:

1.  **Frontend (`vite_react_shadcn_ts`)**:
    *   **Authentication**: Fully wired to using JWT tokens.
    *   ** Dashboard**: Fetches real-time KPI, Fleet, and Audit data from the backend.
    *   **Environment**: dynamically configured via `VITE_API_URL`.

2.  **Backend (`Forsee_FV`)**:
    *   **API Gateway**: `main.py` serves as the entry point.
    *   **Database**: PostgreSQL (with TimescaleDB support enabled but optional).
    *   **Seeding**: Automatically seeds initial **Admin User**, **Organization**, and **Industrial Assets** on startup.
    *   **ML Engine**: Optimized for CPU inference for deployment portability.

3.  **Infrastructure**:
    *   **Docker Compose**: Orchestrates all 5 containers (Frontend, Backend, Worker, DB, Redis).
    *   **Persistence**: Docker volumes ensure data is saved between restarts.

### 🧪 Verification Steps

We have included automated scripts to verify the integrity of the deployment:

1.  **Initialize Admin User**:
    ```bash
    docker-compose exec backend python scripts/create_admin.py
    ```
    *   **User**: `admin@forsee.ai`
    *   **Pass**: `password123`

2.  **Seed Demo Assets**:
    ```bash
    docker-compose exec backend python scripts/seed_assets.py
    ```

3.  **Run Integration Test Suite**:
    ```bash
    docker-compose exec backend python scripts/test_integration.py
    ```
    *   *Verifies Authentication Flow, API Reachability, and Data Structure Integrity.*

---

### 📂 Project Structure for Submission

*   `/frontend`: complete React source code.
*   `/Forsee_FV`: Backend Python source code, ML pipelines, and API.
*   `docker-compose.yml`: Root orchestration file.
*   `.env`: Centralized configuration.
