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

No separately maintained threat model, privacy/data-flow guide, deployment procedure for the checked-out source, release process, operational runbook, or forecast evaluation report was identified in the inspected tree. Add these only with an accountable maintainer and repository-backed evidence.

## Evidence boundary

Simulation outputs are not proof of forecast accuracy. API routes, dependency declarations, test-like scripts, and container images do not prove a passing test suite or production deployment.