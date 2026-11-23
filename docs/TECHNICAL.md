# Technical notes

- Runtime: Node.js 18+, built-in modules only
- Server: HTTP API and static file serving
- Persistence: local JSON file, configurable through AFTERSTATE_DATA
- API: health, items CRUD, summary, events, export
- Client: plain HTML, CSS, JavaScript
- Automated integration tests: Node test runner
- CI: GitHub Actions on pushes and pull requests

## Boundaries

Single-user local prototype. No authentication, TLS, external service integration, or production hardening. Do not expose it publicly. Risk scoring is heuristic and should not be interpreted as prediction.
