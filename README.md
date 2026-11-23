# AFTERSTATE

Commitment accountability and recovery dashboard. Track commitment owners, due dates, priority, status, and transparent heuristic risk indicators.

## Run locally
Node.js 18+ required. No third-party packages. Run `node server.js`, then open http://localhost:3000.

## Safety boundary
Single-user local prototype. No auth/TLS; do not expose publicly. Data stored in `data.json`.

Features: CRUD records, search, status filter, risk score, summary metrics, activity log, JSON export API.