# The Gjallar Philosophy

**Gjallar sounds the warning; you stay free to choose.**

In the old story, Heimdall does not rule. He watches. When danger comes, he raises Gjallarhorn and sounds it so that everyone can see, understand and act. The horn gives no orders; it gives awareness.

That's the spirit of Gjallar. Security should make people freer, not smaller. A tool that protects you but traps you hasn't removed the danger; it has only changed its shape. So Gjallar is built around one belief: real security is freedom.

## The nine freedoms

1. **Freedom of choice.** No single tool should become your master. The things you depend on today can be replaced tomorrow, and nothing you have built or learned is lost when you do.
2. **Freedom of origin.** What you protect may live anywhere: big places, small places, public or private, online or cut off from the world. Protection shouldn't depend on where your work happens to sit.
3. **Freedom of approach.** People see, think and work in different ways. Security should meet each person where they are, and no single way of looking at the truth should be the only door.
4. **Freedom of knowledge.** What you learn about your own systems belongs to you. It should never be held hostage, hidden behind a price, or locked in a form only one party can read.
5. **Freedom of place.** Security should travel with you: to a small home setup, to a large organization, to places with no outside connection at all. No one should need permission from far away to protect what is theirs.
6. **Freedom of identity.** You decide who you trust and who may act. Authority comes from the people responsible, never from the tool. Nothing acting on someone's behalf should be able to do more than that person could.
7. **Freedom from noise.** A thousand alarms protect no one. A good guardian separates the real danger from the distant echo, says plainly why it matters, and lets people spend their attention where it counts.
8. **Freedom to decide.** The guardian advises; people judge. Every warning can be questioned, and every risk can be weighed and consciously accepted. When the guardian itself falters, it steps aside rather than standing in the way.
9. **Freedom for everyone.** Protection isn't a privilege for those who can pay the most. A small team, a school, a community group or a town office deserves the same clear warning as the largest enterprise. What helps society should be open to society.

## What we refuse

- **Chains:** no dependence that cannot be undone.
- **Mystery:** no judgment without a reason.
- **Fear:** we warn honestly; we never sell panic.
- **Secrecy:** nothing about you leaves your hands unless you choose to share it.

## In one breath

> **Security without chains.** See clearly, understand why, and stay free to choose. Gjallar sounds the horn when danger is real; what you do next is always yours.

---

## How Gjallar keeps each promise

| # | Freedom | In the code today |
|---|---|---|
| 1 | Choice | Hexagonal core; every engine (Syft, Grype, Grant, Copa, Trivy, OPA, cosign, Inspektor Gadget) is a subprocess behind a port; swap one adapter, keep the data and history |
| 2 | Origin | Syft sources (registry, Docker, containerd, OCI archive); discovery for Harbor **and any OCI Distribution registry**; offline DB mirror or a DB you build yourself ([gjallar-vunnel](https://github.com/heimdallr-dev/gjallar-vunnel)) |
| 3 | Approach | Web UI, REST, CLI, MCP for AI assistants, Arrow Flight SQL, Kyverno admission, chat notifications: all call the same use cases |
| 4 | Knowledge | Postgres, Parquet/DuckLake (direct attach), SBOMs as **CycloneDX and SPDX**, OpenVEX, Parquet export, Flight SQL; no format only Gjallar can read |
| 5 | Place | Laptop (`gjallar scan`), kind on WSL, homelab, air-gapped (mirrors for every download, see [network egress](operations.md#network-egress-what-leaves-your-network)), many clusters via NATS leaf nodes; agents connect outbound only |
| 6 | Identity | Any OIDC provider (Keycloak, Entra ID, Authentik, Dex, GitLab); roles and groups come from your IdP; namespaces per group (multi-tenancy); MCP forwards the caller's own token |
| 7 | Noise | Risk = CVSS × (KEV or EPSS) × runtime × exposure, with reasons on every finding; runtime reachability demotes packages that never load |
| 8 | Decide | Accept a risk with a reason (VEX); audit log of every human decision; Kyverno Audit by default, `failurePolicy: Ignore` everywhere |
| 9 | Everyone | Apache-2.0; static Go binaries; one-node profile (`values-kind.yaml`); signed, attested releases anyone can verify |

## Holding changes to it

Every pull request is checked against these freedoms (see
[CONTRIBUTING.md](https://github.com/heimdallr-dev/gjallar/blob/main/CONTRIBUTING.md)).
A change that adds a vendor-only feature ships with the open alternative, or
behind a port that the open alternative can implement. When a trade-off is
accepted anyway, it is written down where future readers will see it.
