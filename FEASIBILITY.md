# FEASIBILITY RANKING

> **Weighted Priority Order (High → Low)**
> 1. Faster Development & Completion — **40%**
> 2. Actual Industry Use Case — **30%**
> 3. SDLC Simulation — **20%**
> 4. Resume Value — **10%**

> **Context:** 4th-year engineering student · 1-month build window · Coding agents used for implementation

---

## Scoring Scale

| Score | Meaning |
|-------|---------|
| 5 | Exceptional on this dimension |
| 4 | Strong |
| 3 | Adequate |
| 2 | Weak |
| 1 | Poor / disqualifying |

**Weighted Score = (Dev × 0.40) + (Use Case × 0.30) + (SDLC × 0.20) + (Resume × 0.10)**

---

## Ranked Summary Table

| Rank | Idea | Dev Speed | Industry Use Case | SDLC | Resume | **Weighted Score** |
|------|------|-----------|-------------------|------|--------|--------------------|
| 🥇 1 | IDEA-006 — LLMOps Gateway | 5 | 5 | 5 | 5 | **5.00** |
| 🥈 2 | IDEA-003 — AI Chief-of-Staff | 4 | 5 | 5 | 5 | **4.60** |
| 🥉 3 | IDEA-004 — Project Memory | 4 | 5 | 4 | 5 | **4.40** |
| 4 | IDEA-007 — Multi-Agent Research | 4 | 4 | 5 | 5 | **4.30** |
| 5 | IDEA-005 — Incident Intelligence | 3 | 5 | 5 | 5 | **4.20** |
| 6 | IDEA-001 — Workspace Helper | 4 | 2 | 3 | 2 | **3.00** |
| 7 | IDEA-002 — FlowForge | 1 | 3 | 5 | 4 | **2.70** |

---

## 🥇 Rank 1 — IDEA-006: LLMOps Gateway

**Weighted Score: 5.00 / 5.00**

| Dimension | Score | Rationale |
|-----------|-------|-----------|
| Dev Speed | **5 / 5** | Most modular architecture of all ideas. Every feature (proxy, logging, caching, guardrails, dashboard) is independently shippable — cutting any one still leaves a complete product. HTTP proxy patterns and OpenAI API mirroring are maximally well-understood by coding agents, meaning near-zero implementation debugging. A fully working v1 with semantic cache is achievable by end of Week 2. |
| Industry Use Case | **5 / 5** | Every team shipping AI products faces uncontrolled LLM costs, zero prompt observability, and no version control for prompts. The self-hosted angle targets the real gap: Helicone, LangSmith, and PortKey are cloud-only SaaS. Enterprises with HIPAA, SOC 2, or GDPR requirements cannot use them. Demand is immediate and universal across the AI engineering market. |
| SDLC Simulation | **5 / 5** | Full SDLC cycle is naturally present: API protocol design (OpenAI-compatible surface), data modeling (log schema, prompt schema, cost model), middleware pipeline architecture, integration testing (does the downstream app still work through the proxy?), performance testing (proxy latency overhead), Docker Compose deployment, and user-facing documentation (how to point an existing app to the gateway). |
| Resume Value | **5 / 5** | "I built a self-hosted LLM gateway with semantic caching, prompt version control, and guardrails" communicates infrastructure-level thinking, not just prompt engineering. Directly maps to AI platform engineering roles at companies shipping AI products. |

**Key Demo Moment:** Two API calls side by side — direct OpenAI (800ms, $0.002) vs. gateway with semantic cache hit (4ms, $0.00). Dashboard shows real-time savings. Quantifiable, immediate, universally impressive to anyone who has paid an LLM bill.

**Scope Discipline:** Add features in this order and stop when time runs short — (1) proxy + logging, (2) semantic cache, (3) prompt registry, (4) budget enforcement, (5) guardrails. Every stopping point is a complete product.

---

## 🥈 Rank 2 — IDEA-003: Personal AI Chief-of-Staff

**Weighted Score: 4.60 / 5.00**

| Dimension | Score | Rationale |
|-----------|-------|-----------|
| Dev Speed | **4 / 5** | The WhatsApp-first MVP (goals + reminders + 2-3 specialized agents + persistent memory) is achievable in 4 weeks. Integration risk is the main threat — each external service (WhatsApp API, GitHub, Gmail, Calendar) introduces unexpected debugging. Must limit to 3 integrations maximum and finish them completely before adding a fourth. |
| Industry Use Case | **5 / 5** | Fragmented tools, broken follow-through, and information overload are universal pains for every developer and knowledge worker. The accountability engine (planned vs. actual behavior comparison) and learning agent combination does not exist as a well-implemented product. The multi-channel access (WhatsApp + web) makes it usable, not just a demo. |
| SDLC Simulation | **5 / 5** | Requires clear requirements analysis (what does the user actually need vs. want?), data modeling (goal/task/memory schema), agent orchestration architecture design, testing agent behavior under different user inputs, handling async execution (queues + workers), and multi-channel deployment. Full SDLC is naturally covered. |
| Resume Value | **5 / 5** | "I built a persistent personal agentic operating system with multi-agent orchestration, persistent memory, and proactive goal tracking via WhatsApp" is a top-tier portfolio statement in 2025-2026 AI engineering hiring. Agent orchestration, persistent memory design, and HITL approvals are exactly the skills senior AI engineers interview for. |

**Key Demo Moment:** Send a WhatsApp message: "I want to finish my authentication module today." Assistant breaks it into tasks, checks GitHub progress at end of day, sends accountability check: "You planned 2 hours on auth — GitHub shows 30 minutes of commits. Still on track?" Live and functional, not a slideshow.

**Scope Discipline:** Pick these 3 integrations only — WhatsApp (Twilio) + GitHub + one of (Gmail or News digest). Do not add Calendar, Notion, or browser integration in Month 1. The orchestration and memory architecture are the impressive parts, not the number of integrations.

---

## 🥉 Rank 3 — IDEA-004: Project Memory

**Weighted Score: 4.40 / 5.00**

| Dimension | Score | Rationale |
|-----------|-------|-----------|
| Dev Speed | **4 / 5** | The RAG-over-codebase pipeline is well-understood and heavily covered in coding agent training data. GitHub API client, chunking strategy, embedding generation, vector storage, and RAG chain are all achievable with minimal debugging. Git history parsing (commits, PRs, issues) requires careful schema design but the implementation is straightforward. Achievable MVP by end of Week 3 with polished UI in Week 4. |
| Industry Use Case | **5 / 5** | Every developer who has joined a large codebase has felt the pain of understanding not just what the code does but why decisions were made. The "why" layer — linking code to Git history, PR discussions, and past failures — is a genuine, unsolved problem at scale. Developer tooling with AI is one of the fastest-growing market segments. |
| SDLC Simulation | **4 / 5** | Good coverage: ingestion pipeline design, data modeling (how to represent code + history relationships for retrieval), chunking and embedding strategy decisions, RAG evaluation (are answers accurate and cited?), web UI, and deployment. Slightly weaker than top-ranked ideas because the testing strategy (evaluating RAG answer quality) is more subjective and less structured than protocol testing or integration testing. |
| Resume Value | **5 / 5** | Directly maps to Sourcegraph, GitHub Copilot, Cursor, and AI developer tooling roles. "I built an AI that answers why questions about codebases using RAG over code, commits, and PR history with direct citations" demonstrates RAG depth, code analysis thinking, and developer empathy — all highly valued. |

**Key Demo Moment:** Connect a real GitHub repository (ideally a well-known open source project or your own project). Ask: "Why does this function use 3 retries?" — system answers with a citation to the specific PR discussion where the decision was made. Ask: "What will break if I change this database schema?" — system lists affected files, APIs, and tests with file links. Live with a real repo, not mocked data.

**Scope Discipline:** Do not build a knowledge graph. The impressive version uses a knowledge graph for relationship traversal — but it's a research problem in 1 month. Ship: GitHub API → chunking → embeddings → RAG → citation UI. That alone is exceptional and fully achievable.

---

## Rank 4 — IDEA-007: Multi-Agent Deep Research Engine

**Weighted Score: 4.30 / 5.00**

| Dimension | Score | Rationale |
|-----------|-------|-----------|
| Dev Speed | **4 / 5** | The core (Navigator + 2-3 parallel Web Research Agents + Synthesis Agent) is achievable in 2 weeks. The risk is web scraping reliability — rate limiting, content variation, and paywalled content cause unpredictable debugging time. This risk is eliminated by using a managed scraping API (Firecrawl or Jina Reader) instead of writing raw scrapers. With that mitigation in place, development speed is high. |
| Industry Use Case | **4 / 5** | Strong for knowledge workers, researchers, consultants, and analysts. Slightly less universal than IDEA-006 or IDEA-005 — not every developer encounters the "deep research" need daily, whereas every developer encounters LLM costs or production incidents. The self-hosted positioning is compelling for enterprises that cannot use Google Deep Research. |
| SDLC Simulation | **5 / 5** | Outstanding SDLC coverage: agent protocol design (how agents communicate results back to Navigator), parallelism model (queue-based vs. async/await), state management across a multi-step agent pipeline, testing agent behavior (does the Critic loop actually improve output?), streaming architecture (real-time report generation visible to user), quality evaluation, and deployment. |
| Resume Value | **5 / 5** | Multi-agent orchestration with real coordination logic (Navigator → parallel dispatch → Fact-Check → Critic → re-dispatch → Synthesis) is the most frontier-adjacent skill in applied AI engineering. Almost no portfolio projects implement a genuine critic-and-replan loop. This is the most differentiated architecture of all seven ideas. |

**Key Demo Moment:** Submit a complex technical question live. Show the Navigator decomposing it into sub-questions. Show parallel agents running simultaneously in real time (streaming UI). Show the Critic identifying a gap and triggering a second research pass. Show the final structured document with confidence-tagged claims and inline citations. The streaming real-time generation is visually compelling.

**Scope Discipline:** Use Firecrawl or Jina Reader for web scraping — not raw scrapers. Start with web-only agents; Paper Analysis agent (arXiv) is phase 2. Implement the Critic loop only after Navigator + Web Agents + Synthesis are fully working. The streaming UI (real-time report generation) is the highest-impact demo feature — prioritise it over agent count.

---

## Rank 5 — IDEA-005: AI Production Incident Intelligence

**Weighted Score: 4.20 / 5.00**

| Dimension | Score | Rationale |
|-----------|-------|-----------|
| Dev Speed | **3 / 5** | The pipeline design is clear, but testing requires realistic incidents. Building real infrastructure (a deployed app with Prometheus + Grafana generating real alerts) or building convincing mock incident data is itself a significant Week 1 task. The HITL remediation layer (actual kubectl rollback execution) is unlikely to be production-ready in 1 month — must be simulated in the demo. This is the primary reason for lower development speed score despite a clear architecture. |
| Industry Use Case | **5 / 5** | Production downtime is directly expensive. Every engineering team running production systems has this pain. The AI-native cross-signal correlation layer (logs + metrics + traces + commits + past incident history simultaneously) does not exist as a well-implemented open product. Enterprise MTTR reduction has immediate, measurable ROI — making sales conversations short. |
| SDLC Simulation | **5 / 5** | Excellent SDLC coverage: ingestion pipeline design (multi-source pull, normalization), incident data modeling, correlation algorithm design, testing with simulated incidents (requires designing realistic test scenarios), Slack bot integration, HITL approval flow design, post-mortem template design, deployment, and operational runbook. |
| Resume Value | **5 / 5** | SRE + AI is one of the highest-value intersections in platform engineering. "I built an AI system that compresses incident MTTR from 90 minutes to 60 seconds through automated cross-signal correlation" is a quantified, enterprise-credible portfolio claim. Maps directly to platform engineering, SRE, and DevOps roles at any company running production systems. |

**Key Demo Moment:** Trigger a simulated incident (or deliberately break a running service). Show the alert webhook received. Show the context ingestion (logs + metrics + recent commit). Show the AI-generated hypothesis ranking with evidence. Show the Slack notification with runbook. Show the approve button for the remediation action. Show the auto-generated post-mortem draft. The entire flow in under 2 minutes.

**Scope Discipline:** Accept that remediation execution will be simulated in the demo. Focus effort on making the correlation quality genuinely good — that is the value proposition, not kubectl execution. A realistic simulated incident scenario (with scripted log patterns and metric anomalies) is sufficient for a compelling demo.

---

## Rank 6 — IDEA-001: Real-Time Workspace Helper

**Weighted Score: 3.00 / 5.00**

| Dimension | Score | Rationale |
|-----------|-------|-----------|
| Dev Speed | **4 / 5** | The scope is naturally bounded and an Electron or Tauri app can be built reasonably fast. Coding agents handle the UI, local storage, and LLM integration. However, OS-level APIs (process monitoring, window tracking, file watching with permissions) are platform-specific, poorly documented, and differ significantly across Windows, macOS, and Linux — this introduces debugging time that agents cannot help with. |
| Industry Use Case | **2 / 5** | Desktop productivity tools are a niche category. The target user exists but the problem is less acute than production incidents or LLM cost unpredictability. Many similar tools exist (Raycast, Warp AI, clipboard managers, various AI sidekicks). Without a genuinely novel AI behaviour, this is a utility app competing in a crowded space. |
| SDLC Simulation | **3 / 5** | Requirements are simple and well-defined. Architecture is straightforward (desktop app + local LLM). Testing is mostly manual (does the reminder fire? does the file watcher work?). Deployment is a binary release — simple. The SDLC simulation is thinner than ideas requiring API design, pipeline architecture, or multi-service coordination. |
| Resume Value | **2 / 5** | "I built a desktop AI task manager" is the weakest possible portfolio statement for backend, AI engineering, or platform roles. The technical depth (Ollama integration, file watchers) is real but not visible from the project description alone. Hiring managers reviewing a 3-minute portfolio walkthrough will not be impressed unless the intelligence layer produces remarkable results. |

**Recommendation:** Best absorbed as the Desktop Intelligence component within IDEA-003 (AI Chief-of-Staff), where it becomes one of several tools the agent uses to observe actual developer behaviour — rather than a standalone product.

---

## Rank 7 — IDEA-002: FlowForge

**Weighted Score: 2.70 / 5.00**

| Dimension | Score | Rationale |
|-----------|-------|-----------|
| Dev Speed | **1 / 5** | The 1-month version is inevitably a basic CRUD application. The interesting architecture — Kafka, microservices, WebSockets at scale, AI agents operating the platform through MCP — begins at phase 3 or 4 of a multi-month plan. With coding agents handling the boilerplate, you might finish a slightly more polished CRUD app, but you still won't reach the distributed or AI layers that justify building this in the first place. |
| Industry Use Case | **3 / 5** | The market exists (project management is universal) but is extremely crowded — Linear, Jira, Asana, Monday, Notion all compete here. Without the AI-agent differentiation (which requires months to reach), there is no compelling reason for a user to choose this over established tools. The AI layer is described as a late phase, which means the 1-month product has no differentiation. |
| SDLC Simulation | **5 / 5** | Genuinely excellent SDLC coverage if you reach the interesting parts: multi-service architecture design, database design for multi-tenancy, API design, real-time considerations, Kafka topology design, microservice decomposition, testing strategy, deployment. This is the best idea for SDLC learning — but only if you have more than 1 month. |
| Resume Value | **4 / 5** | At full implementation, this is one of the strongest backend engineering portfolio projects available. A working, deployed FlowForge with Kafka, WebSockets, microservices, and an AI agent layer is remarkable. The problem is that the 1-month version shows none of this — it shows a basic task manager. |

**Recommendation:** This is the right project to build over 6 months as a learning platform — not 1 month as a portfolio piece. If you build it, frame it explicitly as an ongoing engineering laboratory and show the architecture diagram and technical decisions even if the feature set is limited. Never demo the 1-month version as a finished product.

---

## Decision Guide

```text
Goal: Maximum demo-ability in 1 month?
    → IDEA-006 (LLMOps Gateway)

Goal: Best agent engineering learning?
    → IDEA-007 (Multi-Agent Research)

Goal: Most personally useful product you'll keep using?
    → IDEA-003 (AI Chief-of-Staff)

Goal: Best fit for developer tooling / AI coding roles?
    → IDEA-004 (Project Memory)

Goal: Best fit for SRE / platform engineering roles?
    → IDEA-005 (Incident Intelligence)

Goal: Deepest backend engineering learning (long term)?
    → IDEA-002 (FlowForge) — but not in 1 month
```
