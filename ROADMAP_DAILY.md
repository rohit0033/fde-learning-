# FDE Daily Curriculum

> Merges the [Forward Deployed Engineer Roadmap](https://github.com/amitshekhariitbhu/forward-deployed-engineer-roadmap) by Amit Shekhar (Outcome School) with your 8-week plan (`FDE_PLAN.md`) and the FieldDesk capstone.

> **Run one command a day:** `/fde-tutor today`. Read the day's 📌 must-read articles (~20 min, usually 2), then the tutor tests and deepens them and teaches the rest of the day's roadmap topics to you through Socratic questions, sets the build task, writes your notes and moves you to the next day.

## Daily rhythm (Mon-Fri, ~2.5-3 h)

| Block | Time | What |
|---|---|---|
| 0. 📌 Read | ~20 min | The day's 📌 must-read articles (usually 2). Videos and the other links are optional. |
| 1. Session | 45-60 min | `/fde-tutor today`: starts from the must-reads, then teaches the rest of the day's topics by asking you questions, applied to Kirana and your own code. |
| 2. Build | 1-2 h | The day's build task (feeds the capstone). |
| 3. Revise | 5 min | Skim the notes file the tutor wrote for that day. |

**Sat** = build/ship day · **Sun** = review + drill. Missed a day? Don't skip: just run `/fde-tutor today` and it continues from where you are. The dates are targets, not deadlines.

**Already covered in Week 1 (go fast on these):** temperature, structured outputs, prompt caching, reasoning-model cost, prompt injection, guardrails in code.


---

## Week 1 wrap-up

### D0 · Sun 15 Nov · 🔁 Week 1 wrap-up + the big picture
**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 0: Must Know*
- [x] [AI Engineering Explained: LLM, RAG, MCP, Agent, Fine-Tuning, Quantization](https://www.youtube.com/watch?v=lnfWvX66FUk) 🎥

**Questions we'll work through:**
- Explain LLM / RAG / MCP / agent / fine-tuning / quantization to Kirana's VP in one sentence each.
- A customer asks 'RAG or fine-tuning?' What do you ask them first?

**Do:** `/fde-tutor review` (Week 1 quiz). Push emalify-v2 to GitHub (check `git status` shows no .env/logs).


---

## Week 2: Foundations: ML essentials, how LLMs work, choosing models (Roadmap Steps 1-3)

### D1 · Mon 16 Nov · 📖 ML essentials I: data, splits, training
📌 **Read before the session (~20 min).** The session starts from these:
- [x] **[Why do we split data into train, validation, and test sets?](https://outcomeschool.com/blog/train-validation-test-split)**  *(Step 1)*
- [x] **[How does the Bias-Variance Tradeoff work?](https://outcomeschool.com/blog/bias-variance-tradeoff)**  *(Step 1)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 1: AI and Machine Learning Essentials*
- [x] [What is Machine Learning?](https://outcomeschool.com/blog/machine-learning)
- [x] [Supervised vs Unsupervised Learning](https://outcomeschool.com/blog/supervised-vs-unsupervised-learning)
- [x] [What is Feature Engineering in Machine Learning?](https://outcomeschool.com/blog/feature-engineering)
- [x] [Feature Engineering in Machine Learning](https://www.youtube.com/watch?v=QLlywrWuXag) 🎥
- [x] [What is One-hot Encoding in Machine Learning?](https://outcomeschool.com/blog/one-hot-encoding)
- [x] [One-hot Encoding in Machine Learning](https://www.youtube.com/watch?v=6AmedU5i9go) 🎥
- [x] [What are Epoch, Batch, Batch Size, and Iteration in Machine Learning?](https://outcomeschool.com/blog/epoch-batch-and-iteration)
- [x] [Epoch, Batch, Batch Size, Iteration](https://www.youtube.com/watch?v=NFLlXE-6vno) 🎥

**Questions we'll work through:**
- Your 30 Kirana emails: are they training data, validation data or test data? What breaks if you tune your prompt on them and also report results on them?
- Bias vs variance in plain words, using a support-ticket classifier.

**Do:** Split emalify-v2 emails into a 'dev' set (tune prompts on it) and a held-out 'test' set (only report on it). Add 20 new emails so test has 20+.

### D2 · Tue 17 Nov · 📖 ML essentials II: precision, recall, neural nets
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[Precision vs Recall](https://outcomeschool.com/blog/precision-vs-recall)**  *(Step 1)*
- [ ] **[What is a Neural Network and How Does It Work?](https://outcomeschool.com/blog/neural-network)**  *(Step 1)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 1: AI and Machine Learning Essentials*
- [ ] [What are Activation Functions in Neural Networks? Sigmoid, Tanh, ReLU, and Softmax Explained](https://outcomeschool.com/blog/activation-functions)
- [ ] [What is the Softmax Function and How Does It Work?](https://outcomeschool.com/blog/softmax-function)
- [ ] [Softmax Activation Function in Machine Learning](https://www.youtube.com/watch?v=2Zx6x01WwWM) 🎥
- [ ] [What are Logits in Machine Learning?](https://outcomeschool.com/blog/logits-in-machine-learning)
- [ ] [How Does Gradient Descent Work?](https://outcomeschool.com/blog/math-behind-gradient-descent)
- [ ] [What is Reinforcement Learning?](https://outcomeschool.com/blog/reinforcement-learning)

**Questions we'll work through:**
- 'Automated-but-wrong' is a precision problem or a recall problem? For which class?
- Logits → softmax → probability: where could a 'confidence' number for needs_human come from?

**Do:** Add per-category precision & recall to the emalify-v2 report.

### D3 · Wed 18 Nov · 📖 How LLMs work I: tokens and embeddings
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[Tokenization in LLMs](https://outcomeschool.com/blog/tokenization-in-llms)**  *(Step 2)*
- [ ] **[What are Embeddings?](https://outcomeschool.com/blog/what-are-embeddings)**  *(Step 2)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 2: How LLMs Work*
- [ ] [What is Generative AI?](https://outcomeschool.com/blog/what-is-generative-ai)
- [ ] [How does an LLM work?](https://outcomeschool.com/blog/large-language-model-llm)
- [ ] [What are Autoregressive Models?](https://outcomeschool.com/blog/autoregressive-models)
- [ ] [How does Pretraining work?](https://outcomeschool.com/blog/llm-pretraining)
- [ ] [Tokenization in Large Language Models (LLMs)](https://www.youtube.com/watch?v=sK2s9I84EVI) 🎥
- [ ] [What is Byte Pair Encoding (BPE) in LLMs?](https://outcomeschool.com/blog/bpe-in-llms)
- [ ] [Embeddings in Machine Learning](https://www.youtube.com/watch?v=LedXW6xl21s) 🎥
- [ ] [How does Cosine Similarity work?](https://outcomeschool.com/blog/cosine-similarity)

**Questions we'll work through:**
- Why does Hinglish ('bhai mera order abhi tak nahi aaya') cost more tokens than English?
- Cosine similarity of two emails: what does a high score mean and NOT mean?

**Do:** Count tokens of your system prompt vs one email (tiktoken or the provider's tokenizer). Embed 5 emails and print their cosine similarities.

### D4 · Thu 19 Nov · 📖 How LLMs work II: transformers, decoding, sampling
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[How Does the Transformer Architecture Work?](https://outcomeschool.com/blog/decoding-transformer-architecture)**  *(Step 2)*
- [ ] **[What is Self Attention in Transformers?](https://outcomeschool.com/blog/self-attention-in-transformers)**  *(Step 2)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 2: How LLMs Work*
- [ ] [Evolution of LLM Architecture](https://outcomeschool.com/blog/evolution-of-llm-architecture)
- [ ] [How do Greedy Decoding and Beam Search differ?](https://outcomeschool.com/blog/greedy-decoding-vs-beam-search)
- [ ] [How does Temperature control LLM output?](https://outcomeschool.com/blog/how-does-temperature-control-llm-output)
- [ ] [How do Top-k and Top-p Sampling work?](https://outcomeschool.com/blog/how-do-top-k-and-top-p-sampling-work)
- [ ] [Stop Tokens in LLMs](https://outcomeschool.com/blog/stop-tokens-in-llms)
- [ ] [What are Log Probabilities (Logprobs) in LLMs?](https://outcomeschool.com/blog/logprobs-in-llms)
- [ ] [How does Token Streaming work?](https://outcomeschool.com/blog/how-does-token-streaming-work)

**Questions we'll work through:**
- Why is temperature=0 'almost' deterministic and not fully?
- Could logprobs replace the model's own needs_human flag? What's the risk?

**Do:** Request logprobs (if your provider supports it) for the category token; log them next to correct/incorrect results.

### D5 · Fri 20 Nov · 📖 Context limits, hallucination + choosing models
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[Why Do LLMs Hallucinate? The Token-Level Explanation](https://outcomeschool.com/blog/why-do-llms-hallucinate-the-token-level-explanation)**  *(Step 2)*
- [ ] **[What is LLM Routing? How to Send Each Query to the Right LLM](https://outcomeschool.com/blog/llm-routing)**  *(Step 3)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 2: How LLMs Work*
- [ ] [How does the Context Window work?](https://outcomeschool.com/blog/context-window)
- [ ] [Why is the context window limited in LLMs?](https://www.youtube.com/watch?v=CGIhxIaOg3M) 🎥
- [ ] [What is the Lost in the Middle Problem in LLMs?](https://outcomeschool.com/blog/lost-in-the-middle-problem-in-llms)
*Step 3: Choosing the Right Model for the Customer*
- [ ] [What are Small Language Models (SLMs)?](https://outcomeschool.com/blog/small-language-models-slms)
- [ ] [What are Large Reasoning Models (LRMs)?](https://outcomeschool.com/blog/large-reasoning-models)
- [ ] [What is Mixture of Experts (MoE)?](https://outcomeschool.com/blog/mixture-of-experts)
- [ ] [What is Multimodal AI?](https://outcomeschool.com/blog/multimodal-ai)
- [ ] [How does a Vision-Language Model (VLM) work?](https://outcomeschool.com/blog/vision-language-model-vlm)

**Questions we'll work through:**
- Lost in the middle: where in a long prompt would you put Kirana's refund policy?
- Design a router: which Kirana emails could a small model handle, which need a bigger one? How would you prove the router is safe?

**Do:** Read-only day: sketch a routing design (small model first, escalate on invalid/low confidence).

### D6 · Sat 21 Nov · 🔨 BUILD + SHIP

**Do:** Implement the router in emalify-v2, run gate-then-optimize eval (automated-but-wrong gate). Finish README with before/after numbers. Write the blog post.

### D7 · Sun 22 Nov · 🔁 Review + customer drill

**Do:** `/fde-tutor review` then `/fde-tutor drill customer`.


---

## Week 3: Prompting + RAG on customer data (Roadmap Steps 4-5)

### D8 · Mon 23 Nov · 📖 Prompt & context engineering
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[What is Context Engineering?](https://outcomeschool.com/blog/context-engineering)**  *(Step 4)*
- [ ] **[How does Context Compaction work?](https://outcomeschool.com/blog/how-does-context-compaction-work)**  *(Step 4)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 4: Prompt Engineering and Context Engineering*
- [ ] [How does Prompt Engineering work?](https://outcomeschool.com/blog/prompt-engineering)
- [ ] [How does Chain-of-Thought (CoT) Prompting work?](https://outcomeschool.com/blog/how-does-chain-of-thought-prompting-work)
- [ ] [How does Prompt Chaining work?](https://outcomeschool.com/blog/how-does-prompt-chaining-work)
- [ ] [How does Tree of Thoughts work?](https://outcomeschool.com/blog/how-does-tree-of-thoughts-work)
- [ ] [How does Prompt Caching work?](https://outcomeschool.com/blog/how-does-prompt-caching-work)

**Questions we'll work through:**
- Chain-of-thought vs a reasoning model: when would you pay for either on Kirana tickets?
- Context engineering: what goes in the context for a ticket about order KL-88213, and what stays out?

**Do:** Rewrite the emalify-v2 prompt as a prompt chain (classify → extract order_id). Measure on the dev set only.

### D9 · Tue 24 Nov · 📖 RAG I: retrieval foundations
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[How does RAG work?](https://outcomeschool.com/blog/retrieval-augmented-generation-rag)**  *(Step 5)*
- [ ] **[How does Approximate Nearest Neighbor (ANN) Search work?](https://outcomeschool.com/blog/how-does-approximate-nearest-neighbor-ann-search-work)**  *(Step 5)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 5: RAG on Customer Data*
- [ ] [How does a Vector Database work?](https://outcomeschool.com/blog/how-does-a-vector-database-work)
- [ ] [How does Semantic Search work?](https://outcomeschool.com/blog/how-does-semantic-search-work)
- [ ] [How does an Inverted Index work?](https://outcomeschool.com/blog/inverted-index)

**Questions we'll work through:**
- Your Elasticsearch work at Outbox: which of today's ideas did you already use without the name?
- Exact-match SKU 'KL-88213': semantic search or inverted index? Why?

**Do:** Collect/write 10-15 Kirana SOP docs (refund policy, delivery SLAs, address change rules). Start the `fielddesk` repo.

### D10 · Wed 25 Nov · 📖 RAG II: hybrid search, reranking, chunking
📌 **Read before the session (~30 min).** The session starts from these:
- [ ] **[How does Hybrid Search work?](https://outcomeschool.com/blog/how-does-hybrid-search-work)**  *(Step 5)*
- [ ] **[How does a Reranker work?](https://outcomeschool.com/blog/how-does-a-reranker-work)**  *(Step 5)*
- [ ] **[How to Chunk Documents for RAG? Chunking Strategies Explained](https://outcomeschool.com/blog/chunking-strategies-for-rag)**  *(Step 5)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 5: RAG on Customer Data*
- [ ] [How does Contextual Retrieval work?](https://outcomeschool.com/blog/how-does-contextual-retrieval-work)

**Questions we'll work through:**
- A refund policy table gets split across two chunks. What does the customer see?
- When is a reranker worth its latency?

**Do:** Chunk the SOPs 2 ways; build hybrid search (pgvector + BM25/Elasticsearch).

### D11 · Thu 26 Nov · 📖 RAG III: query-side tricks + caching
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[How do Query Rewriting and Multi-Query Retrieval work?](https://outcomeschool.com/blog/how-do-query-rewriting-and-multi-query-retrieval-work)**  *(Step 5)*
- [ ] **[How does Semantic Caching work?](https://outcomeschool.com/blog/how-does-semantic-caching-work)**  *(Step 5)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 5: RAG on Customer Data*
- [ ] [How does HyDE work in RAG?](https://outcomeschool.com/blog/how-does-hyde-work)
- [ ] [What is ColBERT? Late Interaction Retrieval Explained](https://outcomeschool.com/blog/decoding-colbert)
- [ ] [How do Image Embeddings work?](https://outcomeschool.com/blog/how-do-image-embeddings-work)
- [ ] [How does an Embedding Cache work?](https://outcomeschool.com/blog/how-does-an-embedding-cache-work)

**Questions we'll work through:**
- 'the one I ordered Tuesday': which query technique helps, and which can't (because the answer is in a DB, not docs)?
- Semantic cache on support answers: what's the danger for order-specific questions?

**Do:** Write 50 question→correct-chunk pairs; measure recall@5 for each chunking + hybrid vs vector-only.

### D12 · Fri 27 Nov · 📖 RAG IV: agentic, graph, vectorless RAG
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[What is Agentic RAG?](https://outcomeschool.com/blog/agentic-rag)**  *(Step 5)*
- [ ] **[What is GraphRAG? How Knowledge Graphs Improve RAG](https://outcomeschool.com/blog/graphrag)**  *(Step 5)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 5: RAG on Customer Data*
- [ ] [Agentic RAG Explained](https://www.youtube.com/watch?v=6nSegpuWJVw) 🎥
- [ ] [What is Vectorless RAG? RAG Without Embeddings or a Vector Database](https://outcomeschool.com/blog/vectorless-rag)

**Questions we'll work through:**
- When does Kirana need agentic RAG instead of one retrieval call?
- Would GraphRAG help a logistics company? Name a concrete question it answers better.

**Do:** Add a reranker; update the recall@k table in the README.

### D13 · Sat 28 Nov · 🔨 BUILD

**Do:** FieldDesk knowledge layer done: ingestion → hybrid retrieval → rerank, with a retrieval benchmark table.

### D14 · Sun 29 Nov · 🔁 Review + customer drill

**Do:** `/fde-tutor review` then `/fde-tutor drill customer` (scenario: 'our chatbot gives wrong answers').


---

## Week 4: Evals, safety, agents I (Roadmap Steps 8, 9, 6)

### D15 · Mon 30 Nov · 📖 Evals I: metrics and LLM-as-judge
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[What is LLM Evaluation? Metrics, Benchmarks, and Methods Explained](https://outcomeschool.com/blog/llm-evaluation)**  *(Step 8)*
- [ ] **[What is LLM as a Judge?](https://outcomeschool.com/blog/llm-as-a-judge)**  *(Step 8)*


**Questions we'll work through:**
- Your judge model agrees with your labels 80% of the time. Is that good? How do you find out?
- Which Kirana checks need a judge, and which should be plain code?

**Do:** Turn emalify-v2's report into an eval harness: JSONL golden set, deterministic checks, one LLM-judge check (reason quality).

### D16 · Tue 01 Dec · 📖 Evals II: agent evals + observability
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[How to Evaluate AI Agents? Metrics, Methods, and Best Practices](https://outcomeschool.com/blog/ai-agent-evaluation)**  *(Step 8)*
- [ ] **[What is AI Agent Observability? Traces, Spans, and Metrics Explained](https://outcomeschool.com/blog/ai-agent-observability)**  *(Step 8)*


**Questions we'll work through:**
- How do you evaluate a multi-step agent trajectory, not just its final answer?
- Traces and spans: what would you want to see for a ticket that got a wrong refund decision?

**Do:** Add tracing (spans per LLM call / tool call) to emalify-v2 or FieldDesk.

### D17 · Wed 02 Dec · 📖 Safety, security and trust
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[How do LLM Guardrails work?](https://outcomeschool.com/blog/how-do-llm-guardrails-work)**  *(Step 9)*
- [ ] **[What is Prompt Injection in LLMs and How Do We Defend Against It?](https://outcomeschool.com/blog/prompt-injection-in-llms)**  *(Step 9)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 9: AI Safety, Security, and Trust*
- [ ] [What is jailbreaking in LLMs?](https://outcomeschool.com/blog/jailbreaking-in-llms)
- [ ] [How does LLM Watermarking work?](https://outcomeschool.com/blog/how-does-llm-watermarking-work)

**Questions we'll work through:**
- Guardrails: which belong before the model, which after, which in code?
- Your #18 injection got through after a prompt change. Write the regression test that makes sure it never silently passes again.

**Do:** Add 10 injection/jailbreak cases to the golden set; they must route to human.

### D18 · Thu 03 Dec · 📖 Agents I: function calling, loops, ReAct
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[How does Function Calling work in LLMs?](https://outcomeschool.com/blog/how-does-function-calling-work-in-llms)**  *(Step 6)*
- [ ] **[What is an AI Agent Loop?](https://outcomeschool.com/blog/ai-agent-loop)**  *(Step 6)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 6: AI Agents and Tool Integration*
- [ ] [What is an AI Agent? How It Works](https://outcomeschool.com/blog/ai-agent)
- [ ] [What is a ReAct Agent?](https://outcomeschool.com/blog/react-agent)

**Questions we'll work through:**
- What should an agent NEVER be allowed to do without a human at Kirana?
- Tool design: why do tool names, schemas and error messages matter as much as the prompt?

**Do:** Write an agent loop from scratch in Python (no framework) with 2 fake tools.

### D19 · Fri 04 Dec · 📖 Agents II: planning, reflection, human-in-the-loop, memory
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[How do Human-in-the-Loop agents work?](https://outcomeschool.com/blog/human-in-the-loop-agents)**  *(Step 6)*
- [ ] **[How does AI Agent Memory work?](https://outcomeschool.com/blog/ai-agent-memory)**  *(Step 6)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 6: AI Agents and Tool Integration*
- [ ] [What is a Plan-and-Execute Agent?](https://outcomeschool.com/blog/plan-and-execute-agent)
- [ ] [What is a Reflection Agent?](https://outcomeschool.com/blog/reflection-agent)
- [ ] [How does ChatGPT remember you?](https://outcomeschool.com/blog/how-does-chatgpt-remember-you)

**Questions we'll work through:**
- Plan-and-execute vs ReAct for 'refund + address change' in one ticket?
- What should a support agent remember across tickets, and what must it forget (PII)?

**Do:** Add a human-approval step for `issue_refund` to your loop.

### D20 · Sat 05 Dec · 🔨 BUILD

**Do:** Eval harness runs in GitHub Actions on every PR and fails on regression (automated-but-wrong gate).

### D21 · Sun 06 Dec · 🔁 Review + decomposition drill

**Do:** `/fde-tutor review` then `/fde-tutor drill case` ('handle 40% of support tickets with AI in 90 days').


---

## Week 5: MCP, multi-agent, agentic engineering, integration (Roadmap Steps 6-7)

### D22 · Mon 07 Dec · 📖 MCP, agent skills, OKF
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[What is MCP (Model Context Protocol)?](https://outcomeschool.com/blog/what-is-mcp-model-context-protocol)**  *(Step 6)*
- [ ] **[What are Agent Skills?](https://outcomeschool.com/blog/what-are-agent-skills)**  *(Step 6)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 6: AI Agents and Tool Integration*
- [ ] [What is OKF (Open Knowledge Format)?](https://outcomeschool.com/blog/what-is-okf-open-knowledge-format)

**Questions we'll work through:**
- MCP server vs a plain REST API for Kirana's order system: what does MCP add?
- Auth: whose identity does an MCP tool call run as?

**Do:** Expose `lookup_order` and `check_refund_policy` as an MCP server.

### D23 · Tue 08 Dec · 📖 Multi-agent systems and computer/browser agents
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[What are Multi-Agent Systems?](https://outcomeschool.com/blog/multi-agent-systems)**  *(Step 6)*
- [ ] **[What are AI SubAgents?](https://outcomeschool.com/blog/ai-subagents)**  *(Step 6)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 6: AI Agents and Tool Integration*
- [ ] [How AI Agents Communicate](https://outcomeschool.com/blog/how-ai-agents-communicate)
- [ ] [What is AI Orchestration?](https://outcomeschool.com/blog/ai-orchestration)
- [ ] [How do Computer-Use Agents work?](https://outcomeschool.com/blog/how-do-computer-use-agents-work)
- [ ] [How do Browser Agents work?](https://outcomeschool.com/blog/how-do-browser-agents-work)

**Questions we'll work through:**
- When are sub-agents worth the extra cost and failure points?
- Kirana's legacy portal has no API. Browser agent or ask IT for an export? Trade-offs?

**Do:** Design doc only: does FieldDesk need multiple agents? Justify with failure modes.

### D24 · Wed 09 Dec · 📖 Agentic engineering: harness, loop, graph
📌 **Read before the session (~10 min).** The session starts from these:
- [ ] **[What is Harness Engineering?](https://outcomeschool.com/blog/harness-engineering-in-ai)**  *(Step 7)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 7: Agentic Engineering and Building Fast with Coding Agents*
- [ ] [What is Loop Engineering?](https://outcomeschool.com/blog/what-is-loop-engineering)
- [ ] [What is Graph Engineering?](https://outcomeschool.com/blog/what-is-graph-engineering)

**Questions we'll work through:**
- What is the 'harness' around your FieldDesk agent, concretely?
- Loop vs graph: which fits ticket triage?

**Do:** Refactor your agent loop: explicit state, max steps, timeouts, logging.

### D25 · Thu 10 Dec · 📖 Frameworks and coding agents
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[How does LangGraph work?](https://outcomeschool.com/blog/how-does-langgraph-work)**  *(Step 7)*
- [ ] **[How does Claude Code work?](https://outcomeschool.com/blog/how-does-claude-code-work)**  *(Step 7)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 7: Agentic Engineering and Building Fast with Coding Agents*
- [ ] [How does LangChain work?](https://outcomeschool.com/blog/how-does-langchain-work)
- [ ] [How does Cursor work?](https://outcomeschool.com/blog/how-does-cursor-work)

**Questions we'll work through:**
- You removed LangChain in Week 1. When WOULD you choose LangGraph at a customer?
- How do you use Claude Code/Cursor at a customer site without leaking their code or data?

**Do:** Rebuild one small piece in LangGraph and compare (lines of code, debuggability).

### D26 · Fri 11 Dec · 📖 Enterprise integration (not in roadmap; FDE core)

**Questions we'll work through:**
- A webhook arrives twice and out of order. What does your system do?
- OAuth vs SSO/OIDC: what does Kirana's IT team actually ask you for?
- Two-way sync between FieldDesk and their helpdesk: who wins a conflict?

**Do:** Read DDIA ch.11 (streams) summary. Add idempotency keys + webhook signature checks to FieldDesk's ingestion.

### D27 · Sat 12 Dec · 🔨 BUILD

**Do:** FieldDesk agent: tools (lookup_order, check_refund_policy, draft_reply, escalate, issue_refund with approval) via your MCP server, evaluated in CI.

### D28 · Sun 13 Dec · 🔁 Review + incident drill

**Do:** `/fde-tutor review` then `/fde-tutor drill incident`.


---

## Week 6: Latency, cost, serving, system design, deployment (Roadmap Steps 10, 12)

### D29 · Mon 14 Dec · 📖 Inference I: prefill, decode, KV cache
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[Prefill vs Decode: LLM Inference Optimization](https://outcomeschool.com/blog/prefill-vs-decode-llm-inference-optimization)**  *(Step 10)*
- [ ] **[What is KV Cache in LLMs?](https://outcomeschool.com/blog/kv-cache-in-llms)**  *(Step 10)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 10: Latency and Cost in Production*
- [ ] [LLM Inference Optimization](https://outcomeschool.com/blog/llm-inference-optimization)
- [ ] [LLM Inference Optimization](https://www.youtube.com/watch?v=jV2sCj4lHYk) 🎥
- [ ] [The First-Token Latency Problem in LLMs](https://www.youtube.com/watch?v=XD8DD4cEHu0) 🎥
- [ ] [How does an LLM use GPU memory?](https://outcomeschool.com/blog/llm-gpu-memory)

**Questions we'll work through:**
- Your p95 was 20s on Gemini. Prefill or decode? How would you tell?
- Why does a long system prompt hurt time-to-first-token, and how does caching help?

**Do:** Measure time-to-first-token vs total time with streaming in FieldDesk.

### D30 · Tue 15 Dec · 📖 Inference II: batching, paged attention, speculative decoding
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[What is Continuous Batching in LLMs?](https://outcomeschool.com/blog/continuous-batching-in-llms)**  *(Step 10)*
- [ ] **[What is Speculative Decoding?](https://outcomeschool.com/blog/speculative-decoding)**  *(Step 10)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 10: Latency and Cost in Production*
- [ ] [What is Paged Attention in LLMs?](https://outcomeschool.com/blog/paged-attention-in-llms)
- [ ] [What is Prefill-Decode Disaggregation in LLM Inference?](https://outcomeschool.com/blog/prefill-decode-disaggregation)

**Questions we'll work through:**
- Why can a provider serve you cheaper at high volume? Explain to a CFO.
- Speculative decoding: what does it change for the user, and what doesn't it change?

**Do:** Read-only + write a 1-page 'why our latency varies' explainer for Kirana.

### D31 · Wed 16 Dec · 📖 Quantization and self-hosting
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[How does Model Quantization work?](https://outcomeschool.com/blog/how-does-model-quantization-work)**  *(Step 10)*
- [ ] **[How does vLLM work?](https://outcomeschool.com/blog/how-does-vllm-work)**  *(Step 10)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 10: Latency and Cost in Production*
- [ ] [How does GGUF work?](https://outcomeschool.com/blog/how-does-gguf-work)
- [ ] [How does llama.cpp run LLMs on everyday hardware?](https://outcomeschool.com/blog/how-does-llama-cpp-run-llms-on-everyday-hardware)
- [ ] [How does Ollama work?](https://outcomeschool.com/blog/how-does-ollama-work)
- [ ] [How does SGLang work?](https://outcomeschool.com/blog/how-does-sglang-work)
- [ ] [How does TensorRT-LLM work?](https://outcomeschool.com/blog/how-does-tensorrt-llm-work)

**Questions we'll work through:**
- Kirana says 'data can't leave our servers'. Which of today's tools do you reach for, and what accuracy do you lose?
- vLLM vs Ollama: which for a demo, which for production?

**Do:** Run a small quantized model locally with Ollama on your dev set; compare with the gate-then-optimize table.

### D32 · Thu 17 Dec · 📖 AI system design and infrastructure
📌 **Read before the session (~30 min).** The session starts from these:
- [ ] **[How does Model Serving work?](https://outcomeschool.com/blog/model-serving)**  *(Step 12)*
- [ ] **[How does a GPU work for Deep Learning?](https://outcomeschool.com/blog/how-does-a-gpu-work-for-deep-learning)**  *(Step 12)*
- [ ] **[Cloud vs On-device Model Deployment](https://outcomeschool.com/blog/cloud-vs-on-device-model-deployment)**  *(Step 12)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 12: AI System Design and Infrastructure*
- [ ] [AI System Design](https://github.com/amitshekhariitbhu/ai-system-design)
- [ ] [How do CUDA Kernels work?](https://outcomeschool.com/blog/how-do-cuda-kernels-work)
- [ ] [How does a Google TPU work?](https://outcomeschool.com/blog/how-does-a-google-tpu-work)
- [ ] [How does an LPU work?](https://outcomeschool.com/blog/how-does-an-lpu-work)

**Questions we'll work through:**
- Draw FieldDesk end to end on a whiteboard: where are the trust boundaries?
- Cloud vs on-device vs customer GPUs: what 3 questions decide it?

**Do:** Architecture diagram + ADR (architecture decision record) for FieldDesk's deployment.

### D33 · Fri 18 Dec · 📖 Enterprise deployment: VPC, PII, audit (not in roadmap; FDE core)

**Questions we'll work through:**
- 'IT won't let data leave our VPC.' Give 3 deployment options with trade-offs.
- What does 'secure' mean to a bank's CISO vs to you?

**Do:** Add PII redaction before logging + an audit log for every automated action.

### D34 · Sat 19 Dec · 🔨 BUILD

**Do:** Deploy FieldDesk: Docker Compose, one cloud target, basic Terraform, tracing + cost/latency dashboard. Live demo URL.

### D35 · Sun 20 Dec · 🔁 Review + security-head drill

**Do:** `/fde-tutor review` then `/fde-tutor drill customer` (stakeholder: skeptical IT/security head).


---

## Week 7: Fine-tuning, voice agents, capstone polish (Roadmap Steps 11, 13)

### D36 · Mon 21 Dec · 📖 Fine-tuning and customizing models
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[How does Fine-Tuning work?](https://outcomeschool.com/blog/how-does-fine-tuning-work)**  *(Step 11)*
- [ ] **[What is LoRA (Low-Rank Adaptation)?](https://outcomeschool.com/blog/lora-low-rank-adaptation-of-llms)**  *(Step 11)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 11: Fine-Tuning and Customizing Models*
- [ ] [How does Prefix Tuning work?](https://outcomeschool.com/blog/how-does-prefix-tuning-work)
- [ ] [How does Knowledge Distillation work?](https://outcomeschool.com/blog/how-does-knowledge-distillation-work)
- [ ] [What is Continual Learning in LLMs? Solving Catastrophic Forgetting](https://outcomeschool.com/blog/continual-learning-in-llms)
- [ ] [What is RLHF? Reinforcement Learning from Human Feedback Explained](https://outcomeschool.com/blog/reinforcement-learning-from-human-feedback-rlhf)
- [ ] [What is Direct Preference Optimization (DPO)?](https://outcomeschool.com/blog/direct-preference-optimization-dpo)

**Questions we'll work through:**
- Customer: 'Should we fine-tune on our 50k old tickets?' Walk through your decision.
- Distillation: how could Kirana get a cheap model that behaves like the expensive one, and how do you prove it with your evals?

**Do:** Write the 'RAG vs fine-tuning vs prompt' decision memo for Kirana (1 page).

### D37 · Tue 22 Dec · 📖 Voice agents I: architecture and turn-taking
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[Design a Real-Time Voice AI Agent](https://outcomeschool.com/blog/design-a-real-time-voice-ai-agent)**  *(Step 13)*
- [ ] **[Cascaded vs Speech-to-Speech: How to choose the right voice agent architecture?](https://outcomeschool.com/blog/cascaded-vs-speech-to-speech)**  *(Step 13)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 13: Customer Use Case: Real-Time Voice AI Agent*
- [ ] [How do half-duplex and full-duplex voice agents differ?](https://outcomeschool.com/blog/half-duplex-vs-full-duplex-voice-agents)
- [ ] [How do WebRTC and WebSocket differ for voice AI agents?](https://outcomeschool.com/blog/webrtc-vs-websocket-for-voice-ai)
- [ ] [What is turn-taking in a voice AI agent?](https://outcomeschool.com/blog/what-is-turn-taking-in-a-voice-ai-agent)
- [ ] [How does endpointing decide when the user has finished speaking?](https://outcomeschool.com/blog/endpointing-in-voice-agents)
- [ ] [How do silence-based and model-based turn detection differ?](https://outcomeschool.com/blog/silence-vs-model-based-turn-detection)
- [ ] [How does dynamic endpointing adapt to how fast a user talks?](https://outcomeschool.com/blog/dynamic-endpointing)

**Questions we'll work through:**
- Kirana wants a phone line for 'where is my order'. Cascaded or speech-to-speech?
- Why is endpointing harder for an order number than for a sentence?

**Do:** Sketch a voice version of FieldDesk with a latency budget.

### D38 · Wed 23 Dec · 📖 Voice agents II: interruptions and barge-in
📌 **Read before the session (~10 min).** The session starts from these:
- [ ] **[What is barge-in in a voice AI agent?](https://outcomeschool.com/blog/what-is-barge-in-in-a-voice-ai-agent)**  *(Step 13)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 13: Customer Use Case: Real-Time Voice AI Agent*
- [ ] [Why does a voice agent cut people off mid-sentence?](https://outcomeschool.com/blog/voice-agents-cutting-users-off)
- [ ] [How does a voice agent handle long pauses when the user is thinking?](https://outcomeschool.com/blog/long-pauses-in-voice-agents)
- [ ] [How does a voice agent know a phone number or email is not finished yet?](https://outcomeschool.com/blog/unfinished-input-in-voice-agents)
- [ ] [How does a voice agent tell a real interruption from a cough or background noise?](https://outcomeschool.com/blog/interruption-vs-background-noise)
- [ ] [What are backchannels, and why should "mm-hmm" not stop the agent?](https://outcomeschool.com/blog/backchannels-in-voice-agents)
- [ ] [How does a voice agent stop speaking instantly when interrupted?](https://outcomeschool.com/blog/stopping-speech-on-interruption)
- [ ] [How does a voice agent truncate its memory to only what the user actually heard?](https://outcomeschool.com/blog/truncating-context-on-interruption)
- [ ] [How does a voice agent recover from a false interruption?](https://outcomeschool.com/blog/false-interruption-recovery)

**Questions we'll work through:**
- The caller coughs mid-answer. What should happen, and how do you test it?
- Memory truncation: why does it matter what the caller actually HEARD?

**Do:** List 10 voice-specific eval cases for the phone line.

### D39 · Thu 24 Dec · 📖 Voice agents III: latency budgets and tricks
📌 **Read before the session (~20 min).** The session starts from these:
- [ ] **[How do you build a latency budget for a voice AI agent?](https://outcomeschool.com/blog/voice-agent-latency-budget)**  *(Step 13)*
- [ ] **[Why does the time-to-first-audio matter more than total response time?](https://outcomeschool.com/blog/time-to-first-audio)**  *(Step 13)*

**Topics** (taught in the session; links are optional, only if you want to go deeper on something):
*Step 13: Customer Use Case: Real-Time Voice AI Agent*
- [ ] [How does the voice-to-voice latency of a voice agent get measured?](https://outcomeschool.com/blog/voice-to-voice-latency)
- [ ] [How does sentence chunking feed LLM output into TTS faster?](https://outcomeschool.com/blog/sentence-chunking-for-tts)
- [ ] [How does a TTS model start speaking before the full sentence arrives?](https://outcomeschool.com/blog/streaming-tts)
- [ ] [How does speculative LLM generation start replying before the user finishes?](https://outcomeschool.com/blog/speculative-generation-in-voice-agents)
- [ ] [How do filler phrases hide latency in a voice agent?](https://outcomeschool.com/blog/filler-phrases-in-voice-agents)
- [ ] [How does a voice agent hide the delay of a slow tool call?](https://outcomeschool.com/blog/slow-tool-calls-in-voice-agents)

**Questions we'll work through:**
- Why does time-to-first-audio matter more than total time?
- Your lookup_order tool takes 2s. How do you hide it without lying to the caller?

**Do:** Finalize the voice latency budget table (STT, LLM TTFT, tool, TTS).

### D40 · Fri 25 Dec · 📖 Capstone polish + customer artifacts

**Questions we'll work through:**
- Kirana's VP wants feature X, their engineers want Y, you have 2 weeks. What do you do?

**Do:** React ops UI (human-review queue + impact metrics). Write discovery notes, success criteria, runbook, post-mortem.

### D41 · Sat 26 Dec · 🔨 BUILD + SHIP

**Do:** Finish FieldDesk. Record a 5-min demo. Write a 1-page case study (problem → approach → impact numbers → next).

### D42 · Sun 27 Dec · 🔁 Review + 2 mock customer meetings

**Do:** `/fde-tutor review` then 2× `/fde-tutor drill customer` (exec + IT).


---

## Week 8: Interview prep + apply (Roadmap Step 14)

### D43 · Mon 28 Dec · 🎤 Interview: coding with AI agents

**Mock:** Build and debug a small feature end to end with a coding agent, timed, explaining your decisions out loud.

**Do:** Timed exercise: add a new category + eval cases to emalify-v2 in 45 min using Claude Code.

### D44 · Tue 29 Dec · 🎤 Interview: AI system design (RAG)
📌 **Read before the session (~10 min).** The session starts from these:
- [ ] **[AI System Design](https://github.com/amitshekhariitbhu/ai-system-design)**  *(Step 14)*


**Mock:** Design a RAG system for a customer: quality, latency, cost, security trade-offs.

**Do:** `/fde-tutor drill case` with a RAG design prompt.

### D45 · Wed 30 Dec · 🎤 Interview: AI system design (agent / voice agent)

**Mock:** Design an agent or voice agent for a given customer problem.

**Do:** `/fde-tutor drill case` with an agent/voice design prompt.

### D46 · Thu 31 Dec · 🎤 Interview: customer scenarios

**Mock:** Vague business problem → ask questions, define success, pick an approach, explain simply.

**Do:** 2× `/fde-tutor drill case` (customer scenario style).

### D47 · Fri 01 Jan · 🎤 Interview: deep-dive on your own project + behavioural

**Mock:** 'Walk me through FieldDesk. What broke? What would you change?'

**Do:** Write 5 STAR stories (Gether, Outbox, emalify-v2, FieldDesk). Rewrite resume bullets as FDE outcomes.

### D48 · Sat 02 Jan · 🔨 APPLY

**Do:** 15-20 targeted applications (Nanonets, DevRev, Sarvam, Workato, Galileo, Google Cloud, AI startups) with case study + demo link. `/fde-tutor jobs` first.

### D49 · Sun 03 Jan · 🔁 Final review

**Do:** `/fde-tutor review` across all weeks. Plan the next 4 weeks based on weak spots.


---

*Roadmap content © Amit Shekhar / Outcome School. Links point to the original free articles.*
