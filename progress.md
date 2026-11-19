# FDE Progress Tracker

**Start date:** 2026-11-07 · **Target end:** 2027-01-02
**Current day:** D2 — ML essentials II: precision, recall, neural nets (see `ROADMAP_DAILY.md`)
**Current week:** 2 — Foundations · Daily command: `/fde-tutor today`

## Topics (confidence 1–5)
| Week | Topic | Confidence | Artifact shipped |
|---|---|---|---|
| 1 | FDE mindset, raw LLM APIs, structured outputs, tokens/cost/caching | 3.5 (mindset solid; structured outputs 3; cost/caching 4) | emalify-v2 classifier working (Groq gpt-oss-20b: 97% acc, 43% automation after his prompt fix, 0 automated-wrong) — not yet pushed/blogged |
| 2 | Foundations: ML essentials (D1 ✅ 3.5), LLM internals, model choice | in progress | |
| 3 | Evals: golden sets, LLM-as-judge, CI | – | |
| 4 | Agents, tool calling, MCP | – | |
| 5 | Enterprise integration, auth, data sync | – | |
| 6 | Deploy, observe, secure | – | |
| 7 | Customer engagement, capstone polish | – | |
| 8 | Interview mode + applications | – | |

## Weak spots
- Jumps to fixes before finding the broken link (first fix for refund bug was "update the docs", not "move the date math into code").
- Answers in stories rather than structure when asked to list failure points per link. Practice listing each link with its failure mode.
- States a rule boundary ("day 7 is inside") with confidence before checking who owns that decision.
- Schema design: first instinct was string-matching free text; missed that an enum value outside the allowed set ("payments") is the real bug. Missed that a date *range* needs start/end fields, and let the model invent a value the user never gave (leave type "sickLeave"). Rule: if the user didn't say it, the field is null/"unspecified" → ask.
- First schema draft drifted to generic categories (important/spam) unconnected to downstream actions; dropped needs_human. Fixed after one question.
- 2026-11-13: pasted a real API key into source code (as the value of key_env). Lesson: secrets live in .env (gitignored), code reads env var names; rotate any key that leaked.
- Quotes textbook rules without checking fit (D1: 70/15/15 split for a prompt-only system that trains nothing).
- Didn't see why a raw ID is a bad numeric feature (arbitrary labels have no magnitude); needed an explanation for one-hot.
- **Asked for N things, gives fewer** (D1: again on high-bias fixes and the 2-line summary) (4×: metrics ×3, D0 Q6 'two problems'). His own fix: count answers before sending.
- Forgot logs = customer PII (D0 Q5, scored 2/5).
- Asked for two metrics, gives one. Forgot automated-but-wrong AGAIN in S3 (listed accuracy/automation/cost/latency) — repeated weakness, drill it in review.
- Guesses before checking his own data (S3: blamed hidden tokens on retries while his report said 0 retries).
- Gives a decision without the reason (picked Model X with no justification until pushed). Automation rate must always be paired with automated-but-wrong.
- Left identity out of his own summary. Identity/authorization must come from the authenticated channel, never from model output.

## Review scores
| Date | Review | Score | Weakest |
|---|---|---|---|
| 2026-11-16 | Week 1 (D0) | 21.5/30 | git secrets/PII (2), debugging 'what changed' (3), two-problems (3) |

## Drill scores
| Date | Drill | Discovery | Metrics | Objections | Technical | Next steps |
|---|---|---|---|---|---|---|

## Session log
- 2026-11-07 — setup — plan created from JD research + resume
- 2026-11-08 — learn (W1 S1: FDE mindset) — Symptom ≠ cause; trace the chain. Business rules/math go in code, not the model. Ambiguous rules → customer decides → record the decision in docs + tests/evals. Transfer (hospital dosing) passed: code checks rules, model explains, ambiguity → ask hospital for per-patient max-dose rule. Corrected own summary from 'model takes decisions' to 'model explains decisions'. Next: W1 S2 raw LLM APIs + structured outputs.
- 2026-11-09 — learn (W1 S2: structured outputs) — Free text → JSON with enums → schema validation (zod/pydantic) + API structured-output mode. IDs are strings. Model proposes, code verifies: verbatim check → DB exists → ownership vs authenticated sender. Transfer (HR leave bot) partial: needs start/end dates, no invented leave type, bot submits a request rather than approving. Next: W1 S3 tokens, cost, model choice, prompt caching + Emalify rewrite build.
- 2026-11-11 — project (W1 build kickoff) — No code existed yet; built together. Repo: ~/Desktop/Coding/emalify-v2. Rohit designed TicketClassification (enum from downstream actions + 'other' escape hatch + needs_human + reason). Learned: enum values map to code actions; closed enums need an escape hatch; schema validation checks shape, not intent; prompt injection (#18) is defended by code-side override + ownership check, delimiters are only a speed bump. Status: scaffold + 30 emails ready; needs `sudo apt install python3.12-venv` + API key; classify.py steps 1–6 unwritten. No API key yet → build against a fake call_llm() with canned bad responses first; free OpenAI-compatible options: Gemini AI Studio, Groq, Ollama.
  - Follow-up: understood tags = speed bump (like escaping SQL by hand) vs code checks = real defense. Found his own gap: 'other' + needs_human:false slipped past both checks → rule: model can only escalate needs_human, never lower it; risky categories forced to human in code.
- 2026-11-14 — project (W1 build, steps 2–4) — Steps 1–4 working in fake mode (validate, ALWAYS_HUMAN, retry-with-error, fallback). Rohit understood: one passed test ≠ defense; a retry must include the error, since an identical request at temperature=0 returns the same answer. Asked for detailed Python comments (weak in Python, strong in JS/TS). .env still LLM_PROVIDER=fake and LLM_MODEL not a real ID. Next: Step 5 (API errors/rate limits + token/latency logging), Step 6 (run all 30).
- 2026-11-14 — project (W1 build, step 5) — Switched to real Gemini (gemini-3.5-flash; 3.8 gave 503, 2.5 gave 404). Rohit correctly split retryable (429/503) from permanent (401/404) errors and recalled BullMQ-style wait-and-retry. Built exponential backoff + jitter + Retry-After, SDK retries off, JSONL call log (tokens/latency). Real run: ~300 in / ~35 out tokens per email; one 26.8s latency outlier (#16). Next: Step 6 run all 30 + accuracy + human-rate.
  - Latency debug: couldn't find the cause alone (correct — 1 sample isn't enough). Designed the right experiment himself (run 5×: all slow = email, mixed = provider). Result #16: 2.3–20.7s, median 4.4s → provider variance. Hit 429 on the free tier when backoff was bypassed. Learned p50 vs p95. NOTE: emails.json #16 key accidentally typed over as 'idnot acceptable but'; he needs to fix it.
- 2026-11-14 — project (W1 build, step 6) — Rohit picked cost first, then reached automation rate (% with no human) himself. Step 6 report built (accuracy, automation rate, automated-but-wrong, fallbacks, tokens, p50/p95). Real Gemini run hit the free-tier quota: 26/30 fell back on 429 → 0 automated-but-wrong (safe) but 3% automation (useless). Open question for him: the report mixes 'AI was wrong' with 'API was down'. Next: separate those metrics, slow the request rate or switch to Groq, re-run.
- 2026-11-14 — project (W1 build, report split + Groq) — Rohit: an API outage must not be reported as low AI accuracy → report now splits system health / AI quality / business value. Mixed up LLM_PROVIDER vs LLM_MODEL again (put provider name in MODEL). Switched to Groq openai/gpt-oss-20b: 29/30 accurate, p50 654ms / p95 1.8s, 0 API failures, automation only 27% (every delivery email sent to human), 0 automated-but-wrong. Only miss #24 (rude agent: label 'other' vs model 'delivery') = label ambiguity → customer decides. Next: raise automation without raising automated-but-wrong; push repo + README; Friday drill.
  - Diagnosed the low automation himself (the 'complaint' rule was too broad) and wrote a signal-based rule (simple late = auto; lost/angry/refund threat = human). Automation went 27% → 43% with 0 automated-wrong. Side effect: injection #18 now fooled the model (refund) but ALWAYS_HUMAN caught it → saw why every prompt change needs a full re-run (Week 3 preview).
  - Close: summary 'accuracy matters, but real value to the customer + guardrails + retry feedback' (good; sharpened with numbers). Transfer (bank, '99% accurate → automate all'): named automation rate but forgot automated-but-wrong as the second number; picked refunds as the always-human type (ok) but missed bank-specific ones (fraud/unauthorized transaction, account access, KYC). Weak spot: names one metric when asked for paired metrics.
- 2026-11-14 — learn (W1 S3: tokens, cost, models) — Repeated system prompt is most of the input; hidden reasoning tokens are billed as output. Choose a model by eval: gate (automated-but-wrong≈0), then optimize; did the break-even math himself (₹42/150 = ₹0.28 per email). Caching: stable prefix first, changing data last. Transfer (edtech textbook) passed. Notes: notes/W1-S3-tokens-cost-models.md. Next: push repo + README, blog, Friday drill customer, Sunday review.
- 2026-11-15 — setup — Merged the Outcome School FDE roadmap (github.com/amitshekhariitbhu/forward-deployed-engineer-roadmap) into a 50-day curriculum (ROADMAP_DAILY.md, D0 2026-11-15 → D49 2027-01-03). New daily command: /fde-tutor today.
- 2026-11-16 — today D0 (big picture + W1 review) — 6 terms via questions: RAG for slow knowledge vs tools for live data; workflow vs agent; MCP = build once; fine-tune for tone only after prompt+examples fail a leads-rated 1–5 target; temperature ≠ tone; quantization gated on automated-but-wrong (answered unprompted). Review 21.5/30. Fairly challenged an ambiguous schema question (Q2 regraded). His summary: 'count answers before sending, ask what changed before fixing'. Build task pending: push both repos to GitHub. Notes: notes/D0-big-picture-week1-review.md
- 2026-11-18 — today D1 (ML essentials I) — Read both must-reads. Realised his W1 '43%' was a validation number (overfit). Honest test = real Kirana emails, labeled by their leads, stratified, run once; prompt systems need dev+test only. Bias/variance via his own student analogy; dev≫test = variance, both low = bias → look at failures first. Supervised vs unsupervised (clustering for discovery), features must be real numbers, one-hot (needed explanation), iterations math (got 80 after explanation). Transfer (hospital vendor 98%) good: held-out set + doctor labels. Build: stratified dev/test split in emalify-v2. Notes: notes/D1-ml-essentials-data-splits.md. GitHub push still pending.
  - D1 build done: 20 messy emails added (50 total), split.py (stratified 50/50, seed 42), classify.py --set dev|test|all. Groq: dev 100% acc / 44% auto, test 100% acc / 48% auto, 0 automated-wrong on both. Labeling review: confused category with needs_human on #34 (legal threat → still delivery + human); saw #36 multi-intent = single-label schema limit; skipped #40 (count!). #40 COD cancel → question for Kirana.
