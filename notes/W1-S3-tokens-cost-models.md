# Week 1 · Session 3: Tokens, Cost & Choosing a Model
*2026-11-14 · Revision notes*

---

## 1. Where the tokens actually go

Your Groq run: **avg 466 input / 133 output tokens per email.**

**Input side:** email #1 is only ~25 tokens of customer text, so the other ~440 tokens are the **system prompt, sent again on every call.**
→ Kirana mostly pays for **your instructions**, not the customer's words.

**Output side:** the JSON reply is ~35 tokens, but gpt-oss averaged 133.
→ The extra ~100 are **hidden "thinking" tokens**. Reasoning models think before answering, and those tokens are **billed as output** (the expensive kind) even though you never see them.

| Model | Output tokens (#1) | Why |
|---|---|---|
| Gemini 3.5 Flash | ~42 | mostly just the JSON |
| Groq gpt-oss-20b | ~133 avg | JSON + hidden reasoning |

Thinking isn't bad: it helps on hard problems. But for *"pick 1 of 5 categories,"* you have to **prove** it's worth paying for.

---

## 2. ⭐ Choose a model by eval: gate first, then optimize

**"By eval"** = run the same 30 emails on each model and compare the numbers. Not opinions, not benchmarks, not hype.

**The hiring analogy:**
- **Gate:** a driver without a license is OUT, however cheap they are.
- **Optimize:** among licensed drivers, compare salary, speed, experience.

**For models:**
1. **Gate** (pass/fail, no trade-offs): **automated-but-wrong ≈ 0**
2. **Optimize** among the survivors: automation ↑, cost ↓, latency ↓

| | Model A | Model B | Model C |
|---|---|---|---|
| Gate: automated-but-wrong | ✅ 0 | ❌ 3 | ✅ 0 |
| Automation | 43% | 50% | 45% |
| Cost / 1,000 | ₹40 | ₹10 | ₹12 |
| → | candidate | **OUT** | **pick (cheaper, faster, passes gate)** |

> **Safety rules first (filter), then best value among the survivors.**
> Never trade customer harm for ₹30. A failed model may pass after a prompt fix, but **re-run the eval to prove it.**

### Comparing survivors: convert everything to business value
Hindi inbox case: X (40% automation, ₹50) vs Y (25%, ₹8), both passing the gate.
- Per 1,000 emails: X costs **₹42 more** and automates **150 more** emails.
- Break-even: **₹42 ÷ 150 = ₹0.28 per email.**
- A human handling one email costs Kirana ~₹15–40 → **X wins by 50–100×.**

**How to say it to a VP:**
> *"X costs ₹42 more per 1,000 emails but saves 150 human-handled emails, roughly ₹3,000+ of agent time. Z was rejected because it sent 2 wrong answers to customers unchecked."*

**Lead with business value, not model specs.**

---

## 3. ⭐ Prompt caching: stable first, changing last

Same idea as Redis: don't redo expensive work for identical input. The provider stores its processed version of a repeated prompt, and later calls reuse it → **cheaper + faster**. (Some providers cache automatically; some need you to mark what to cache.)

**Caches match on the PREFIX, byte for byte, from the very first token.**

```
❌ [email text] + [440-token system prompt]   → prefix differs on every email → ~0% hits
✅ [440-token system prompt] + [email text]   → identical prefix every time → hits
```

### The trap
```
Today is 2026-11-14 10:42:07. You are helping customer Priya Sharma.   ← changes every call!
You classify customer support emails for Kirana Logistics...
```
→ The timestamp changes every second and the name every customer, so **the cache never hits again.**
**Fix:** move changing data to the **end** (the user message). And ask: **does the task even need it?** Every token costs money on every call.

### Transfer: edtech tutor
`[student name + question]` + `[50-page textbook]` → flip it: **textbook first, question last.**
It saves a lot here because the textbook is **tens of thousands of identical tokens** on every call, so caching turns the biggest part of the bill into the cheap part.
*(Week 2 preview: also ask whether you need to send the WHOLE textbook at all, or only the relevant pages. That's retrieval.)*

---

## ⚠️ My mistakes (don't repeat)
- Guessed the hidden output tokens were "reason or retry feedback." My own report showed **0 retries**, and `reason` is inside the visible JSON. **Check my own data before guessing.**
- Listed accuracy, automation, cost and latency, but **forgot automated-but-wrong again**. It's the gate, the most important number.
- Picked Model X without saying **why**. Always give the reason (break-even math).
- Skipped the "where in the request" half of the caching question at first.

---

## 🔁 Quick self-test
1. Your call uses 466 input tokens for a 25-token email. Where do the rest go?
2. Why does a reasoning model cost more for the same JSON answer?
3. What's the gate when choosing a model? What do you optimize after it?
4. X costs ₹42 more per 1,000 emails and automates 150 more. What number decides it?
5. Why must the system prompt come first for caching to work?
6. A teammate adds a timestamp at the top of the system prompt. What breaks?

<details><summary>Answers</summary>

1. The system prompt, repeated on every call.
2. Hidden thinking tokens, billed as (expensive) output tokens.
3. Gate: automated-but-wrong ≈ 0. Then optimize automation, cost and latency among the survivors.
4. The cost of a human handling one email. Break-even is ₹0.28.
5. Caches match the prefix from the first token; the stable part must come first.
6. The prefix changes every call → 0% cache hits. Move it to the end, or drop it.
</details>
