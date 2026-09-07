# WeaveTab Organization Security Policy

> **Organization:** WeaveTab | **Engine:** Layer 0 Chrome DevTools Protocol | **Last Updated:** August 2026

WeaveTab is built for mission-critical and enterprise environments where privacy, deterministic execution, and local containment are mandatory. This document outlines our threat model, defensive architecture, and responsible vulnerability disclosure process across all repositories within the WeaveTab organization.

---

## Supported Packages & Versions

Only active major release lines receive security updates. Operators and developers must keep installations current.

| Package / Repository | Branch / Major | Supported | Status |
|:---|:---|:---|:---|
| `@weavetab/mcp` | `main` (2.x) | Yes | Current Core Engine |
| `@weavetab/sdk` | `main` (2.x) | Yes | Current Plugin SDK |
| `@weavetab/skills` | `main` (2.x) | Yes | Current Operational Skills |
| Legacy (`@fy2ne/weavetab`, `< 2.0.0`) | Deprecated | No | End of Life |

---

## Architectural Security Model

WeaveTab interacts directly with local Chromium browser instances (Google Chrome, Microsoft Edge, Brave) via the Chrome DevTools Protocol (CDP). Because it commands the browser at the operating system level, WeaveTab operates at a privileged interface (**Layer 0**).

### Core Security Guarantees

| Guarantee | Technical Implementation | Purpose |
|:---|:---|:---|
| **Localhost Isolation** | WebSocket CDP servers and IPC transports bind strictly to `127.0.0.1`. | Prevents remote network exposure or external connection attempts. |
| **Zero Cloud Telemetry** | Zero external analytics, tracking, or telemetry pings. | Ensures zero prompt, DOM, or action data leaves the local machine. |
| **Domain Policy Engine** | Per-domain enforcement rules (`allow`, `read-only`, `deny`). | Prevents autonomous agents from accessing IAM portals, cloud consoles, or banking domains. |
| **Blind Injection** | Credentials injected via `browser_type_secret` resolve directly from local secure stores. | Prevents LLM context windows, logs, and DOM snapshots from echoing credentials. Values are masked as `[REDACTED]`. |
| **DOM Tree Pruning & Filtering** | Semantic stripping of malicious input patterns, invisible characters, and prompt injection traps. | Defends against indirect prompt injection embedded within hostile web pages. |
| **Path Traversal Defenses** | Strict normalization and rejection of `..` paths across profiles, downloads, and storage dumps. | Prevents directory escape vulnerabilities. |

---

## Responsible Vulnerability Disclosure

If you discover a security vulnerability within any WeaveTab repository, package, or tool, do **not** open a public issue.

### Disclosure Channels

1. **GitHub Private Security Advisory (Preferred)**:
   Submit a private advisory via [GitHub Security Advisories](https://github.com/Weavetab/.github/security/advisories/new).
2. **Direct Security Inbox**:
   Email detailed findings to **`security@weavetab.pages.dev`**.

### What to Include

- Clear description of the vulnerability and potential attack vector.
- Affected packages and versions.
- Minimal, deterministic Proof-of-Concept (script, cURL, or reproduction steps).
- Expected vs. observed impact.

### Response Timelines

| Stage | SLA | Action |
|:---|:---|:---|
| **Acknowledgment** | **48 Hours** | Confirmation of receipt by core maintainers. |
| **Assessment** | **7 Days** | Severity classification and attack surface reproduction. |
| **Resolution** | **30 Days** | Emergency patch build and synchronized NPM / GitHub release. |

---

## Maintainer Security Contacts

- **Security Reports**: `security@weavetab.pages.dev`
- **Security Advisories**: https://github.com/Weavetab/.github/security/advisories

Public disclosure of vulnerabilities before coordinated disclosure with maintainers is strictly prohibited.
