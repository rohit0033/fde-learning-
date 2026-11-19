# Forward Deployed Engineer — 8-Week Plan for Rohit

> Built on: 2026-11-07 · Starting point: ~1.5 yrs full-stack (React/Node/TS), RAG + LLM side projects, payments/webhooks/queues in production.
> Tutor: run `/fde-tutor today` in this folder every day. Progress lives in `progress.md`.
> **Day-by-day curriculum:** `ROADMAP_DAILY.md`. It merges this plan with the [Outcome School FDE Roadmap](https://github.com/amitshekhariitbhu/forward-deployed-engineer-roadmap). From Week 2 on, the week-by-week topics below are superseded by that file (same capstone, roadmap order).

---

## 1. What the market is asking for (JD research, Nov 2026)

Postings sampled: DevRev (Bangalore/Chennai), Nanonets (Bangalore), Anthropic (Applied AI), OpenAI, Sarvam AI, Workato (Bangalore), Galileo, C3 AI, Google Cloud GenAI FDE, Palantir FDSE, Scale AI, Prodapt, plus 2026 role guides.

### Skill frequency across postings

| Skill | How often it shows up | Typical wording |
|---|---|---|
| Python + TypeScript/JS production code | Almost all | "Strong TS/JS and Python, DS&A" (DevRev) |
| LLM apps: RAG, function/tool calling, agents | Almost all AI-company FDE roles | "LLMs, prompt engineering, RAG, function calling" |
| **Evals** for LLM/agent systems | Every frontier-lab posting | "Build evals that catch hallucinations, regressions" (OpenAI/Anthropic) |
| Enterprise integrations: REST, GraphQL, webhooks, pub/sub, 2-way sync | Most | "Large-scale one-way and two-way data sync" (DevRev) |
| MCP servers / sub-agents / agent skills | Rising fast | "Deliver MCP servers, sub-agents, agent skills" (Anthropic) |
| Cloud + deploy: serverless, containers, CI/CD, observability | Most | "AWS Lambda, GCF, containers, telemetry" |
| SQL + data modeling, schema mapping, dashboards | Most | "Data mapping, schema alignment" |
| Customer discovery, scoping, demos, stakeholder comms | All | "Underspecified customer scenario" interview round |
| Ambiguity / problem decomposition | All | Palantir "Decomposition" round, OpenAI "deployment case study" |
| Security/compliance (auth, SSO, PII, VPC deploys) | Enterprise roles | "Security, compliance, enterprise deployment requirements" |

**Experience bar:** Big labs want 4–8 yrs. India startups (Nanonets 2–5 yrs, DevRev, Sarvam 4+ preferred, Weekday 4–6 yrs @ ₹60–80L) are where a ~2-yr engineer with **a strong shipped project + case-study skills** can get in. Search titles too: *Forward Deployed Software Engineer, AI Solutions Engineer, Deployment Engineer, Applied AI Engineer, Customer Engineer*.

**Interview loop (common pattern):** practical coding/debugging → **decomposition/deployment case study** → LLM systems deep-dive (evals, drift, hallucinations) → stakeholder communication → values/judgment.

---

## 2. Your gap analysis

| Area | You have | Gap → what to build |
|---|---|---|
| Full-stack TS/React/Node | ✅ Strong (Gether, Outbox) | Keep it sharp; stop learning new frameworks |
| Integrations (webhooks, Stripe, OneSignal, Zoom SDK, Gmail OAuth) | ✅ Good base | Idempotency, retries, 2-way sync, conflict resolution, rate limits |
| Queues / async (BullMQ, Redis) | ✅ | Dead-letter queues, backpressure, exactly-once myths |
| Customer support (Intercom tickets) | 🟡 Some | Run discovery calls, write scoping docs, demo |
| RAG (LangChain + Pinecone) | 🟡 Prototype level | Chunking/hybrid search/reranking, **retrieval evals**, drop framework magic |
| Agents / tool calling / MCP | 🔴 Missing | Build agent loop from scratch, MCP server, sub-agents |
| **Evals & LLM observability** | 🔴 Missing (most important gap) | Golden sets, LLM-as-judge, regression CI, tracing |
| Python depth (FastAPI, pydantic, async) | 🟡 Listed | Ship one real service in Python |
| Docker / CI/CD / cloud deploy / IaC | 🟡 Basic AWS | Docker Compose, GitHub Actions, one Terraform module, Lambda/Cloud Run |
| SQL analytics / data modeling | 🟡 DBMS coursework | Window functions, messy data mapping, dashboards |
| Security: SSO, RBAC, PII, prompt injection | 🔴 | OAuth/OIDC deep, PII redaction, injection defenses |
| Decomposition & case interviews | 🔴 | Weekly practice with the tutor as interviewer |

Your **edge**: you've shipped end to end, debugged customer tickets, and integrated third-party SDKs. That's the core FDE skill. The plan adds AI-systems depth on top and turns it into stories you can tell in interviews.

---

## 3. The 8-week plan (≈3 hrs weekday + 6 hrs weekend ≈ 21 hrs/week)

Each week = **Learn (Socratic sessions) → Build (feeds the capstone) → Field drill (customer/interview skill) → Ship a public artifact.**

### Week 1 — The FDE mindset + LLM API fundamentals without frameworks
- **Learn:** How FDEs differ from SWE/SE/consultants. Raw LLM APIs: messages, tool use, structured outputs, streaming, tokens/cost, prompt caching, model selection.
- **Build:** Rewrite a piece of Emalify **without LangChain**: classify an email with raw API calls, return structured JSON validated with pydantic/zod, log tokens and cost.
- **Field drill:** Read 5 live FDE JDs and rewrite each one as "the customer problem this team solves."
- **Ship:** Blog post titled "What I learned removing LangChain from my project."
- **Socratic anchors:** *Why would a company pay an engineer to sit with a customer rather than ship product? / What breaks if your JSON output is 99% valid? / When is a framework a liability at a customer site?*

### Week 2 — Retrieval done properly
- **Learn:** Chunking strategies, embeddings, hybrid (BM25 + vector) search, reranking, metadata filters, pgvector vs Pinecone vs Elasticsearch (you already know ES!).
- **Build:** Retrieval layer on Postgres + pgvector **plus** your ES experience for hybrid search. Measure recall@k on a 50-question set you write yourself.
- **Field drill:** Mock discovery call. The tutor plays a customer who says "our chatbot gives wrong answers." Your job is to find the real problem.
- **Ship:** A retrieval benchmark table in the repo README.
- **Socratic anchors:** *How do you know retrieval failed versus generation failed? / Why might keyword search beat embeddings for SKU numbers?*

### Week 3 — Evals (the #1 differentiator)
- **Learn:** Golden datasets, code-based checks, LLM-as-judge (and its biases), pairwise comparisons, regression suites, eval-driven development, hallucination/groundedness metrics.
- **Build:** Eval harness: about 100 cases, scored by both deterministic checks and an LLM judge, run in **GitHub Actions on every PR**, with a failure report.
- **Field drill:** Write a "success criteria" doc *before* building, the way OpenAI FDEs define metrics first.
- **Ship:** CI badge plus an eval report.
- **Socratic anchors:** *If your judge model agrees with you 80% of the time, is that good? / What eval would have caught your last bug?*

### Week 4 — Agents, tool calling, MCP
- **Learn:** Agent loops, tool design (names, schemas, errors), planning vs ReAct, sub-agents, human-in-the-loop approvals, MCP (servers, tools, resources, auth).
- **Build:** An agent loop from scratch in Python (no framework) with 4–5 tools, then expose the customer's systems as an **MCP server**.
- **Field drill:** First **decomposition case**: "A logistics company wants AI to handle 40% of support tickets in 90 days."
- **Ship:** The open-source MCP server.
- **Socratic anchors:** *What should an agent never be allowed to do without a human? / How do you eval a multi-step trajectory, not just the final answer?*

### Week 5 — Enterprise integration & data
- **Learn:** OAuth2/OIDC/SSO (SAML basics), RBAC, webhooks at scale (idempotency keys, signatures, retries, DLQ), 2-way sync and conflict resolution, rate limits, schema mapping messy data, SQL window functions.
- **Build:** Connectors for the capstone: ingest from a helpdesk-style API plus a CSV dump with dirty data, normalize into your schema, keep it in sync via webhooks plus a polling fallback.
- **Field drill:** Customer says "IT won't let data leave our VPC." Propose 3 deployment options with tradeoffs.
- **Ship:** Architecture diagram plus ADR (architecture decision record).
- **Socratic anchors:** *A webhook arrives twice and out of order. What does your system do? / Who owns the data mapping when the customer's schema changes?*

### Week 6 — Production: deploy, observe, secure
- **Learn:** Docker/Compose, GitHub Actions CD, one cloud target (AWS Lambda or GCP Cloud Run), Terraform basics, tracing (OpenTelemetry/Langfuse-style LLM traces), cost/latency dashboards, prompt injection, PII redaction, audit logs.
- **Build:** Deploy the capstone with one command. Add tracing, a cost dashboard, PII redaction, and injection tests in your eval suite.
- **Field drill:** Write an incident post-mortem for a staged outage (the tutor will break something for you to debug).
- **Ship:** Runbook plus a live demo URL.
- **Socratic anchors:** *Latency doubled overnight and nobody deployed anything. What are your first 3 checks? / What does "secure" mean to a bank's CISO vs. to you?*

### Week 7 — Customer engagement & polish
- **Learn:** Discovery frameworks, scoping/SOW, demo craft, handling objections, writing for executives, feeding field insights back to product.
- **Build:** Finish the capstone: admin UI (your React strength), human-review queue, metrics page showing business impact (deflection rate, time saved).
- **Field drill:** 2 full mock customer meetings (exec plus IT/security), recorded, with self-review.
- **Ship:** 5-min Loom demo plus a 1-page case study ("problem → approach → impact → what I'd do next").
- **Socratic anchors:** *The customer's VP wants feature X, their engineers want Y, and you have 2 weeks. What do you do?*

### Week 8 — Interview mode
- **Learn:** Review your weakest areas from `progress.md`.
- **Do:** 3 decomposition mocks, 2 LLM-systems deep-dives on *your own* project, 1 practical coding/debugging session, behavioral stories (STAR) from Gether/Outbox/capstone.
- **Apply:** 15–20 targeted applications (Nanonets, DevRev, Sarvam, Workato, Galileo, Google Cloud, AI startups). Send each one with your case study plus demo link.
- **Ship:** Updated resume where every bullet is framed as an FDE outcome.

---

## 4. Capstone project — "FieldDesk": an AI support-ops agent deployed into a messy customer environment

**Scenario:** You are the FDE for *"Kirana Logistics"*, a fictional mid-size Indian logistics company (the tutor plays their stakeholders). They get about 3k support tickets a week across email and a helpdesk tool, the SOP docs are scattered, and order data lives in Postgres. They want an AI agent that resolves or triages tickets **safely**.

This builds on Emalify (email + LLM) and your Intercom/BullMQ/Stripe experience, so you're extending something you know rather than starting from zero.

**What you build**
1. **Connectors:** Gmail (reuse your OAuth work), a mock helpdesk REST API with webhooks, and dirty CSV order exports. Idempotent sync goes through BullMQ.
2. **Knowledge layer:** SOP/PDF ingestion → hybrid search (pgvector + BM25/ES) → reranking.
3. **Agent:** A Python/FastAPI agent loop with tools (`lookup_order`, `check_refund_policy`, `draft_reply`, `escalate`, `issue_refund` *behind a human approval*). The same tools are exposed as an **MCP server**.
4. **Evals:** 150+ case golden set (correct action, groundedness, tone, PII leakage, injection attempts). Runs in CI and blocks merges on regression.
5. **Production:** Docker Compose for local dev, cloud deploy (Cloud Run or Lambda) via Terraform, tracing, cost/latency dashboard, PII redaction, audit log.
6. **Ops UI (React):** Human-review queue, approve/edit drafts, and an impact metrics dashboard.
7. **FDE artifacts (as important as the code):** discovery notes, success-criteria doc, architecture diagram, ADRs, deployment-options memo (SaaS vs VPC vs on-prem), runbook, post-mortem, case study, and the 5-min demo.

**Definition of done:** Someone can clone the repo and run `make up`. The eval suite passes in CI. A live demo exists. The case study states measurable results, e.g. "auto-resolved 38% of eval tickets with 0 PII leaks and 96% grounded answers."

---

## 5. Weekly rhythm

| Day | Activity |
|---|---|
| Mon–Thu (≈45 min/day) | `/fde-tutor learn` Socratic session + reading |
| Mon–Thu (≈2 hr/day) | Build |
| Fri | `/fde-tutor drill`: customer role-play or decomposition case |
| Sat | Build + ship the weekly artifact |
| Sun | `/fde-tutor review`: weekly quiz, update `progress.md`, refresh JDs every 2 weeks |

## 6. Core resources
- Anthropic docs: tool use, MCP spec, "Building effective agents"; OpenAI cookbook (evals, structured outputs)
- Hamel Husain & Shreya Shankar's writing on LLM evals; Eugene Yan's "Patterns for building LLM-based systems"
- *Designing Data-Intensive Applications* (ch. 5, 7, 11) for sync, replication, and streams
- Palantir/Exponent decomposition guides: [tryexponent](https://www.tryexponent.com/guides/palantir-forward-deployed-engineer-interview), [Scaler](https://www.scaler.com/topics/palantir-fde-interview)

## 7. Sources (JD research)
- [DevRev FDE — Greenhouse](https://job-boards.greenhouse.io/devrev/jobs/5668939004)
- [Nanonets FDE — Greenhouse](https://job-boards.greenhouse.io/nanonets/jobs/5152992008)
- [Anthropic FDE, Applied AI](https://jobs.generalcatalyst.com/companies/anthropic/jobs/69674588-forward-deployed-engineer-applied-ai)
- [OpenAI FDE guide](https://fde.academy/blog/openai-forward-deployed-engineer)
- [FDE jobs in India & global — Scaler](https://www.scaler.com/topics/forward-deployed-jobs-in-india-global/)
- [Workato Senior FDE](https://www.themuse.com/jobs/workato/senior-forward-deployed-engineer)
- [Weekday FDE Bengaluru](https://apply.workable.com/weekday-1/jobs/view/420986EFD6.md)
- [Galileo FDE](https://jobs.weekday.works/forward-deployed-engineer-at-galileo-4392180652)
- [Scale AI FDE, GenAI](https://scale.com/careers/4593571005)
- [FDE role guide — Aced](https://www.aced.io/blog/what-is-a-forward-deployed-engineer)
- [FDE 2026 guide — Hashnode](https://hashnode.com/blog/a-complete-2026-guide-to-the-forward-deployed-engineer)
