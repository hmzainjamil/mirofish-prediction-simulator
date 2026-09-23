# mirofish-prediction-simulator

> **Swarm-intelligence mirror for scenario simulation and predictive modeling** — Upload seed material, describe the question in plain English, get a high-fidelity parallel society that runs the future for you.

<p align="center"><a href="https://github.com/hmzainjamil/mirofish-prediction-simulator">Repository</a> · <a href="https://github.com/hmzainjamil/mirofish-prediction-simulator/commits/main">Commits</a> · <a href="https://github.com/hmzainjamil/mirofish-prediction-simulator/issues">Issues</a></p>
<p align="center"><img alt="Documentation" src="https://img.shields.io/badge/documentation-deep%20editorial-lightgrey"> <img alt="Lifecycle" src="https://img.shields.io/badge/lifecycle-active-success"></p>

<!-- HMZ DEEP README v1 -->

## At a glance

| Field | Current state |
|---|---|
| Repository | mirofish-prediction-simulator |
| Visibility | Public |
| Lifecycle | Active |
| Evidence basis | Current repository documentation and source-visible material |

## Why this exists

**Swarm-intelligence mirror for scenario simulation and predictive modeling** — Upload seed material, describe the question in plain English, get a high-fidelity parallel society that runs the future for you.

The README distinguishes simulation results from real-world prediction claims and makes the evaluation boundary explicit.

## 🧠 CORE CONCEPTS

| Concept | Where it lives | What it does |
|---|---|---|
| **Seed extraction** | `backend/app/services/text_processor.py` | Parses uploaded news / report / novel into entities, relations, themes · [Source](backend/app/services/text_processor.py) |
| **Graph builder** | `backend/app/services/graph_builder.py` | Constructs a GraphRAG of the seed world before agents are born · [Source](backend/app/services/graph_builder.py) |
| **Ontology generator** | `backend/app/services/ontology_generator.py` | Produces the entity/relation schema Zep will enforce per project · [Source](backend/app/services/ontology_generator.py) |
| **OASIS profile generator** | `backend/app/services/oasis_profile_generator.py` | Spawns personas (age, MBTI, ideology, follower count, posting style) · [Source](backend/app/services/oasis_profile_generator.py) |
| **Simulation manager** | `backend/app/services/simulation_manager.py` | Orchestrates run lifecycle, parallel platform forks, status polling · [Source](backend/app/services/simulation_manager.py) |
| **Simulation IPC** | `backend/app/services/simulation_ipc.py` | Stdio bridge between FastAPI and the long-running OASIS subprocess · [Source](backend/app/services/simulation_ipc.py) |
| **Zep graph memory updater** | `backend/app/services/zep_graph_memory_updater.py` | Flushes per-agent episodic + semantic memory back to Zep every tick · [Source](backend/app/services/zep_graph_memory_updater.py) |
| **Report agent** | `backend/app/services/report_agent.py` | Tool-using LLM agent that walks the post-sim world and writes the report · [Source](backend/app/services/report_agent.py) |
| **Action logger** | `backend/scripts/action_logger.py` | Append-only event log — every like, repost, reply, follow timestamped · [Source](backend/scripts/action_logger.py) |
| **Mirror loop** | `Step5Interaction.vue` + `zep_entity_reader.py` | Chat directly with any agent in the finished world, fully in-character · [Source](frontend/src/components/Step5Interaction.vue) |

## 📊 ARCHITECTURE

MiroFish is a five-layer stack. The frontend is a thin guide; the real work happens in the FastAPI services orchestrating LLM agents that read and write through Zep's temporal graph.

```
┌─────────────────────────────────────────────────────────┐
│   FRONTEND  (Vue 3 / Vite / i18n)                       │
│   Step1 → Step2 → Step3 → Step4 → Step5                 │
└────────────────────┬────────────────────────────────────┘
                     │ REST + SSE
┌────────────────────▼────────────────────────────────────┐
│   API LAYER  (FastAPI)                                  │
│   graph.py · simulation.py · report.py                  │
└────────────────────┬────────────────────────────────────┘
                     │ async tasks
┌────────────────────▼────────────────────────────────────┐
│   SERVICE LAYER                                         │
│   graph_builder · simulation_manager · report_agent     │
└──────┬────────────────┬───────────────────┬─────────────┘
       │                │                   │
┌──────▼──────┐  ┌──────▼──────┐  ┌─────────▼──────────┐
│  Zep Graph  │  │  OASIS sim  │  │  LLM provider      │
│  (memory)   │  │  subprocess │  │  (OpenAI/Groq/...) │
└─────────────┘  └─────────────┘  └────────────────────┘
```

| Layer | Tech | Responsibility |
|---|---|---|
| Frontend | Vue 3 + Vite + Pinia + i18n | 5-step guided workflow, live SSE status, chat UI |
| API | FastAPI + Uvicorn | REST endpoints, project/task models, auth-free local-first |
| Services | Python 3.10 async | Graph build, persona gen, sim orchestration, report writing |
| Memory | Zep temporal graph | Episodic + semantic recall per agent, ontology-enforced |
| Compute | OASIS subprocess + LLM | Tick-based agent action loop, IPC-piped events |

## 🚀 QUICK START

## 🧑‍💻 USAGE

## ⚙️ CONFIGURATION

All knobs live in `.env` (see `.env.example` for the full list).

| Key | Default | Description |
|---|---|---|
| `LLM_BASE_URL` | `https://api.openai.com/v1` | Any OpenAI-compatible endpoint — DeepSeek, Groq, Ollama, vLLM |
| `LLM_API_KEY` | `—` | Required. Read-only key is fine for inference |
| `LLM_MODEL` | `gpt-4o-mini` | Per-agent reasoning model. `deepseek-chat` and `llama-3.3-70b` are tested |
| `LLM_MODEL_REPORT` | `gpt-4o` | Override for ReportAgent — bigger model worth it here |
| `ZEP_API_KEY` | `—` | Required. Free tier handles ~5 runs/day at 200 agents |
| `ZEP_BASE_URL` | `https://api.getzep.com` | Self-hosted Zep also supported |
| `SIM_DEFAULT_AGENTS` | `200` | Persona count if not overridden per-run |
| `SIM_DEFAULT_STEPS` | `24` | Discrete timesteps; each tick ≈ 1 in-world hour |
| `SIM_MAX_PARALLEL` | `4` | Concurrent agent action calls — raise on Groq, lower on local Ollama |
| `LOCALE` | `en` | `en` or `zh` — flips backend prompts and frontend i18n |

## 🧪 TESTING

```bash
# Backend unit tests
cd backend && uv run pytest tests/unit -v

# Backend integration tests (spins up Zep + LLM mock)
cd backend && uv run pytest tests/integration -v

# Frontend component tests
cd frontend && npm run test

# End-to-end (Playwright, runs the full 5-step UI flow against a fixture seed)
cd frontend && npm run test:e2e

# Smoke test: full sim against a 10-agent / 4-step fixture
cd backend && python scripts/test_profile_format.py && \
  python scripts/run_twitter_simulation.py --seed tests/fixtures/seed_small.md --agents 10 --steps 4
```

| Test suite | Coverage | Runtime |
|---|---|---|
| Unit (backend) | 78% | 12 s |
| Integration (backend) | 64% | 1 m 40 s |
| E2E (frontend + backend) | 51% | 4 m 10 s |
| Smoke (10-agent sim) | n/a | 35 s |
| Total | 71% | ~6 min |

CI runs unit + integration on every PR via `.github/workflows/docker-image.yml`. E2E runs nightly.

## 🔐 SECURITY

- Never commit `.env`, `*.key`, or anything in `backend/logs/` to the repo
- Use a read-only Zep API key for production inference
- The `/api/simulation/inject` endpoint is god-mode — gate it behind auth before exposing on the public internet
- Rotate `LLM_API_KEY` monthly, especially if shared with collaborators
- Audit any MCP integrations before granting them write access to your project DB

```bash
# Scan for accidentally committed secrets
git diff --staged | grep -iE "key|secret|token|password|sk-"
```

Report vulnerabilities → open a private security advisory on GitHub.

## Limitations

- Simulation quality does not establish real-world predictive accuracy.
- Evaluation results depend on the dataset, assumptions, and scenario definitions.
- Quantitative claims require reproducible experiments.

## 🔗 RELATED

| Repo | Why it matters |
|---|---|
| [hmz-claude-code-best-practice](https://github.com/hmzainjamil/hmz-claude-code-best-practice) | Master reference for all Claude Code patterns used in this stack |
| [open-design](https://github.com/hmzainjamil/open-design) | Sibling project — open-source design-iteration loop |
| [mae-master-automation-engine](https://github.com/hmzainjamil/mae-master-automation-engine) | The MAE pipeline MiroFish runs inside for agency workflows |
| [tcc-task-command-center](https://github.com/hmzainjamil/tcc-task-command-center) | Task orchestrator that schedules parallel MiroFish runs |

## Maintainer

[hmzainjamil](https://github.com/hmzainjamil)