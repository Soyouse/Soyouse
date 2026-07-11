<div align="center">

# Soyouse

**I build AI-agent systems that run themselves — pushing toward zero human intervention.**
Autonomous agents, a dozen home-built MCP servers, and the formal guardrails that let them operate with less and less supervision.

*A one-person operation, with AI in the loop — not a team behind these.*

[![GitHub followers](https://img.shields.io/github/followers/Soyouse?style=flat&logo=github)](https://github.com/Soyouse)
[![X (Twitter)](https://img.shields.io/badge/X-%40SoyouseHQ-black?style=flat&logo=x)](https://x.com/SoyouseHQ)

</div>

---

### What I do

I design and ship systems where AI agents take on more of the loop over time — not by trusting the model more, but by **engineering the boundary around it**: mechanical guardrails, contract tests between components, formal specs where concurrency is real, static coupling detection, and production canaries that catch drift before it becomes an incident.

The rule underneath all of it: **the LLM proposes, a deterministic machine gives the verdict — never the other way around.** The only non-deterministic input I allow is the invariant itself (human instinct); everything downstream is decided by a machine.

Most of my work lives in **MCP (Model Context Protocol) servers** — thin, typed bridges between AI agents and real systems (infra, comms, CRM, social, media, prospecting) — each built to be driven by an agent as reliably as a human drives a UI. They run a real business end to end.

### The thesis: an assurance ladder matched to what can be proven

This is the part most solo builders never touch. Every kind of code gets the strongest verification that *fits* it:

| Code shape | Verification |
|---|---|
| Pure logic, strong invariant | **Property-based tests** (`fast-check`) + **mutation gates** (`Stryker`, ratcheted — the threshold only ever goes up) |
| Non-serialized concurrency (daemons, queues, locks, shared mutable state) | **`TLA+` spec + trace validation** — TLC proves the plan, a trace anchors code to plan, and a **mandatory negative-check** kills hollow specs (because the spec was written by an LLM) |
| Every boundary between components | **Contract test sealed *before* the first incident**, not after — shape *and* orchestration |
| Residual I/O that can't be unit-tested | **Production canaries** — best-effort, non-blocking, they page me on drift |
| Any multi-file project | **Static coupling detection** — `dependency-cruiser` (imports/boundaries) + `jscpd` (duplicated literals/paths) + shared types (`tsc` as impact analysis). Implicit coupling is enemy #1. |

Decision logic is always isolated from I/O (pure functions) so it stays testable and mutable. Bugs get a **red test first**, then the fix. CI runs async and **never blocks a push** — heavy verification (mutation, full suite) happens off the critical path. GitHub is a bonus, **never a production dependency**: everything runs locally too.

### What I've built

**🔌 A dozen+ MCP servers** — each a raw, concurrency-hardened bridge to a real system:

| | |
|---|---|
| **infra** | Deploy, off-box builds, DNS, SEO, blog, booking, forms, analytics — the control plane for a fleet of client sites |
| **prospection** | French government-API pipeline + site detection + lead scoring — the agency's growth engine (**629 tests**, ratcheted mutation gate) |
| **[reddit](https://github.com/Soyouse/reddit-mcp)** | Multi-account Reddit over the official OAuth API, with an anti-spam / anti-manipulation **safety layer as the core value** (throttle, vote-guard, warmup gating) |
| **[discord](https://github.com/Soyouse/discord-mcp)** | Multi-bot Discord + a two-container Postgres history relay + a **sister React web client** (live over Socket.IO) on the same core |
| **[publer](https://github.com/Soyouse/publer-mcp)** | Multi-workspace social scheduling, concurrent-session safe |
| **[media](https://github.com/Soyouse/media-mcp)** | AI image & video generation via a **swappable** backend (xAI/Grok default) — the visual hands of the social agent |
| **odoo** | Guarded Odoo CRM — post-write readback, duplicate-send/-invoice guards, ID-provenance hook, billing canary. Published open-source. |
| **+ more** | gworkspace, umami (analytics), browser automation, SSH, blog, QA-SEO — all agent-driven |

**🤖 Autonomous agents in production**
- A **0-human social agent** posting on a real schedule (3×/week + Sunday), gated by a vision check before anything ships — **248 tests**, running unattended on a VPS.
- A **Stop-gate** hook that enforces *proof-before-done*: an agent can't mark work complete without evidence it actually ran.

**⚙️ Custom engines, built from scratch**
- **[memory-engine](https://github.com/Soyouse/memory-engine)** — 100% local, compaction-aware semantic memory for AI agents: GPU embeddings (`Qwen3-Embedding` via `llama.cpp`) + hybrid `BM25 + RRF` recall, auto-reindexing. Published as a plugin.
- **wz-design-engine** — spec-driven website generation with a **self-repair loop** (a `SubagentStop` hook that catches warnings and re-runs until clean) — **380 tests**, mutation ~81.
- **svg-core** — deterministic SVG → PNG rendering (Resvg + Yoga layout), single-call, seek-safe.
- A **video pipeline** on HyperFrames — HTML compositions rendered by a worker.

**🧠 Deep on the harness itself, not just prompting it**
Custom **hooks** (SessionStart, PreCompact, PreToolUse doc-injection, Stop-gates), a **self-updating semantic memory system** with auto-reindexing, **35 authored skills**, **plugin/skill development**, protected-path guardrails, and a dozen home-built MCP servers wired in as the daily driver.

**🏗️ The infrastructure it all runs on**
A **Tailscale mesh across 8 machines**, 3 VPS (dev / prod / proxy), an **off-box build system** (pull-based, 3 builders, sha256 OCI digests, on-box fallback), a **fail-fast deploy dispatcher** that provably refuses bad state, immutable-infra discipline (twelve-factor, single-source writable paths sealed by a static drift-test).

### How I work

- **Scientific method before code.** Hypothesis → measurement → root cause → targeted fix. A failed attempt means going back to measurement, not trying something else blind.
- **Zero technical debt, scalable from the start.** No shortcut I'll have to retrofit — anything expensive to redo is built right the first time.
- **Operator scaling law.** Zero-human is an open experiment: I only scale when the number of instinct/surface decisions *decreases*. An instinct I hit twice at the same door gets frozen into a gate. Self-hosted standards over homegrown; compose over accumulate.
- **No flattery, ever.** I want the real state of a system, including — especially — when it's bad.

### Stack

**Languages & runtime**
`Node.js` · `TypeScript` · `Python` · `C++` (native STT/TTS bindings) · `Bash`

**AI / ML**
`Claude` · `MCP` · `OpenClaw` (persistent agent runtime) · `OpenAI` · `xAI Grok (Aurora)` · `Gemini` · `Whisper` (STT) · `Kyutai TTS` · `Qwen3-Embedding` (local GPU) · `llama.cpp` · `ONNX Runtime` · `BM25 + RRF hybrid semantic search`

**Verification & formal methods**
`TLA+` / TLC (model checking + trace validation) · `fast-check` (property-based) · `Stryker` (mutation, ratcheted) · `dependency-cruiser` + `jscpd` (implicit-coupling detection) · `Vitest` · `node:test` · `Playwright` · `Pytest`

**Monitoring & observability**
`Uptime Kuma` (watchdog) · `ntfy` (alerting) · production **canary** checks (best-effort, non-blocking) · append-only JSONL run journals

**Web & backend**
`Next.js` · `React` · `Fastify` · `Express` · `Prisma` · `Zod` · `Socket.IO` · `Tailwind`

**Data**
`PostgreSQL` · `DuckDB` · `SQLite`

**Infra, CI & deploy**
`Docker` · `Nginx` · `Tailscale` · `Cloudflare` · `systemd` · `pnpm` / `Turbo` monorepo · `GitHub Actions` (async, never blocking) · `Husky`

**Custom engines**
`memory-engine` (local semantic recall) · `svg-core` (deterministic SVG→PNG) · `wz-design-engine` (spec-driven, self-repairing) · HyperFrames video pipeline

---

<div align="center">
<sub>Building for a future where agents run the loop, not just answer questions in it.</sub>
</div>
