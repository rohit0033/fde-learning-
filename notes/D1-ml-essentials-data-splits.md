# D1 · ML Essentials I: Data, Splits, Training
*2026-11-18 · Revision notes · Roadmap Step 1*

---

## 1. ⭐ Train / validation / test
| Set | Analogy | Rule |
|---|---|---|
| **Train** | Studying | The model learns from it |
| **Validation (dev)** | Mock test | Tune on it as often as you like |
| **Test** | Final exam | **Locked. Run ONCE at the end. Change nothing after.** |

**The moment you tune on the test set, it becomes a validation set.**

### My Week 1 mistake
I tuned the prompt *while looking at* the 30 emails, then reported "43% automation" on **the same 30** → that was a **validation** number, **too optimistic**. Fitting too closely to what you tuned on = **overfitting**.

### ⭐ An honest test set
1. A **random sample of REAL emails** from Kirana (e.g. 200 from last month, PII removed). **Not written by me**: I'd unconsciously write clean emails that fit my own categories. Real traffic is messy (Hinglish, typos, multi-intent, angry threads). A self-written set is **not representative of the real data distribution**.
2. Labeled by **Kirana's support leads**, not by me.
3. **Stratified split**: split *within each category*. If only 8 legal notices exist and all 8 land in dev, the test never checks the riskiest category.
4. Lock it. Run once. Report that number.

### ⭐ Prompt-based system = no training set
In emalify-v2 nothing is trained; I only tune the prompt. So:
- **Dev ~50%**: tune here
- **Test ~50%**: make it big, because with 30 test emails one mistake = 3%

**70/15/15 is for when you actually train a model** (fine-tuning, Week 7). Knowing when the textbook rule doesn't apply = the FDE skill.

---

## 2. ⭐ Bias vs variance
**The student analogy (mine):**
- **High bias = underfitting**: gets even the **practised** questions wrong. Didn't really learn, or the method is too simple.
- **High variance = overfitting**: perfect on practised questions, fails on **new** ones. Memorized instead of understood.

| | Symptom (my classifier) | Fix direction |
|---|---|---|
| **High variance** | Dev 97%, test 70% | More **general** rules (not "if it mentions Hubli hub..."), more varied dev examples |
| **High bias** | Dev 70%, test 70% | **First look at the failing emails.** Then: clearer or split categories · more information (examples, DB context like order status) · a stronger model (re-run the gate!) |

Not "add more rules" before knowing what fails.

---

## 3. Supervised vs unsupervised
- **Supervised** = has labels (`expected_category`) → my classifier
- **Unsupervised** = no labels → e.g. *"10,000 emails, what are customers writing about?"* → **clustering**
- **FDE use:** in discovery, **cluster real emails first** so categories come from data, not guesses.

---

## 4. Feature engineering + one-hot encoding
Old-school ML only understands **numbers**, so features must be actual numbers:
- ❌ "words" → ✅ **count of refund words** (refund, money back, charged twice)
- ✅ email length
- ❌ raw order ID (88214 isn't "more refund-ish" than 88213; IDs are arbitrary labels) → ✅ **`has_order_id` (0/1)**, or look it up → `days_since_delivery`, order status

### ⭐ Categories → one-hot, never 1, 2, 3, 4
`delivered=1, in_transit=2, returned=3, cancelled=4` → the model thinks cancelled is "4× delivered" and returned sits "between" in_transit and cancelled. Nonsense.

**One-hot** = one yes/no column per value:
```
          UPI  card  COD
COD order  0    0     1
```
Same reason **IDs are strings**: the label matters, not its size.

---

## 5. Epoch, batch, iteration
(Like BullMQ: process jobs in chunks, not one giant job.)
- **Batch** = a chunk of examples processed together
- **Iteration** = one batch → the model updates once
- **Epoch** = one full pass over **all** the training data

**Iterations = (examples ÷ batch size) × epochs**
- 1,000 ÷ 100 × 3 = **30**
- 2,000 ÷ 50 × 2 = **80**

**Too many epochs (e.g. 30)** → the model sees the same data repeatedly → memorizes → **high variance**.

---

## 6. Transfer: hospital X-ray vendor
*"98% accuracy, tested on the same 500 reports we built it with."*
Ask:
1. **Tested on which reports?** → it must be a **held-out** set of new reports never used while building
2. **Who labeled them?** → **doctors**, not the vendor
3. *(D2 preview)* **How many reports were actually urgent?** If only 2% are urgent, a model that **always says "not urgent" scores 98% accuracy** and catches **zero** emergencies. Accuracy alone can hide the cases that matter most → precision & recall, tomorrow.

---

## 7. 🔨 Build: honest split in emalify-v2
- `emails.json`: 50 emails (20 new messy ones), each with `expected_category` (the **answer key**) and `split` (`dev`/`test`)
- `split.py`: stratified 50/50, seed 42 → same split every run
- `classify.py --set dev` (default) · `--set test` (final exam, run once) · `classify.py 1 36` (debug)
- **Accuracy** = `r.category == e["expected_category"]`, i.e. does the model match the answer key?

| | Dev | Test |
|---|---|---|
| Accuracy | 100% | 100% |
| Automation | 44% | 48% |
| Automated but wrong | 0 | 0 |

### ⭐ What "100%" really means
It proves the model **agrees with OUR labels** on **emails WE wrote**. It doesn't prove it works on real emails, or that our labels match Kirana's.
**Get FROM Kirana:** real emails + labels by their support leads → run once → report that.

### Labeling lessons
- **#34** (late + consumer-court threat): `category` = **what** (delivery); `needs_human` = **how risky** (true). A legal threat changes *who handles it*, not *what it's about*.
- **#36** (slot change + refund): one `category` field can't hold two intents → **schema limitation**. Future fix: `categories: list[...]` or split into two tickets.
- **#40** (cancel unpaid COD): change_request vs refund → **Kirana decides** (question for the customer).

---

## ⚠️ My mistakes (don't repeat)
- My Week 1 "43%" was a **validation** number reported as a result.
- Quoted the article's **70/15/15** without checking that my system trains nothing.
- "Check for noise" was vague → the concrete check is a **stratified split**.
- High bias fix: said "stricter rules" before looking at failures, then gave **one** fix when asked for **two**.
- Summary: wrote **one** line when asked for **two**. **COUNT before sending.**
- Labeling: confused `category` with `needs_human` on #34; skipped #40 (count!).
- Said "send test results TO Kirana"; it's "get real emails + labels FROM Kirana."
- Didn't know why a raw order ID is a bad feature (arbitrary labels have no size).

## 🔁 Quick self-test
1. Why is a number from emails you tuned on "too optimistic"?
2. Why shouldn't you write the test emails yourself?
3. Dev 97%, test 70%: bias or variance? Fix?
4. Dev 70%, test 70%: bias or variance? What do you do first?
5. Why not encode statuses as 1, 2, 3, 4?
6. 5,000 examples, batch size 100, 4 epochs: how many iterations?
7. What's a stratified split, and why does it matter for rare categories?

<details><summary>Answers</summary>

1. The prompt was fitted to those exact emails (overfitting); new emails will do worse.
2. You'd write emails that fit your own categories. They aren't representative of real messy traffic.
3. Variance (overfitting). More general rules, more varied examples.
4. Bias. First look at the failing emails, then clearer categories / more context / a stronger model.
5. The model treats them as amounts (4 > 2, "between"). Use one-hot.
6. 5,000 ÷ 100 × 4 = 200.
7. Split within each category so rare ones (legal) appear in both dev and test.
</details>
