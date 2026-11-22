---
name: gjallar-contributing
description: Rules for changing Gjallar's code, chart, policies or docs across the heimdallr-dev repositories. Use before writing or reviewing any change to gjallar, gjallar-helm, gjallar-opa, gjallar-docs, gjallar-grafana, gjallar-analytics, gjallar-vunnel, gjallar-mcp or gjallar-e2e.
---

# Contributing to Gjallar

Check every change against the gjallar-philosophy skill first. Then follow
these rules, which are how the codebase keeps its promises.

## Which repository

| Change | Repo |
|---|---|
| Go code: services, CLI, web UI, adapters, Dockerfile, `make e2e` | `gjallar` |
| Helm chart, Kyverno policies, Keycloak realm | `gjallar-helm` |
| Rego for OPA / Conftest / Gatekeeper, CI gate | `gjallar-opa` |
| Documentation (MkDocs) | `gjallar-docs` |
| Dashboards, alert rules | `gjallar-grafana` (copy the dashboard into the chart) |
| Notebooks, SQL reports, client examples | `gjallar-analytics` |
| Self-built Grype DB | `gjallar-vunnel` (fork; never edit upstream files, only `gjallar/`) |
| AI client setup | `gjallar-mcp` |
| Cluster e2e (kind, Playwright) | `gjallar-e2e` |
| Skills like this one | `gjallar-skills` |

A behaviour change usually touches the core, the chart and the docs together.

## Code rules (gjallar)

- **Layers:** `internal/domain` imports nothing from Gjallar; `internal/app`
  imports only the domain and defines ports (interfaces); `internal/adapters`
  implement ports; `cmd/*` wires them. New engines are new adapters.
- **Engines are subprocesses** (Syft, Grype, Grant, Copa, Trivy, OPA, cosign,
  kubectl-gadget), run through `scanner.ExecRunner`, which also meters them and
  disables update checks.
- **No new dependency** when the standard library or an existing one does the
  job. Dependencies are vendored (`go mod vendor`).
- **Every download is pinned and verified** against the publisher's checksum,
  in the Dockerfile and in CI. Never `curl | sh` from a branch. Pin GitHub
  Actions by commit SHA. Prefer releases at least two weeks old.
- **Fail open** for admission and anything on the request path of a cluster
  (`failurePolicy: Ignore`, Audit by default).
- **Every score has reasons**; add one when you add an input.
- **Tenancy**: any new read endpoint filters by the caller's scope
  (`a.scope(r)`); any new write is admin-only and is audit-logged automatically.
- **No network call the user didn't ask for.** New outbound connections go in
  the "Network egress" table in the operations guide, with a mirror option.

## Checks before you finish

```bash
gofmt -l cmd internal test        # must print nothing
go vet ./... && go test ./...
make e2e                          # or BUILDER=nerdctl GJALLAR_E2E_PORT=28080
helm lint charts/gjallar          # in gjallar-helm
opa test policy                   # in gjallar-opa
mkdocs build --strict             # in gjallar-docs
```

New non-trivial logic gets a test. Bugs get a regression test that fails
without the fix.

## Commits

Sign off (DCO): `git commit -s`. One topic per change, message says why.
Security issues go through private reporting (SECURITY.md), never an issue.
