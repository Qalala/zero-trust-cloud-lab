# Zero-Trust Cloud Lab

A cloud-security lab built around the principle **“never trust, always verify.”** It prototypes an authentication service, an Nginx API gateway, PostgreSQL persistence, Docker Compose local orchestration, and Kubernetes manifests for a containerized microservices layout.

The stack is:
- **Auth microservice**: Node.js / Express + JWT / MFA-oriented flows
- **Gateway**: Nginx with rate-limiting / routing controls
- **Data**: PostgreSQL
- **Ops**: Docker Compose + Kubernetes YAML

This is an academic cloud-computing / security architecture project with week-by-week lab artifacts and a runnable local prototype.

## Tech stack
- Node.js / Express
- Nginx (API gateway)
- PostgreSQL
- Docker / Docker Compose
- Kubernetes
- JWT + MFA-oriented auth
- Azure-oriented lab tooling

## Architecture (high level)

```
Users / clients
        │
        ▼
┌──────────────────────┐
│   API Gateway        │  Nginx: routing, rate limits, edge controls
│   (src/api-gateway)  │
└─────────┬────────────┘
          │
          ▼
┌──────────────────────┐
│   Auth Service       │  JWT sessions, validation middleware, audit logs
│   (src/auth-service) │
└─────────┬────────────┘
          │
          ▼
┌──────────────────────┐
│   PostgreSQL         │  users / sessions / audit-related tables
└──────────────────────┘

Repo layout:
├─ docker-compose.yml
├─ kubernetes/                 [namespace, deployments, secrets template]
├─ src/
│  ├─ api-gateway/nginx.conf
│  └─ auth-service/        [Express app + Dockerfile]
├─ data-collection/          [synthetic / Azure log helpers]
├─ docs/                     [zero-trust notes]
├─ scripts/                  [setup / API test helpers]
└─ week5-data / week6-design / week7-prototype1
```

### What is implemented
- Authentication service with JWT-oriented access control
- Middleware for auth, validation, and errors
- Session / user / audit model scaffolding
- Nginx gateway config as the front door
- Docker Compose stack for local bring-up
- Kubernetes manifests for cluster-style deployment experiments
- Data-collection scripts for synthetic security/auth/network style logs

### Zero-trust ideas demonstrated
- No implicit trust based on network location alone
- Authenticate/authorize at the service edge
- Gateway as a controlled entry point
- Auditable auth/session activity
- Container isolation for services

---

## Running the project

### Prerequisites
- Docker Desktop (or Docker Engine + Compose plugin)
- Node.js 18+ if running auth-service outside Compose
- Optional: `kubectl` for Kubernetes experiments
- Free local ports used by Compose (Postgres `5432`, auth `8081`, gateway as configured)

### Quick start (recommended)

```bash
docker compose up -d
```

Then verify health using the project’s documented endpoint (commonly gateway health such as `http://localhost:8080/health` — confirm against your Compose/gateway mapping).

Copy env values from `env.template` if you need custom secrets/passwords.

### Auth service (local Node workflow)

```bash
cd src/auth-service
npm install
npm start
```

### Useful docs in this repo
- `START_HERE.md` — fastest onboarding path
- `QUICKSTART.md` / `QUICK_REFERENCE.md` — concise ops notes
- `FRONTEND_GUIDE.md` — UI/gateway interaction notes
- `IMPLEMENTATION_SUMMARY.md` / `PROJECT_STATUS.md` — progress snapshot
- `docs/zero-trust-principles.md` — conceptual background

---

## How to navigate the repo
- Runtime services: `src/auth-service`, `src/api-gateway`
- Local orchestration: `docker-compose.yml`
- Cluster manifests: `kubernetes/`
- Telemetry/lab data tools: `data-collection/`
- Weekly academic artifacts: `week5-data`, `week6-design`, `week7-prototype1`

---

## Demo walkthrough
1. Start Docker Desktop.
2. From the repo root: `docker compose up -d`.
3. Wait for Postgres healthcheck + auth container.
4. Hit the gateway/auth health or auth routes from the quickstart docs.
5. Register/login (as exposed by auth routes) and inspect JWT-protected behavior.
6. Optionally apply Kubernetes manifests in a local cluster (kind/minikube/AKS) using the templates under `kubernetes/`.

### Notes / limitations
- This is a **lab/prototype**, not a hardened production zero-trust mesh
- Secrets templates must be filled before real deployments
- Some week folders are documentation/design checkpoints around the running prototype
- Azure integration pieces are tooling/docs-oriented rather than a full managed cloud deployment out of the box

---

## Project purpose
Prototype a zero-trust style cloud security architecture with authenticated services, a controlled API gateway, containerization, and Kubernetes-ready packaging for academic cloud-security work.
