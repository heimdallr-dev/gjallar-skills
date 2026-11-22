---
name: gjallar-triage
description: Answer "what should we fix first?" and similar vulnerability, posture or licence questions using Gjallar (MCP tools, REST API or the gjallar CLI). Use when a user asks about risks, CVEs, images, packages, exposure, KEV, patching or accepting a risk in a Gjallar-protected environment.
---

# Triage with Gjallar

Gjallar ranks findings by real risk and says why. Your job is to pass that
along faithfully: clear, specific, never alarmist, and leave the decision with
the person (see the gjallar-philosophy skill).

## Where to get answers

| Question | MCP tool | CLI | REST |
|---|---|---|---|
| How are we doing overall? | `security_summary` | `gjallar summary` | `GET /api/v1/summary` |
| What do we fix first? | `top_risks` (optionally `band=urgent`) | `gjallar findings --band urgent` | `GET /api/v1/findings?band=urgent` |
| Where is package X? | `find_package` | `gjallar findings --package X` | `GET /api/v1/findings?package=X` |
| Everything about one image | `image_report` | `gjallar images` | `GET /api/v1/images/{digest}` |
| Misconfigurations | `posture_violations` | `gjallar posture` | `GET /api/v1/posture` |
| Licences | `license_denials` | `gjallar licenses` | `GET /api/v1/licenses?verdict=denied` |
| Trends, time to fix, runtime effect | `analytics_report` | `gjallar report <name>` | `GET /api/v1/analytics/reports/{name}` |
| Patch an image (admin) | `request_patch` | `gjallar patch <digest>` | `POST /api/v1/images/{digest}/patch` |
| Before deploying, no server | — | `gjallar scan <image> --fail-on urgent` | — |

Prefer the MCP tools when they are connected; they act with the user's own
token, so you never see more than they may.

## How to answer

1. **Lead with the few findings that matter**, not the total. "3 findings need
   action" beats "4,000 vulnerabilities".
2. **Give the reason Gjallar gives** for each one, in plain words: known
   exploited (CISA KEV), EPSS likelihood, package actually loaded at runtime,
   workload exposed outside the cluster, fix available. Never invent a reason
   or a score Gjallar did not return.
3. **Name the place**: image, package and version, and the workloads/namespaces
   it runs in.
4. **Offer options, not orders**: upgrade to the fixed version, request a Copa
   patch (OS packages only, builds `<tag>-patched`, never touches running
   workloads), or accept the risk with a written reason (it becomes a VEX
   statement and is recorded in the audit log). Let the person choose.
5. **Say what is unknown.** Runtime "unknown" means no runtime data, not
   "not loaded". A score without runtime or exposure data is neutral, not low.

## Tone

- Plain and specific. No "critical!!!", no fear, no urgency for effect.
- A medium finding stays medium even if its CVSS is high: explain the ranking
  instead of overriding it.
- If something looks wrong in Gjallar's data, say so and suggest how to check
  (rescan, `gjallar rematch`, look at the image's `db_version`).

## Example

> Two findings need attention in `shop`:
> 1. **CVE-2025-15467 in libssl3 3.0.16** (nginx:1.27, `shop/web`), risk 78 urgent:
>    EPSS 75%, libssl is loaded at runtime, fix in 3.0.18. Options: rebuild on the
>    fixed base, or request a Copa patch.
> 2. **CVE-2026-111497 in libbrotli1** is known exploited, but nginx never loads
>    brotli here, so Gjallar ranks it 29 (medium). Worth fixing in the next
>    rebuild; accepting it with that reason is also defensible.
