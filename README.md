<div align="center">

```
██╗    ██╗███████╗ █████╗ ██╗   ██╗███████╗████████╗ █████╗ ██████╗ 
██║    ██║██╔════╝██╔══██╗██║   ██║██╔════╝╚══██╔══╝██╔══██╗██╔══██╗
██║ █╗ ██║█████╗  ███████║██║   ██║█████╗     ██║   ███████║██████╔╝
██║███╗██║██╔══╝  ██╔══██║╚██╗ ██╔╝██╔══╝     ██║   ██╔══██║██╔══██╗
╚███╔███╔╝███████╗██║  ██║ ╚████╔╝ ███████╗   ██║   ██║  ██║██████╔╝
 ╚══╝╚══╝ ╚══════╝╚═╝  ╚═╝  ╚═══╝  ╚══════╝   ╚═╝   ╚═╝  ╚═╝╚═════╝ 
```

### The Autonomous Browser Infrastructure for Enterprise AI Agents
**Deterministic Chrome DevTools Protocol &middot; Sub-10ms Local IPC &middot; Zero Cloud Telemetry &middot; Zero WebDriver Overhead**

<br/>

[![@weavetab/mcp](https://img.shields.io/npm/v/@weavetab/mcp.svg?style=flat-square&label=@weavetab/mcp&color=18181b)](https://www.npmjs.com/package/@weavetab/mcp)
[![@weavetab/sdk](https://img.shields.io/npm/v/@weavetab/sdk.svg?style=flat-square&label=@weavetab/sdk&color=18181b)](https://www.npmjs.com/package/@weavetab/sdk)
[![@weavetab/skills](https://img.shields.io/npm/v/@weavetab/skills.svg?style=flat-square&label=@weavetab/skills&color=18181b)](https://www.npmjs.com/package/@weavetab/skills)
[![Docs](https://img.shields.io/badge/docs-weavetab.dev-black?style=flat-square)](https://weavetab.dev/docs)

</div>

<br/>

---

## Executive Overview

**WeaveTab** is the foundational **Layer 0 interface** that connects autonomous artificial intelligence agents to live Chromium execution environments (Google Chrome, Microsoft Edge, Brave). 

Conventional agent automation architectures rely on heavy virtualization, brittle screenshot-loop latency, or cloud-hosted headless browsers that compromise user credentials and leak internal enterprise network surfaces. 

WeaveTab replaces this with a direct, multiplexed **Chrome DevTools Protocol (CDP)** engine bound strictly to local loopback (`127.0.0.1`). AI agents interact with the web through typed **Model Context Protocol (MCP)** tool definitions with sub-10ms dispatch, deterministic state awareness, and zero telemetry.

<br/>

## The WeaveTab Stack

```
┌────────────────────────────────────────────────────────────────────────┐
│                          AGENT RUNTIME LAYER                           │
│     Claude Desktop  │  Cursor  │  Cline  │  Antigravity  │  Custom LLM │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ Model Context Protocol (JSON-RPC)
┌───────────────────────────────────▼────────────────────────────────────┐
│                  WEAVETAB LAYER 0 CORE ENGINE (@weavetab/mcp)          │
│  ┌───────────────────────┬───────────────────────┬──────────────────┐  │
│  │   44+ MCP Toolset     │  Blind Injection      │  DOM Pruning &   │  │
│  │   (click, fill, eval) │  Secret Shield        │  Delta Streaming │  │
│  └───────────┬───────────┴───────────┬───────────┴──────────┬───────┘  │
│              │                       │                      │          │
│              │ Chrome DevTools       │ Local Chrome         │ Live CDP │
│              │ Protocol (WebSocket)  │ Extension API        │ Sessions │
└──────────────┼───────────────────────┼──────────────────────┼──────────┘
               │                       │                      │
┌──────────────▼───────────────────────▼──────────────────────▼──────────┐
│                      LOCAL CHROMIUM RUNTIME                            │
│           Google Chrome   │   Microsoft Edge   │   Brave               │
└────────────────────────────────────────────────────────────────────────┘
```

<br/>

## Ecosystem Packages & Repositories

| Repository / Package | Scope | Role & Description | Status |
|:---|:---|:---|:---|
| [`Weavetab/mcp`](https://github.com/Weavetab/mcp)<br/>`@weavetab/mcp` | Core Engine *(Private)* | High-performance MCP server translating agent intents into raw CDP instructions. Manages session lifecycles, DOM delta observers, and security policies. | `Production` |
| [`Weavetab/sdk`](https://github.com/Weavetab/sdk)<br/>`@weavetab/sdk` | Developer SDK *(Public)* | Strongly-typed TypeScript toolkit for building custom plugins, domain drivers, and isolated automation tools for the WeaveTab ecosystem. | `Production` |
| [`Weavetab/skills`](https://github.com/Weavetab/skills)<br/>`@weavetab/skills` | Operational Library *(Public)* | Reusable agent behavior patterns, extraction recipes, and multi-step workflows designed for minimal token consumption. | `Production` |
| [`Weavetab/Studio`](https://github.com/Weavetab/Studio) | Developer Tooling *(Public)* | Browser DevTools automation setup and test harness built natively around the Model Context Protocol. | `Active Dev` |
| [`Weavetab/exemple-plugin`](https://github.com/Weavetab/exemple-plugin) | Reference Plugin *(Public)* | Complete boilerplate demonstrating custom MCP tool authoring, lifecycle hooks, and typed schemas with `@weavetab/sdk`. | `Reference` |
| [`Weavetab/registry`](https://github.com/Weavetab/registry) | Verification *(Public)* | Index of verified community plugins, cryptographic hashes, and security sign-offs. | `Infrastructure` |

<br/>

## Architectural Tenets

### 1. Deterministic Layer 0 Execution
Agents do not guess clicks through lossy vision grids or fragile heuristic selectors. WeaveTab drives Chrome directly at the protocol level. Clicks dispatch through Chromium's native Input domain, scripts execute in exact isolated contexts, and DOM snapshots are pruned semantically to save 90%+ prompt tokens.

### 2. Blind Injection Security Architecture
Enterprise credentials never enter the agent's LLM context window. Through `browser_type_secret`, credentials resolve dynamically from local AES-protected keyrings directly into form inputs within the browser, replacing values with `[REDACTED]` tokens across all subsequent logs, DOM dumps, and debug artifacts.

### 3. Local-First Loopback Isolation
- Zero remote servers or telemetry collectors.
- All IPC traffic strictly restricted to `127.0.0.1`.
- Built-in domain access controls (`allow`, `read-only`, `deny`) and hard-blocked sensitive domains (banking consoles, IAM portals).

<br/>

## Quickstart

### Connect Any MCP-Compatible Agent

Run the server directly via `npx`:

```bash
npx -y @weavetab/mcp
```

Add to your MCP Client Configuration (`cline_mcp_settings.json`, Claude Desktop, or Antigravity):

```json
{
  "mcpServers": {
    "weavetab": {
      "command": "npx",
      "args": ["-y", "@weavetab/mcp"]
    }
  }
}
```

### Install the TypeScript SDK

For developers building custom plugins and domain tools:

```bash
npm install @weavetab/sdk
```

```typescript
import { definePlugin, ToolBuilder } from "@weavetab/sdk";

export default definePlugin({
  name: "custom-automation",
  version: "1.0.0",
  tools: [
    new ToolBuilder("extract_metrics")
      .description("Extract custom performance metrics from active tab")
      .handler(async ({ session }) => {
        const metrics = await session.send("Performance.getMetrics");
        return { success: true, metrics };
      })
  ]
});
```

<br/>

## Security & Governance

WeaveTab is built for environments where security is non-negotiable.

- **Vulnerability Disclosure**: Report security findings via private advisory or directly to `security@weavetab.pages.dev`. See [`SECURITY.md`](https://github.com/Weavetab/.github/blob/main/SECURITY.md).
- **Contributing**: All contributions follow strict conventional commits and surgical pull request workflows. See [`CONTRIBUTING.md`](https://github.com/Weavetab/.github/blob/main/CONTRIBUTING.md).
- **Architecture Decision Records**: Major architectural decisions are preserved in [`docs/decisions/`](https://github.com/Weavetab/.github/tree/main/docs/decisions).

<br/>

---

<div align="center">
<sub>&copy; WeaveTab Organization &middot; Engineered by <a href="https://github.com/fy2ne">@fy2ne</a> &middot; Built on Chrome DevTools Protocol</sub>
</div>
