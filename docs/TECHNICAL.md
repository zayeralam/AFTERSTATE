# AFTERSTATE — Technical notes

## Overview
A dependency-free Node.js HTTP application with browser frontend and JSON persistence. Intended for a single user on a trusted local device.

## Components
- `server.js`: HTTP routing, API, persistence, and heuristic risk.
- `public/`: static frontend.
- `data.json`: default store; configurable with `AFTERSTATE_DATA`.
- `tests/server.test.js`: Node integration tests.
- `.github/workflows/ci.yml`: CI test workflow.

## Run
Node.js 18+.
```bash
npm start
npm test
```
Default address is `127.0.0.1:3000`. `PORT` and `HOST` environment variables can override the listening port/address; changing HOST can expose the app to other devices and is discouraged.

## API
| Method | Route | Purpose |
|---|---|---|
| GET | `/api/health` | Health response |
| GET | `/api/summary` | Record, active, overdue, blocked, completed counts |
| GET | `/api/events` | Recent activity |
| GET | `/api/export` | JSON store export |
| GET | `/api/items` | List records; supports `q` and `status` |
| POST | `/api/items` | Create record |
| PATCH | `/api/items/:id` | Update record |
| DELETE | `/api/items/:id` | Delete record |

## Fields
Record fields include id, title, description, owner, due date, priority, status, creation/update timestamps. Priorities: `low`, `medium`, `high`, `critical`. Statuses: `open`, `in_progress`, `blocked`, `done`.

## Risk
Rule-based additive factors include blocked status, high/critical priority, absent owner, and due-date proximity/lateness. Score capped at 100; done records are 0. Not a validated prediction.

## Persistence
JSON store with `items` and `events`. Writes use temporary-file rename. No automated backups or recovery.

## Security limitations
- No authentication, authorization, or TLS.
- Intended only for loopback/local use.
- Not hardened for public or hostile-network exposure.
- No concurrency guarantees or production recovery.
- Treat store and export as sensitive if they contain personal details.
