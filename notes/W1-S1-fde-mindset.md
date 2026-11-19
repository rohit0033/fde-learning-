# Week 1 · Session 1: The FDE Mindset
*2026-11-08 · Revision notes*

---

## 1. Symptom ≠ Cause

A customer reports a **symptom** (what they see). The **cause** is often somewhere else entirely.

**Your own example (Outbox):**
- Symptom: "The dashboard shows wrong data."
- Team's guess: "The backend is broken."
- Real cause: the **frontend sent the wrong filter** in the API request, so the backend correctly returned the wrong data.
- The clue was already there: *the same API returned correct data elsewhere*, so the bug had to be in **what's different between the callers**.

**Why the team guessed wrong:** they assumed *"the bug is wherever the data comes from."*

### Trace the chain
Data passes through a chain of links, and any link can break. The symptom only shows up at the end.
```
user → frontend filter → request → API → DB → response → render
```

**Rule:** Before naming a cause, **list every link** and ask how each one could produce the symptom.

---

## 2. AI version: "The model is hallucinating!"

Kirana's VP says: *"Your AI told a customer their refund was approved. It wasn't. Fix the hallucination."*

That's the same pattern: a symptom with a confidently guessed cause. The chain looks like this:
```
ticket → order lookup → tool call → docs retrieval → model answer
```

**Scenario:** the policy says *7 days from order*, but the agent compared against the *delivery date*, so it decided the customer was eligible.
→ That's **not** a hallucination. The **data/tool layer** gave the model the wrong date to reason with.

---

## 3. ⭐ Business rules belong in code, not the model

| ❌ Weak fix | ✅ Strong fix |
|---|---|
| "Add 'use order date' to the prompt" | **Code** calculates eligibility |
| "Fix the docs wording" | Tool returns the decision, not raw dates |

The tool should return something like:
```json
{ "refund_eligible": true, "days_since_order": 7, "policy": "7d_from_order" }
```
The model then just **explains** a decision code already made. That's deterministic and testable, and it works on 10,000 tickets a week.

> **Code enforces rules (money, policy, limits). The model understands the request and explains the outcome.**

The model still makes *soft* calls ("is this a refund or a delivery question?"). Anything involving money, policy or compliance is decided by **code**.

---

## 4. Ambiguous rules → the customer decides

"7 days from order": is day 7 included? **You don't decide that, and neither does the model. Kirana decides.**

**What an FDE does:**
1. Notice the ambiguity.
2. Ask the business owner and get a clear answer.
3. **Record the decision** where it can't silently break:
   - 📄 docs
   - 🧪 test cases
   - 📊 **eval set** (e.g. "ordered Oct 28, asks Nov 4 → eligible"; "asks Nov 5 → not eligible")

**Also:** read the customer's **existing source of truth** (their order system, their policy table). Don't copy their rules into your code, because copies go stale.

---

## 5. Transfer example: hospital

*"Can patient in bed 12 get another paracetamol dose now?"*
- **Code:** checks the last dose time and the max daily dose
- **Model:** explains the result to the nurse
- **First question to the hospital:** what's the max-dose rule *per patient* (weight, liver condition)? And **where does that rule already live**, in the doctor's order in their records system or a formulary table? Read it from there.

---

## ⚠️ My mistakes (don't repeat)
- I jumped to a fix ("update the docs") **before** finding which link broke.
- I answered with a story when asked for a **structured list**. Interviewers score structure.
- I stated a rule boundary ("day 7 is inside") with confidence **before asking who owns that decision**.
- In my first summary I wrote "the model's job is to take decisions." Wrong: **the model explains decisions.**

---

## 🔁 Quick self-test
1. A customer says "wrong data on the dashboard." What's your first move?
2. Who should calculate "is this order within the refund window," and why?
3. A policy is ambiguous. Who decides, and where do you record the answer? (3 places)
4. What's the model's job vs. code's job, in one line?

<details><summary>Answers</summary>

1. List the chain of links and find which one differs or breaks. Don't guess the cause.
2. Code. It's deterministic, testable and the same on every ticket.
3. The customer/business owner. Record it in docs, tests and the eval set.
4. The model understands and explains; code enforces rules.
</details>
