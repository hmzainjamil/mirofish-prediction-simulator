# Documentation index

Use the root README for scope, local development, configuration, and evidence boundaries.

## Technical references

- [Backend API modules](../backend/app/api/)
- [Graph, simulation, and report services](../backend/app/services/)
- [Backend configuration](../backend/app/config.py)
- [Frontend package scripts](../frontend/package.json)
- [Environment variable template](../.env.example)
- [Docker Compose definition](../docker-compose.yml)
- [License](../LICENSE)

## Documentation gaps

[SECURITY.md](../SECURITY.md) records the inspected provider/data boundaries and handling cautions. A separate threat model, deployment procedure, release process, operational runbook, and forecast evaluation report were not identified.

## Evidence boundary

Simulation outputs are not proof of forecast accuracy. API routes, dependency declarations, test-like scripts, and container images do not prove a passing test suite or production deployment.