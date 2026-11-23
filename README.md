# AFTERSTATE

**A local-first commitment accountability system.**

AFTERSTATE is a lightweight dashboard for recording commitments, tracking their status, and surfacing work that may need attention. It combines a commitment ledger, rule-based risk indicators, a recovery queue, and an activity trail.

> Risk scores are transparent heuristics intended to prompt review. They are not forecasts or guarantees.

## Capabilities
- **Commitment ledger:** create, edit, and delete records.
- **Status tracking:** open, in progress, blocked, and done.
- **Priority & ownership:** capture priority, owner, context, and due date.
- **Risk heuristics:** review a score based on status, priority, assignment, and deadline.
- **Recovery queue:** surface elevated-score records.
- **Search and filtering:** search record text and filter by status.
- **Activity trail:** view recent record actions.
- **JSON export:** export record and event data.
- **Local persistence:** JSON-file storage configurable through `AFTERSTATE_DATA`.

## Requirements
- Node.js 18 or later.
- No third-party runtime packages required.

## Run locally
```bash
git clone https://github.com/zayeralam/AFTERSTATE.git
cd AFTERSTATE
npm start
```
Open **http://localhost:3000** in your browser.

## Tests
```bash
npm test
```
The test suite uses Node's built-in test runner and starts an isolated server with temporary test data.

## Repository layout
| Path | Purpose |
|---|---|
| `server.js` | HTTP server, API routes, persistence, risk calculation |
| `public/` | Frontend structure, styles, client-side logic |
| `tests/server.test.js` | Integration tests |
| `.github/workflows/ci.yml` | GitHub Actions test workflow |
| `docs/TECHNICAL.md` | API and implementation notes |

## Risk-score model
The current implementation uses additive rules for factors such as blocked status, priority, missing owner, and deadline proximity or lateness. Scores are capped at 100; completed records score zero. See [Technical notes](docs/TECHNICAL.md). This is not a validated predictive model.

## Data and security boundary
AFTERSTATE is a **single-user local prototype**, not a hardened production service.
- No authentication or authorization.
- TLS is not configured.
- Do not expose it to the internet or an untrusted network.
- The default data file is `data.json`; protect and back up your data yourself.
- Scores are heuristics, not objective predictions.

## Continuous integration
GitHub Actions is configured to run the test suite on pushes and pull requests targeting `main`. Check the repository Actions tab for actual run results.

## Project status
The project is evolving. The current focus is dependable local commitment tracking, clear risk visibility, and reviewable recovery workflows.

[Repository](https://github.com/zayeralam/AFTERSTATE) · [Technical notes](docs/TECHNICAL.md)
