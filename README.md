<div align="center">

# Théo

**I build AI agent systems, pushing toward zero human intervention.**
Autonomous agents, MCP servers, and the guardrails that let them run with less and less supervision.

[![GitHub followers](https://img.shields.io/github/followers/Soyouse?style=flat&logo=github)](https://github.com/Soyouse)
[![X (Twitter)](https://img.shields.io/badge/X-%40SoyouseHQ-black?style=flat&logo=x)](https://x.com/SoyouseHQ)

</div>

---

### What I do

I design and ship systems where AI agents take on more of the loop over time — not by trusting the model more, but by engineering the boundary around it: mechanical guardrails, contract tests between components, fail-fast checks, and monitoring that catches drift before it becomes an incident.

Most of my work lives in **MCP (Model Context Protocol) servers** — thin, typed bridges between AI agents and real systems (infra, comms, CRM, social, media) — built to be driven by an agent as reliably as a human drives a UI.

### How I work

- **Scientific method before code.** Hypothesis → measurement → root cause → targeted fix. A failed attempt means going back to measurement, not trying something else blind.
- **Zero technical debt, built scalable from the start.** No shortcuts I'll have to retrofit later — infrastructure that's expensive to redo is built right the first time.
- **Anti-regression by contract, not just by incident.** Every boundary between components gets a contract test *before* it breaks, not just after — bugs get a red test first, then the fix.
- **CI that never blocks.** Fast local feedback (watch mode), heavier verification (mutation testing, full suite) runs async in CI — never in the way of shipping.
- **No flattery, ever.** I want the real state of a system, including when it's bad.

### Selected projects

| | |
|---|---|
| **[reddit-mcp](https://github.com/Soyouse/reddit-mcp)** | Home-built MCP server for driving Reddit accounts through the official OAuth Data API — multi-account, with a dedicated anti-spam / anti-manipulation safety layer (throttling, vote-guarding, warmup gating) as the core value, not an afterthought. |
| **[memory-engine](https://github.com/Soyouse/memory-engine)** | Semantic memory system for AI agents — persistent recall across sessions. |

### Stack

`Node.js` · `TypeScript` · `MCP` · `Docker` · `Vitest` / `Stryker` (mutation testing) · `GitHub Actions`

---

<div align="center">
<sub>Building for a future where agents run the loop, not just answer questions in it.</sub>
</div>
