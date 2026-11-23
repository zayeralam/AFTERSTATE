# AFTERSTATE

**A local-first commitment accountability system.**

AFTERSTATE is a lightweight dashboard for recording commitments, tracking their status, and surfacing work that may need attention. It combines a commitment ledger, rule-based risk indicators, a recovery queue, and an activity trail.

> Risk scores are transparent heuristics intended to prompt review. They are not forecasts or guarantees.

## Capabilities
- **Commitment ledger:** create, edit, and delete records.
- **Status tracking:** open, in progress, blocked, and done.
- **Priority & ownership:** capture priority, owner, context, and due date.
- **Risk heuristics:** review scores based on status, priority, assignment, and deadline.
- **Recovery queue:** surface elevated-score records.
- **Search and filtering:** search record text and filter by status.
- **Activity trail:** review recent record actions.
- **JSON export:** export record and event data.
- **Local persistence:** JSON-file storage configurable through `AFTERSTATE_DATA`.

## Requirements
- Node.js 18 or later.
- No third-party runtime dependencies.

## Run locally
```bash
git clone https://github.com/zayeralam/AFTERSTATE.git
cd AFTERSTATE
npm start
```
Open **http://127.0.0.1:3000**. The server binds to loopback by default.

## Configuration
- `PORT`: listening port (default `3000`).
- `HOST`: listening address (default `127.0.0.1`).
- `AFTERSTATE_DATA`: JSON data-file path (default `data.json`).

## Tests
```bash
npm test
```
Tests use Node's built-in runner and isolated temporary storage.

## Repository layout
| Path | Purpose |
|---|---|
| `server.js` | HTTP server, API routes, persistence, risk calculation |
| `public/` | Frontend structure, styles, client-side logic |
| `tests/server.test.js` | Integration tests |
| `.github/workflows/ci.yml` | GitHub Actions workflow |
| `docs/TECHNICAL.md` | API and implementation notes |

## Risk-score model
Rule-based additive indicators include blocked status, high/critical priority, missing owner, and deadline proximity or lateness. Scores are capped at 100; completed records score zero. See [Technical notes](docs/TECHNICAL.md). This is not a validated predictive model.

## Data and security boundary
AFTERSTATE is a **single-user local prototype**, not a hardened production service.
- No authentication or authorization.
- TLS is not configured.
- By default, it binds to loopback; do not deliberately bind it to an untrusted network.
- The default data file is `data.json`; protect and back up your data yourself.
- Data writes are local; no built-in backup/recovery or multi-user guarantees.
- Scores are heuristics, not predictions.

## Continuous integration
GitHub Actions is configured to run tests on pushes and pull requests targeting `main`. Actual status is visible in the repository Actions tab.

## Project status
The project is an evolving local prototype focused on commitment tracking, reviewable risk visibility, and recovery workflows.

[Repository](https://github.com/zayeralam/AFTERSTATE) · [Technical notes](docs/TECHNICAL.md)
