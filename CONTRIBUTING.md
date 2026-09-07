# Contributing to the WeaveTab Ecosystem

> **Organization:** WeaveTab | **Engine:** Layer 0 Chrome DevTools Protocol | **Last Updated:** August 2026

Thank you for contributing to WeaveTab. We build high-performance, local-first Layer 0 browser control infrastructure for autonomous AI agents. We value clean code, deterministic mechanics, and zero-waste execution.

---

## Engineering Standards & Architecture Rules

All contributions across all WeaveTab repositories (`@weavetab/mcp`, `@weavetab/sdk`, `@weavetab/skills`, `Studio`, plugins) must adhere to these foundational principles:

1. **Sub-10ms IPC Dispatch**: WeaveTab commands the browser via direct CDP over local WebSocket. Do not introduce bloated abstractions, unnecessary intermediate event loops, or heavy third-party dependencies that degrade response times.
2. **Local-First & Zero Telemetry**: Every tool and package must operate fully offline on `127.0.0.1`. Never send analytics, user telemetry, or context snippets to remote services.
3. **Deterministic Mechanics**: Prefer deterministic CDP selectors, element refs, and native Input domain events over speculative heuristics or lossy screenshot-only guesswork.
4. **Single Source of Truth (No Doc Drift)**: Whenever a tool parameter, SDK method, or configuration option is modified, corresponding documentation in `/docs` and markdown files must be updated in lockstep. Speculative or hallucinated documentation is strictly forbidden.

---

## Development & Git Workflow

### 1. Branch Naming Convention

Create branches using structured prefixes:

- `feat/<feature-name>`: New tool, SDK method, or architectural capability.
- `fix/<issue-description>`: Bug fix or protocol correction.
- `perf/<optimization>`: Latency reduction or token pruning enhancement.
- `docs/<subject>`: Documentation, guides, or architectural decision updates.
- `chore/<task>`: Dependency maintenance, CI, or toolchain updates.

### 2. Commit Message Standards (Conventional Commits)

We enforce standard Conventional Commits:

```
<type>(<scope>): <short imperative description>

[optional body explaining motivation and mechanics]

[optional footer(s), e.g. Fixes #123]
```

**Types:**
- `feat`: New feature or tool
- `fix`: Bug fix
- `docs`: Documentation updates only
- `perf`: Performance or token-reduction improvements
- `refactor`: Code changes that neither fix a bug nor add a feature
- `test`: Adding or correcting tests
- `chore`: Build process, package updates, or repo tooling

**Example:**
```
feat(mcp): implement delta streaming for rapid dom change detection

Fixes #42
```

### 3. Pull Request Standards

- **Targeted Scope**: Keep PRs focused (<400 lines changed). Large multi-feature PRs will be requested to be split.
- **Verification**: Include exact terminal commands or scripts demonstrating local reproduction and verification against Chromium.
- **Testing**: Ensure all automated test suites pass cleanly before opening a pull request:
  ```bash
  npm test
  npm run verify
  ```
- **PR Template**: Complete all sections of the [Pull Request Template](.github/PULL_REQUEST_TEMPLATE.md).

---

## Tool & Plugin Authoring Guidelines

When authoring tools using `@weavetab/sdk` or modifying core tools in `@weavetab/mcp`:

1. **Strict Zod Schemas**: Every parameter must be explicitly validated with descriptive error messages.
2. **Predictable Return Payloads**: Handlers should return `{ success: true, ... }` or throw structured errors with actionable remediation advice.
3. **Secret Redaction**: Any tool accepting credentials must enforce Blind Injection protections and never log raw tokens.

---

## Reporting Issues & Feature Proposals

- **Bug Reports**: Open an issue using the [Bug Report Form](.github/ISSUE_TEMPLATE/bug_report.yml). Provide exact OS, Chromium engine version, and reproduction steps.
- **Proposals**: Open an issue using the [Feature Proposal Form](.github/ISSUE_TEMPLATE/feature_request.yml). Detail the exact protocol mechanics and latency impact.
- **Security Vulnerabilities**: Follow [SECURITY.md](SECURITY.md). Do not submit security vulnerabilities via public issues.
