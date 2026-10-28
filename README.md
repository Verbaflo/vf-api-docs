# vf-api-docs

Public API reference for the **VerbaFlo Public API & Event Platform**, hosted on GitHub Pages at
**https://verbaflo.github.io/vf-api-docs/**.

This is a lightweight, zero-build static site:

| File | Role |
|---|---|
| `openapi.yaml` | OpenAPI 3.1 spec, **the single source of truth**. Everything else just renders it. |
| `index.html` | Renders `openapi.yaml` with [Scalar](https://github.com/scalar/scalar) (loaded from CDN). |
| `.github/workflows/pages.yml` | Publishes the site to GitHub Pages on every push to `main`. |
| `.nojekyll` | Serves files verbatim (no Jekyll processing). |

## Scope

Client-facing surface only: get an access token, create/read campaigns, read contact results,
fetch recordings, and the **webhook events** VerbaFlo delivers to client endpoints. Internal
provisioning/admin routes are intentionally not documented here.

## Edit

The spec is **authored from the shipped service code** (vf-webhook gateway, vf-auth-service,
vf-core_v2, vf-event-relay, config-model), not from a design doc. When a route or model changes
in those services, update `openapi.yaml` to match. It is hand-maintained, not generated.

## Preview locally

```bash
# any static server works; the page fetches ./openapi.yaml over HTTP
python3 -m http.server 8080
# open http://localhost:8080
```

## Validate

```bash
npx @redocly/cli lint openapi.yaml
```

## Deploy

Push to `main`. The GitHub Pages workflow publishes automatically. First-time setup:
enable **Settings → Pages → Source: GitHub Actions**. The site is then served at
`https://verbaflo.github.io/vf-api-docs/`.
