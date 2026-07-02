# CloudBees Unify Candidate Demo — Application (Release Orchestration)

This is the **Application** repository for the CloudBees Unify SE candidate demo. It holds the **Release Orchestration (RO)** workflows that coordinate a release across multiple components.

It is intentionally **separate from the component repository**, because in CloudBees Unify an Application and a Component cannot be the same repo:

- **Component repo** — [`cloudbees-unify-demo-kit`](https://github.com/cb-demos/cloudbees-unify-demo-kit): CI (build/test/scan) and component deployment for `orders-api`.
- **Application repo** — this repo: staged, governed release workflows that orchestrate `orders-api`, `payments-api`, and `web-frontend`.

**Everything here is self-contained and mock/echo-based**, and **every job publishes evidence** to the run's **Evidence** tab. The workflows run green in any CloudBees Unify org with **no clusters, secrets, registries, or integrations** required.

## Quick start

1. **Fork** this repository.
2. **Connect** it to your CloudBees Unify organization as an **Application**.
3. Open a release workflow under `.cloudbees/workflows/` and click **Run workflow**.
4. Open the run and review the **Evidence** tab per job.

## Release workflows

- `.cloudbees/workflows/release-finsure-bank.yaml` — **FinSure Bank**, regulated financial services. Governance → staging → validation → production approval → production → evidence package. Emphasizes auditability, change tickets, and approvals.
- `.cloudbees/workflows/release-horizon-health.yaml` — **Horizon Health Systems**, healthcare / platform engineering. Golden-path check → QA → validation → staging → summary. Emphasizes release standardization and health-data compliance. (`payments-api` is intentionally not deployed in this scenario.)

Each job publishes a Markdown **evidence item** via the native-workflow action `https://github.com/cloudbees-io/publish-evidence-item@v1` (no PAT required).

## Supporting props (evidence / talking points)

- `manifests/` — sample release manifests per scenario
- `policies/` — mock governance, approval, and change-control YAML
- `mock-data/` — mock Jira, ServiceNow, security, and release evidence data

## Demo tips

- Run a release end-to-end and walk the Evidence tab job by job to tell the governance/audit story.
- In the Unify Workflow Composer, add a **real manual approval gate** where the `production-approval` step is, to show governance live.
- Pair with the component repo's `ci.yaml` to show the full build → release story across the two repos.
