# MiroFish Prediction Simulator

MiroFish is a web application for building a simulated multi-agent environment from seed material, running scenario simulations, and generating reports. Simulation output is model-generated scenario analysis, not a verified forecast of real-world events.

> **Status:** Source tree inspected. Runtime behavior, external providers, deployment, simulation quality, and test results were not verified in this documentation update.

## How it is structured

| Component | Location | Evidence |
|---|---|---|
| Vue 3 and Vite frontend | frontend/ | Source and package scripts |
| Flask API | backend/app/api/ | Graph, simulation, and report route modules |
| Simulation and graph services | backend/app/services/ | Source modules for graph building, profiles, simulation, and reports |
| External services | Zep Cloud and an OpenAI-compatible LLM endpoint | Dependency/configuration references; no live connection checked |
| Research and evaluation | backend/scripts/ | Includes a profile-format script; no test suite results claimed |

The backend uses OASIS/Camel dependencies for social simulation and Zep Cloud for graph memory. Provider behavior and compatibility depend on external service versions and configuration.

## Local development

Requirements: Python 3.11 or newer, Node.js/npm, and uv.

    cp .env.example .env
    # Set the required LLM and Zep values in .env
    npm run setup:all
    npm run dev

The commands are from the root package scripts and backend configuration; they were not executed here. The frontend uses port 3000 and proxies API requests to port 5001. The backend defaults to binding 0.0.0.0:5001, and the frontend dev script passes Vite's --host. Treat both as network-accessible; do not expose them to an untrusted network. Review and restrict bindings before shared or public use.

## Configuration and data

The root .env.example lists LLM_API_KEY, LLM_BASE_URL, LLM_MODEL_NAME, ZEP_API_KEY, and optional provider settings. Keep credentials in an untracked local .env file.

Seed documents, prompts, generated agent content, and reports may be sent to configured LLM and Zep services. This repository does not establish local-only processing or third-party retention behavior. Review provider terms and data controls before using sensitive material.

## Validation and deployment

The prior README listed unit, integration, Playwright, smoke-test suites, coverage percentages, timings, and CI schedules that were not present in the inspected source tree. Those results and commands are removed until maintainers provide reproducible evidence. The root package currently defines setup, development, and frontend build scripts; no general test script is declared.

The checked-in Docker Compose file pulls ghcr.io/666ghj/mirofish:latest; it does not build the current checkout. Do not assume that image matches this repository revision.

## Limitations

- A simulation is a scenario exploration. It does not prove predictive accuracy or establish what will happen.
- Output quality depends on source material, model/provider behavior, simulation settings, and assumptions.
- No benchmark, production deployment, security review, or forecast-accuracy evidence is claimed here.

## Documentation

- [Documentation index](docs/README.md)
- [Backend API modules](backend/app/api/)
- [Simulation services](backend/app/services/)
- [Backend configuration](backend/app/config.py)
- [Environment template](.env.example)
- [License](LICENSE)

## License

The root [LICENSE](LICENSE) contains the GNU Affero General Public License version 3. See the license text for use and distribution terms.