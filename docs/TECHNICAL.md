# AFTERSTATE — Technical notes

## Overview
AFTERSTATE is a dependency-free Node.js HTTP application with a browser frontend and JSON-file persistence. It is intended as a single-user local prototype.

## Components
- `server.js`: HTTP routing, API logic, persistence, and heuristic risk calculation.
- `public/`: static HTML, CSS, and JavaScript.
- `data.json`: default persistent store (not committed; configurable via `AFTERSTATE_DATA`).
- `tests/server.test.js`: integration tests using Node's built-in test runner.
- `.github/workflows/ci.yml`: CI test job.

## Run and test
Requires Node.js 18+.
```bash
npm start
npm test
```
The server defaults to port 3000; the `PORT` environment variable can override it. Storage location can be overridden with `AFTERSTATE_DATA`.

## API reference
| Method | Route | Purpose |
|---|---|---|
| GET | `/api/health` | Basic health response |
| GET | `/api/summary` | Record, active, overdue, blocked, completed counts |
| GET | `/api/events` | Recent activity events |
| GET | `/api/export` | JSON export of the store |
| GET | `/api/items` | List records; supports `q` and `status` query parameters |
| POST | `/api/items` | Create a record |
| PATCH | `/api/items/:id` | Update a record |
| DELETE | `/api/items/:id` | Delete a record |

## Record fields
Records include an identifier, title, description, owner, due date, priority, status, created timestamp, and updated timestamp. List/create/update responses include a calculated risk value.

Priorities: `low`, `medium`, `high`, `critical`. Statuses: `open`, `in_progress`, `blocked`, `done`.

## Risk heuristic
The rule-based score adds indicators for blocked status, high/critical priority, missing owner, and deadline proximity or lateness. It is capped at 100. Completed records return zero. It is a prioritization heuristic, not a validated predictive model.

## Persistence
The store is a JSON object containing `items` and `events`. Writes use a temporary file followed by rename. The application has no built-in backup or recovery mechanism.

## Security and limitations
- Single-user prototype only.
- No authentication, authorization, or TLS.
- Not hardened for public or hostile-network use.
- Local JSON storage by default.
- No multi-user concurrency guarantees or sophisticated recovery.
- Treat exported data and the data file as sensitive if records contain personal information.
