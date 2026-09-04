# Skills For Principled Engineers

[![skills.sh](https://skills.sh/b/ckdals1108/skills)](https://skills.sh/ckdals1108/skills)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

> **Understand what you (or the AI) built from first principles — not vibe learning.**

> *"If you can't explain it simply, you don't understand it well enough."*  
> — Richard Feynman

AI coding agents can generate entire microservices and complex distributed transactions in seconds. But shipping fast creates **understanding debt**: when production crashes at 2 AM or architecture reviews come up, can you actually explain why the system works in your own words?

Summaries do not create understanding. Bullet points do not create mental models.

### The Contrast

| Dimension | Generic AI Explanations | `/teach-me` (Socratic DAG) |
| :--- | :--- | :--- |
| **Pacing** | Dumps 2,000 words of monolithic lecture | Slices into prerequisite DAG; 1 node at a time |
| **Cognitive Mode** | Passive skimming (illusion of competence) | Active verbalization from first principles |
| **Anchoring** | Starts with edge cases & full complexity | Anchors in minimal **Base Case** (happy path) |
| **Verification** | Assumes you understand; moves on | Exactly **1 check question**; waits for your explanation |
| **Outcome** | Vanishes in 30 minutes (**Understanding Debt**) | Permanent mental model (**True Mastery**) |

These skills are designed to turn agents into rigorous Socratic mentors that decompose systems into **prerequisite DAGs**, anchor on **Base Cases**, and verify your understanding one slice at a time.

---

## Quickstart (30-second setup)

### Install via skills.sh (Codex CLI, Claude Code, Cursor, Antigravity)

Use the universal `skills.sh` installer:

```bash
npx skills@latest add ckdals1108/skills --skill teach-me
```

To install globally for a specific harness:

```bash
# Codex CLI
npx skills add ckdals1108/skills --skill teach-me -g --agent codex

# Claude Code
npx skills add ckdals1108/skills --skill teach-me -g --agent claude
```

---

### Install as a native Claude Code Plugin

Prefer a managed, plug-and-play install that automatically updates? Install directly inside Claude Code:

```text
/plugin marketplace add ckdals1108/skills
/plugin install ckdals1108-skills@ckdals1108
```

Or from your shell:

```bash
claude plugin marketplace add ckdals1108/skills
claude plugin install ckdals1108-skills@ckdals1108
```

---

## Flagship Skill: `/teach-me`

Decompose any topic, PR, or unfamiliar codebase into an executable prerequisite DAG. 

```bash
# In your agent:
/teach-me Teach me how the distributed 2-Phase Commit (2PC) in our payments service works.
```

### What happens in the terminal:

```text
## Understanding DAG

S1 [Core · In Progress · Prereq: None] What problem does 2PC solve, and who participates?
  → S2 [Core · Yet · Prereq: S1] What happens in the prepare (vote) phase?
    → S3 [Core · Yet · Prereq: S2] What happens in the commit/abort decision phase?
      → S4 [Core · Yet · Prereq: S3] How does 2PC provide atomicity across services or databases?
        → S5 [Important · Yet · Prereq: S4] What happens when a coordinator or participant crashes?
          → S6 [Important · Yet · Prereq: S5] When is 2PC a poor fit, and what are alternatives?

Recommended path: S1 → S2 → S3 → S4 → S5 → S6.

## Big Picture

Two-Phase Commit (2PC) coordinates one logical transaction across multiple independent systems so they reach the same outcome: all commit or all abort. We start with the actors and the consistency problem, because the two phases only make sense once you know who must agree and why partial success is dangerous.

Current Slice: S1 — What problem does 2PC solve, and who participates?

### Learning Goal
You will be able to explain why a distributed transaction needs 2PC and distinguish the coordinator from participants.

### Explanation
...
For now, use the happy-path model: all systems are reachable and eventually agree. Crashes, timeouts, and the risk of blocking come later in S5.

### Related Questions
**Question 1.** Why can’t the coordinator simply tell every service to commit at the same time?
**Question 2.** Is 2PC intended to make services eventually consistent or immediately atomic?
**Question 3.** What makes a participant able—or unable—to safely commit?

### Understanding Check
In your own words: for the order-and-inventory example, what partial-success problem does 2PC prevent, and what is the coordinator’s job?
```

Notice what just happened:
1. **The agent did not dump a 10-page monolithic lecture.**
2. It built a strict **prerequisite DAG** showing the entire roadmap first.
3. It anchored in a minimal **Base Case** (happy path) to break circular dependencies.
4. It asked **exactly one** understanding check question and stopped to wait for your answer.

---

## Why It Works: The Cognitive Architecture

Unlike generic prompt templates, `teach-me` is engineered around foundational cognitive science and software engineering principles:

* **Cognitive Load Theory (Sweller)**: Prevents working memory overload by controlling element interactivity. Concepts are sliced so you only encounter one new runtime mechanism at a time.
* **Base Case Anchoring**: Breaks infinite dependency cycles by introducing a minimal, self-contained happy-path model first, deferring complex recoveries and distributed edge cases downstream.
* **Semantic Slicing (Weiser / Parnas)**: Modules are split along information-hiding seams and runtime decision boundaries rather than arbitrary syntactic lines.
* **Preservation of Coupled Concepts**: Essential interactions (e.g. concurrency locks, leader leases) are kept together to prevent misconceptions.
* **Mini-Synthesis (Divide-Conquer-Combine)**: Every 2–3 completed Slices, the agent runs a synthesis check to reconnect isolated pieces back into the macroscopic architecture.
* **Multilingual Out-of-the-Box**: Works seamlessly in English, Korean, or any other language — headers and statuses automatically adapt to the conversation (`## 이해 DAG`, `## 전체 관점`, `### 이해 점검`).

---

## Built-in Verification Suite

Every skill in this repository includes a dedicated headless evaluation suite under `eval/`:

```bash
# Test against the 6 standard regression cases:
codex -a never exec --ephemeral --skip-git-repo-check -s read-only -C /tmp \
  'Use $teach-me to ...'
```

Verified assertions include:
- Base Case root anchoring
- Single-mechanism semantic slicing
- Strictly bounded single check question
- Source-grounded misconception recovery
- Strict separation between `Quick Overview` and verified mastery

---

## License

[MIT](LICENSE)
