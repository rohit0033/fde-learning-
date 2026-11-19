# D0 · The 6 Big Words + Week 1 Review
*2026-11-16 · Revision notes*

---

## 1. ⭐ The 6 words from every first customer meeting

| Term | One-line version for a VP | FDE nuance |
|---|---|---|
| **LLM** | The model that reads and writes text | Knows nothing about *their* business by default |
| **RAG** | Look up the company's documents and show the relevant pages to the AI before it answers | For **slow-changing knowledge** (policies, SOPs), not live data |
| **Agent** | The AI decides which tools to use, in a loop, until it's done | A **workflow** = your code decides the steps (emalify-v2). An **agent** = the model decides. Riskier → risky tools need human approval in code |
| **MCP** | A standard plug: build a tool once, and any MCP-compatible AI app can use it | Like USB-C. Ask: **whose permissions** does the tool call run with? |
| **Fine-tuning** | Retrain the model to change *how* it behaves (tone, style, format) | Bad for **changing facts**. Try prompt + examples first, and prove the need with a score |
| **Quantization** | Shrink a model to fit smaller hardware (e.g. 16-bit → 4-bit, ~4× smaller) | Some quality loss → test on **their** data, with the gate |

### ⭐ RAG vs tools
- *"What's our refund policy?"* → **RAG** (a document, changes monthly at most)
- *"Is item X in stock right now?"* → **tool / DB query** (live data; an index would be outdated)

### ⭐ Before fine-tuning for tone
1. Prompt with **3-5 real replies from their best agents** as examples (models copy examples better than descriptions)
2. **Temperature does NOT control tone.** It controls randomness. Higher = more varied, not friendlier.
3. Measure: **Kirana's support leads rate ~50 replies 1-5**, with the target **agreed beforehand** (e.g. avg ≥ 4)
4. Fine-tune **only if** prompt + examples can't reach the target
5. Later: an **LLM-as-judge** trained to score like the leads (Week 4)

### Quantization check
Compare quantized vs full on their emails. **Gate = automated-but-wrong stays 0.** (Answered unprompted ✅)

---

## 2. Week 1 review: 21.5 / 30

| Q | Topic | Score | Key lesson |
|---|---|---|---|
| 1 | "Since Tuesday, delivery emails go to spam" | 3 | Ask **"what changed on Tuesday?"** (prompt, model version, email mix) **before** fixing |
| 2 | Hotel booking schema | 4 | Guest didn't say a room type → `"unspecified"`. Identity comes from the session (if it's the model's output schema) |
| 3 | 401 → "increase retries" | 5 | 401 = permanent (wrong key). Retries hide the real error |
| 4 | CEO: "remove the `other` → human rule" | 4 | Explain what's IN `other` (legal, vendors, injection) + **offer a safe path** (split `other` into categories) |
| 5 | `.env` and `logs/` in git status | 2 | `.env` = keys, `logs/` = **customer PII**. `git rm --cached`, check `.gitignore`. Leaked key → **rotate** |
| 6 | Timestamp + name at prompt top, 3× bill | 3 | (1) breaks the cache → move to the end; (2) **the classifier doesn't need them at all** → remove; trim the 400 lines |

### Model answer: Q1
1. Pull the misrouted emails from the logs and read their `reason`
2. **Check what changed on Tuesday**: deploys, prompt edits, model version, incoming email mix
3. Reproduce with the old vs the new setup
4. Fix the cause, add those emails to the eval set, re-run everything

### Model answer: Q4 (how to say no to an exec)
> *"No. `other` holds legal notices, vendor invoices, staff complaints and injection attempts. Auto-replying to those is how we get a consumer-court problem. But I can raise automation safely: split `other` into specific categories, route each properly, and show you the new automation rate with automated-but-wrong still at 0."*

### Model answer: Q5
```bash
git rm --cached .env
git rm -r --cached logs/
# confirm .gitignore has .env and logs/, then:
git status   # both gone → now commit
```

---

## ⚠️ My mistakes (don't repeat)
- **Asked for N things, gave fewer** (4th time: Q6 asked for two problems, I gave one). → **Count my answers before sending.**
- **Jumped to a fix** (Q1: "change the prompt") before asking what changed.
- Forgot that **logs contain PII**. They matter as much as API keys.
- Said temperature could help with tone. It controls randomness only.
- First answer on how to judge tone was "I will judge it": a feeling, and not the customer's. → Their leads, 1-5, target agreed beforehand.

## ✅ What went well
- Spotted that live inventory doesn't belong in RAG.
- Named the gate (automated-but-wrong) **without being prompted**.
- Pushed back on an ambiguous question. Next time, ask the clarifying question **before** answering.

## 🔁 Quick self-test
1. Policy question vs stock question: which uses RAG, which uses a tool?
2. What makes something an agent rather than a workflow?
3. A customer wants their brand tone. What do you try first, and how do you measure it?
4. What does temperature control?
5. "Since Tuesday, X is broken." What's your step 2?
6. Which two files must never be pushed, and why?

<details><summary>Answers</summary>

1. Policy → RAG (slow-changing documents). Stock → tool/DB query (live data).
2. The model decides which tool to call next, in a loop. In a workflow, your code decides.
3. Prompt + 3-5 examples from their best agents. The support leads rate replies 1-5 against a target agreed beforehand.
4. Randomness/variety, not tone or style.
5. Check what changed on Tuesday (prompt, model version, deploys, input mix).
6. `.env` (API keys) and `logs/` (customer PII).
</details>
