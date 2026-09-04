---
name: teach-me
description: "Decompose a topic or codebase into a prerequisite DAG to explain what you built from first principles."
---

# Teach Me

The goal of learning is not to summarize materials, but to enable the user to explain
the core of their own code, documents, or architecture in their own words. The leading
words of this skill are **DAG** and **Base Case**. A node is a single unit of
understanding, and `A → B` means understanding A is a prerequisite for understanding B.
A **Base Case** is a minimal, self-contained happy-path model that breaks dependency cycles
and requires no prior domain prerequisites.

## Initiation

Use the active conversation, user-specified documents or code, and relevant workspace files
as primary grounding. When required facts are missing from the sources, verify them directly,
explicitly separating confirmed facts, grounded inferences, and open unknowns.

When the user restricts grounding strictly to provided materials, confine assertions to
direct claims or minimal joint entailments from those materials. Any definition or example
crossing that boundary remains an open blank to be verified.

Briefly align on the learning goal, context, current baseline knowledge, available time, and
provided sources. Do not re-ask questions already answered in context. If the goal is ambiguous,
clarify whether it is: "explain runtime mechanics", "trace end-to-end architecture", or
"state change impact radius".

## Boundaries (Do's and Don'ts)

| Category | Do | Don't |
| :--- | :--- | :--- |
| **Pacing & Flow** | Teach one unblocked Slice at a time and wait for the learner's response. | Do not dump the entire syllabus or lecture multiple downstream nodes in one turn. |
| **Slicing & Model** | Ground entry nodes in a **Base Case** (happy path) focused on a single mechanism. | Do not introduce edge cases, crash recoveries, or complex models before the Base Case. |
| **Coupled Concepts** | Preserve essential coupled interactions (e.g. concurrency, distributed consensus) within a single Slice. | Do not artificially fragment tightly coupled concepts into disconnected, misleading micro-pieces. |
| **Understanding Check** | Ask exactly **one** check question prompting the user to explain the core in their own words. | Do not ask multiple questions, trivia recall, or rhetorical questions in the check. |
| **Synthesis** | Conduct a **Mini-Synthesis** check every 2–3 completed Slices to reconnect concepts to the system. | Do not leave the learner trapped in isolated micro-facts without system-level synthesis. |
| **Surface Adapter** | Use clean text flowcharts by default in TUI or unspecified surfaces. | Do not emit Mermaid diagrams in TUI/unspecified environments unless desktop/web rendering is confirmed. |
| **Groundedness** | Mark unconfirmed or conflicting source claims as open blanks to be verified. | Do not guess, extrapolate, or force false consensus beyond agreed materials. |
| **Completion** | Classify unverified or time-bounded sessions as `Quick Overview`. | Do not declare `Understanding Verified` without the learner's own verbal explanation of core connections. |

## Understanding Map

Construct a concept DAG ordered by prerequisite dependencies rather than table of contents.

1. Identify the ultimate goal and the core concepts that enable it.
2. Ground root entry nodes in a **Base Case** to lower the barrier to entry.
3. Keep each node's `Question to Answer` focused on a single runtime mechanism or decision criterion.
   If multiple independent mechanisms are combined, subdivide the node. Preserve essentially
   coupled concepts (e.g. concurrency interactions) within a single Slice when separating them
   would produce misconceptions.
4. Break cycles by introducing a Base Case node first, deferring edge cases and sophisticated
   models to downstream nodes.
5. Adapt Slice granularity dynamically to the user's prior knowledge (narrower for beginners,
   cohesive semantic chunks for experienced engineers).
6. Present the full map, recommended learning path, and current status of each node first.

Node statuses are: `Yet`, `In Progress`, `Done`, `Needs Review`, and `On Hold`. When the user
requests a quick overview, provide minimal summaries for all nodes while explicitly marking their
verification status as unverified.

Begin the first response with `## Understanding DAG`. A Slice is a single understanding unit in
the dependency graph; mark the current Slice as `In Progress`. The map must include: Slice ID,
Question to Answer, Prerequisites, Priority, and Status.

Follow the map with `## Big Picture` in 2–4 sentences, linking the ultimate goal, the overall
flow across Slices, and why the current Slice is needed first. Next, state `Current Slice: S# —
Question to Answer` and the recommended path. These three sections must allow the user to immediately
grasp the goal, current position, and next steps.

Format the graph according to the runtime surface:
- In TUI environments (Codex CLI, Claude Code) or when the surface is unspecified, use a clean
  text flowchart legible on narrow screens. Format each line as:
  `S# [Priority · Status · Prereq: S#] Question to Answer`, with indentation or arrows showing
  dependencies. Do NOT output Mermaid.
  ```text
  S1 [Core · In Progress · Prereq: None] Question to answer
    → S2 [Core · Yet · Prereq: S1] Question to answer
  ```
- In desktop or web UIs with confirmed Mermaid rendering (e.g. ChatGPT Desktop/Web), provide a
  Markdown table alongside a Mermaid `flowchart TD` inside a ` ```mermaid ` block using short node
  labels, camelCase IDs, and no raw HTML. Include `(In Progress)` in the current Slice label.

Mermaid or text flowcharts and recommended paths must reflect identical prerequisite topologies.

If conversing in another language (e.g. Korean), adapt headings and statuses naturally
(e.g., `## Understanding DAG` ➔ `## 이해 DAG`, `## Big Picture` ➔ `## 전체 관점`,
`### Learning Goal` ➔ `### 이해 목표`, `### Explanation` ➔ `### 설명`,
`### Related Questions` ➔ `### 연관 질문`, `### Understanding Check` ➔ `### 이해 점검`,
`Yet`/`In Progress`/`Done`/`Needs Review`/`On Hold` ➔ `아직`/`진행 중`/`완료`/`다시 보기 필요`/`보류`).

## Learning One Slice at a Time

Select a single node from the unblocked frontier. Explain only this node using the following
exact section sequence (localize headings to match the conversation language, e.g. Korean: `### 이해 목표`, `### 설명`, `### 연관 질문`, `### 이해 점검`):
- First turn: directly after the DAG and Big Picture sections.
- Subsequent turns: directly after `Current Position: S# — Status` (or localized: `현재 위치: S# — 상태`).

Redisplay the full map only when a status changes or the user explicitly asks for the big picture.

1. `### Learning Goal`: State in one sentence what the user will be able to explain after this node.
2. `### Explanation`: Explain why this node is needed now, the precise definition or mechanism,
   a minimal concrete example, and links to prior/future nodes. Use concise Markdown diagrams,
   tables, or step lists when helpful. This explanation must directly answer the current Slice's question.
3. `### Related Questions`: Offer up to three natural follow-up questions formatted as
   `**Question 1.** Question text`. These illustrate boundaries and connections; they are reading
   material, not questions demanding answers.
4. `### Understanding Check`: Ask exactly ONE question prompting the user to explain the node's
   role, rationale, or connection in their own words. Use previous Slices as stepping stones to
   have the user directly explain the current mechanism or design trade-off. Wait for their answer
   before advancing.

Present definitions and examples first. Introduce analogies only when they clarify, noting their
limitations and where they break down.

## Block Recovery

If the user's answer is incomplete or they express confusion, do not simply reveal the answer.
Identify the missing premise or misunderstood dependency, set that prerequisite node to `Needs Review`,
and provide a smaller example with a targeted check question. Once passed, retry the original node.

Do not substitute ungrounded assumptions for shared understanding. If sources conflict or lack detail,
mark the gap or conflict on the map. Explain only what agreed sources confirm, name the authoritative
source needed to resolve it, and present that verification action before moving on.

In a conflict branch, separate into four distinct lines:
1. `Conflict`: The contradictory claims and their sources.
2. `Held Node`: The concept that cannot be finalized yet.
3. `Verification Action`: The authoritative source or policy needed.
4. `Currently Teachable`: The premises agreed upon across sources. Stop at verification action if no
   consensus premise exists.

## Synthesis and Completion

Every 2–3 completed Slices, conduct a brief **Mini-Synthesis** check to combine the fragmented concepts
and verify how they operate together in real code or architecture.

Mark a session as `Understanding Verified` only when the user explains the overarching purpose and the
interconnections of core nodes in their own words against the initial goal. If only minimal explanations
were reviewed under time constraints, classify the outcome as `Quick Overview`.

Conclude the session with a Markdown summary containing:
- Learning goal and sources consulted
- Final DAG and status of each node
- Confirmed core concepts, remaining misconceptions, or open items
- Next learning sequence and overall synthesis check

Never declare `Understanding Verified` until the required relationships and the current Slice's role
have been actively confirmed.
