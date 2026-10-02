# Security and data handling

## Scope and data flow

The checked-in application accepts seed documents and uses configured LLM and Zep services. Seed text, prompts, generated agent content, graph data, and reports may leave the local application boundary. This repository does not establish third-party retention behavior, tenant isolation, or production access controls.

## Safe handling

- Do not upload confidential, personal, regulated, or otherwise sensitive seed material until the accountable data owner approves the provider, purpose, retention, and access model.
- Keep LLM and Zep credentials in an untracked local environment file; never commit keys or include them in logs/issues.
- Treat simulated posts, forecasts, and generated reports as model output, not evidence or verified predictions. Require human review before using outputs for consequential decisions.
- Review authentication, authorization, upload validation/limits, path handling, graph access, and report access before any public or multi-user deployment.
- Define retention and deletion for source uploads, graph state, traces, and reports; the reviewed docs do not establish a complete cleanup process.

## Verification boundary

This document records repository-visible configuration and source references. No provider, upload, deployment, access-control, retention, or runtime test was performed for this documentation change. It is not a security or privacy certification.

Report security issues privately to the repository maintainer; do not include sensitive source material or credentials in public issues.
