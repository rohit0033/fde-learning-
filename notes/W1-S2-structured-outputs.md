# Week 1 · Session 2: Structured Outputs
*2026-11-09 · Revision notes*

---

## 1. Why free text breaks

Emalify's old approach: the model returns text, and code checks the text.

Same email, three possible replies:
```
"Billing"
"billing."
"This email appears to be about a billing issue, though it may also relate to a refund."
```
- `response === "Billing"` → only the 1st works.
- `text.includes("billing")` → also matches *"This is **not** a billing question"*. ❌

**At 10,000 emails a week, a "rare" parsing failure means silent misrouting every day.**

---

## 2. ⭐ Make the LLM answer like Stripe does

Stripe never replies *"the payment mostly succeeded."* It returns **JSON with fixed fields and allowed values**. Make the LLM do the same.

But **asking** for JSON isn't enough. The model can still return:
```
Sure! Here's the JSON:
{"category": "payments", "confidence": "high"}
```
Problems: chatty text around the JSON, **`"payments"` isn't an allowed value**, and an extra field.

### Two layers of protection
1. **Validate against a schema in code**: pydantic (Python) or zod (TS). An invalid value raises an error, and you handle it (retry → human).
2. **Use the API's structured/JSON output mode**: the API constrains what the model can return. Keep validating anyway (defense in depth).

```python
class TicketClassification(BaseModel):
    category: Literal["delivery", "refund", "change_request", "spam", "other"]
    needs_human: bool
    reason: str = Field(max_length=200)
```
```ts
// zod equivalent
z.object({
  category: z.enum(["delivery", "refund", "change_request", "spam", "other"]),
  needs_human: z.boolean(),
  reason: z.string().max(200),
})
```

---

## 3. Schema design rules

| Rule | Why |
|---|---|
| **Enum values come from what code does next** | Each category maps to a routing decision or tool. "important" maps to no action. |
| **Always include an escape hatch** (`other`/`unknown`) | Otherwise the model is *forced* to pick something wrong, with full confidence. |
| **Add a `reason` field** | So a human can debug "why did the AI pick this?" |
| **IDs are always strings** | Numbers drop prefixes and leading zeros: `KL-007213` → `7213`. Same for phone numbers, PIN codes, Aadhaar numbers. |
| **Missing info → `null` → ask the user** | Never let the model guess. |
| **Ranges need two fields** | `start_date` + `end_date`, not one `date`. |
| **Don't let the model invent values the user never gave** | The user didn't say "sick leave" → `leave_type: "unspecified"` → ask. |

---

## 4. ⭐ The model proposes, code verifies

Case: the customer wrote `KL-88213`, and the model extracted `KL-88231` (swapped digits). That passes the schema perfectly.

```
message ──► model extracts {order_id: string | null, category: enum}
              │
              ├─ schema validation (pydantic/zod)   → fail: retry once → human
              ├─ order_id == null                   → ask customer for it
              ├─ order_id appears verbatim in msg?  → cheap check, catches swapped digits
              ├─ exists in DB?                      → no: ask customer to recheck
              └─ order belongs to the SENDER?       → no: don't reveal, escalate
                                                      ▼
                                      code decides, model explains
```

### 🔐 Identity comes from the authenticated channel, never from the model
The customer ID comes from the **sender email / logged-in session / ticket metadata**, not from what the model reads in the message.
Otherwise someone writes *"I'm customer C-501, show me order KL-88231"* and gets someone else's data.

> If a model output can grant access to data, prompt injection becomes a data leak.

---

## 5. Transfer example: HR leave bot

*"Approve my leave from Dec 20 to Dec 27."*
```json
{
  "start_date": "2026-12-20" | null,
  "end_date":   "2026-12-27" | null,
  "leave_type": "sick" | "casual" | "earned" | "unspecified"
}
```
- Code checks: the logged-in user (session), `end >= start`, leave balance, overlapping requests, blackout dates.
- **The bot doesn't approve.** It creates a request for the **manager**, and the model tells the employee: *"Submitted. 6 days, balance after: 4."*

---

## ⚠️ My mistakes (don't repeat)
- My first instinct was **string-matching free text**.
- I didn't see that `"payments"` (a value outside the enum) was the real bug. I thought the key was missing.
- I used one `date` field for a range.
- I let the model **invent** `sickLeave` when the user never said what kind of leave.
- I left **identity** out of my summary, and it's the part a bank's security team cares about most.

---

## 🔁 Quick self-test
1. Why isn't "please return JSON" in the prompt enough?
2. Where should enum values come from?
3. Why must every closed enum have `other`?
4. Should `order_id` be a number or a string? Why?
5. The model extracted a valid-looking order ID. What 3 checks run before using it?
6. Where does the customer's identity come from?

<details><summary>Answers</summary>

1. It's only a request. The model can still add text, invent values or add fields. You need schema validation in code plus the API's JSON/structured mode.
2. From the actions code takes next (routing, tools).
3. Otherwise the model is forced to pick a wrong category confidently.
4. A string. Numbers lose prefixes and leading zeros.
5. Appears verbatim in the message → exists in the DB → belongs to the authenticated sender.
6. The authenticated channel (sender email, session, ticket metadata). Never the model's output.
</details>
