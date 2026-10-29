# Zero-Trust Cloud Lab

## Brief description
A cloud security architecture built on the **never trust, always verify** principle, featuring multi-factor authentication, an API gateway, and containerized microservices.

## Project purpose
Prototype a zero-trust style service layout with JWT/MFA-oriented auth, Nginx API gateway controls, PostgreSQL, Docker Compose, and Kubernetes manifests for academic cloud-security work.

## Project requirements
- Docker Desktop (or Docker Engine + Compose)
- Node.js 18+ (for local auth-service work)
- Optional: kubectl if deploying the Kubernetes manifests
- Free local ports used by Compose (see `docker-compose.yml`)

## How to navigate
- `src/auth-service/` — authentication microservice
- `src/api-gateway/` — Nginx gateway config
- `kubernetes/` — deployment manifests
- `data-collection/` — synthetic/Azure log tooling
- `docs/` — zero-trust notes
- `docker-compose.yml` — local multi-container stack
- `START_HERE.md`, `QUICKSTART.md` — deeper lab guides

## How to run
```bash
docker compose up -d
```

Then check the health endpoint (default guide uses `http://localhost:8080/health`).

For service-level development:

```bash
cd src/auth-service
npm install
npm start
```

See `START_HERE.md` for the full lab walkthrough.