# AFTERSTATE

A local-first commitment accountability dashboard. AFTERSTATE records commitments, exposes status and heuristic risk, and provides a recovery queue and activity history.

## Run

Requires Node.js 18+.

```sh
npm start
```

Open http://localhost:3000.

## Test

```sh
npm test
```

No third-party runtime dependencies.

## Capabilities

- Create, update, and delete commitment records
- Owner, deadline, priority and status tracking
- Search and status filtering
- Heuristic risk scoring and recovery queue
- Summary metrics and activity trail
- JSON export API
- Local JSON persistence

## API

| Endpoint | Method | Purpose |
|---|---|---|
| /api/health | GET | Health check |
| /api/items | GET | List/search/filter |
| /api/items | POST | Create record |
| /api/items/:id | PATCH | Update record |
| /api/items/:id | DELETE | Delete record |
| /api/summary | GET | Summary counts |
| /api/events | GET | Activity history |
| /api/export | GET | JSON export |

## Safety and scope

This is a local, single-user prototype—not a production service. It has no authentication or TLS. Keep it on your own machine; do not expose it to the public internet. Data is stored locally in `data.json` (override with `AFTERSTATE_DATA`). The risk score is a transparent heuristic, not a prediction or professional assessment.

## CI

GitHub Actions runs the Node test suite on pushes and pull requests to `main`.
