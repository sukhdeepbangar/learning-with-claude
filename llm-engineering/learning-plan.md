# LLM Engineering Learning Plan

A structured path to understanding LLM internals and building better LLM applications.

---

## Current Status

**Phase:** Phase 1 - How Text Becomes Numbers
**Current topic:** Tokenization (in progress)
**Last session:** 2026-01-16

### Where We Left Off

Covered conceptually:
- What tokens are (the fundamental unit LLMs process)
- Why tokens exist (sweet spot between characters and words)
- How BPE tokenization works (merging common pairs)
- Why case matters ("ChatGPT" vs "chatgpt" produce different tokens)

**Next steps when you return:**
1. Run through the notebook: `phase-1-tokenization/tokenization-exploration.ipynb`
2. Experiment with the case sensitivity and word splitting examples
3. Continue with any questions that arise
4. When ready, move to **Embeddings** (next topic in Phase 1)

---

## Learning Profile

| Aspect | Preference |
|--------|------------|
| Goals | Understand internals + Build better LLM apps |
| Sessions | Flexible timing |
| Learning style | Doing > Reading. Jupyter notebooks for exploration |
| Projects | At major milestones, brainstorm together |
| Python | Familiar, not fluent |
| Frameworks | Open - no lock-in |
| Documentation | Markdown notes in this repo |

**Starting point:**
- Know: API calls, agents, tool use mechanics
- Don't know: ML basics, NLP, how LLMs actually work

**Approach:** Hybrid - enough foundation to make doing meaningful, then build, then go deeper.

---

## Phase 1: How Text Becomes Numbers

Everything else builds on this. You can't understand LLMs without knowing what they actually see.

### Topics

- [ ] **Tokenization**
  - Format: Notebook
  - Learn: Text → tokens → numbers. Why "ChatGPT" and "chatgpt" are different to a model
  - Resources: _to be added_
  - Notes: _to be added_

- [ ] **Embeddings**
  - Format: Notebook
  - Learn: Words as vectors. Similar meanings = nearby vectors
  - Resources: _to be added_
  - Notes: _to be added_

### Project: Semantic Search Tool

- [ ] **Build a semantic search tool**
  - Find similar content by meaning, not keywords
  - Uses embeddings + cosine similarity
  - *Why here:* You'll feel vectors "click" when you see that "dog" finds "puppy" and "canine"
  - Link: _to be added_

---

## Phase 2: How LLMs Generate Text

Now you know the inputs. Time to understand the outputs.

### Topics

- [ ] **Next-token prediction**
  - Format: Notebook
  - Learn: The core mechanic - LLMs just predict the next word, repeatedly
  - Resources: _to be added_
  - Notes: _to be added_

- [ ] **Temperature & sampling**
  - Format: Notebook
  - Learn: Why the same prompt gives different outputs. Control the randomness
  - Resources: _to be added_
  - Notes: _to be added_

- [ ] **Context window**
  - Format: Explanation + notebook
  - Learn: What the model "sees". Why long conversations get weird
  - Resources: _to be added_
  - Notes: _to be added_

### Project: Token Visualizer / Probability Explorer

- [ ] **Build a token probability explorer**
  - Shows top candidate tokens at each step and their probabilities
  - *Why here:* Demystifies "creativity" - you'll see it's just weighted dice rolls
  - Link: _to be added_

---

## Phase 3: The Transformer (The Architecture)

You've seen the inputs and outputs. Now peek inside the box.

### Topics

- [ ] **Attention mechanism**
  - Format: Explanation + visual
  - Learn: How the model decides what to "pay attention to"
  - Resources: _to be added_
  - Notes: _to be added_

- [ ] **Transformer architecture**
  - Format: Explanation
  - Learn: The building blocks - attention, feed-forward, layers
  - Resources: _to be added_
  - Notes: _to be added_

- [ ] **Why this matters for your apps**
  - Format: Discussion
  - Learn: Connect architecture to practical behavior
  - Resources: _to be added_
  - Notes: _to be added_

### Project: Attention Visualizer (Optional)

- [ ] **Build an attention visualizer**
  - Visualize which tokens attend to which in a prompt
  - *Why here:* See the theory come alive. Understand why word order matters
  - More advanced - can skip if it feels too deep
  - Link: _to be added_

---

## Phase 4: Building Better LLM Apps

Now you understand the internals. Time to apply that knowledge.

### Topics

- [ ] **Systematic prompt engineering**
  - Format: Notebook + notes
  - Learn: Move beyond trial-and-error
  - Resources: _to be added_
  - Notes: _to be added_

- [ ] **RAG (Retrieval Augmented Generation)**
  - Format: Notebook
  - Learn: Give LLMs knowledge they weren't trained on
  - Resources: _to be added_
  - Notes: _to be added_

- [ ] **Chunking strategies**
  - Format: Notebook
  - Learn: How to split documents for retrieval
  - Resources: _to be added_
  - Notes: _to be added_

- [ ] **Evaluation**
  - Format: Notebook
  - Learn: How to measure if your LLM app is working
  - Resources: _to be added_
  - Notes: _to be added_

### Project: RAG System from Scratch

- [ ] **Build a "chat with your docs" system**
  - Embeddings, retrieval, generation - full pipeline
  - *Why here:* Combines everything - embeddings (Phase 1), generation (Phase 2), prompting
  - Link: _to be added_

---

## Phase 5: Agents - Going Deeper

You already work with agents. Now understand them properly.

### Topics

- [ ] **Agent loops & patterns**
  - Format: Explanation + notebook
  - Learn: ReAct, planning, reflection patterns
  - Resources: _to be added_
  - Notes: _to be added_

- [ ] **Memory architectures**
  - Format: Explanation
  - Learn: Short-term, long-term, how to persist context
  - Resources: _to be added_
  - Notes: _to be added_

- [ ] **Tool use internals**
  - Format: Deep dive
  - Learn: What's actually happening when an agent calls a tool
  - Resources: _to be added_
  - Notes: _to be added_

### Project: Research Agent

- [ ] **Build a research agent**
  - Searches, reads, synthesizes, and cites sources
  - *Why here:* Integrates everything. Make architectural decisions and understand why
  - Link: _to be added_

---

## Phase 6: Optional Deep Dives

Pick based on interest. Not required.

- [ ] **Fine-tuning** - When and how to adapt a model to your domain
- [ ] **RLHF** - How models get "aligned" - why Claude behaves differently than base models
- [ ] **Open vs closed models** - Trade-offs, when to use what
- [ ] **Model evaluation & benchmarks** - How to read papers, compare models

---

## Session Log

Track what we covered in each session.

| Date | Phase | Topics Covered | Notes |
|------|-------|----------------|-------|
| 2026-01-16 | Phase 1 | Tokenization (concepts) | What tokens are, BPE, case sensitivity |

---

## Resources Created

Links to notebooks, notes, and projects as we build them.

| Resource | Type | Phase | Link |
|----------|------|-------|------|
| Tokenization Exploration | Notebook | Phase 1 | [tokenization-exploration.ipynb](phase-1-tokenization/tokenization-exploration.ipynb) |

---

## How We Work

```
Each topic:
    You ask questions → I explain
    Notebook exploration → You experiment
    Document key insights → Markdown notes

Each project:
    We brainstorm scope together
    You build (I help when stuck)
    Document what you learned
```
