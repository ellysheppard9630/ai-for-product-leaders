---
name: gap-analysis
description: Run a structured gap analysis on a project brief, PRD, or feature spec in a question-and-answer format. Walks through four stages — analyze, stress-test, decisions, improved spec — asking the user targeted questions at each stage and incorporating answers into a final buildable spec. 

Triggers on: gap analysis, analyze this brief, stress test this spec, find the gaps, make this buildable, improve this PRD.
---

Use this skill to turn a rough project brief, PRD, or feature spec into a buildable specification by identifying gaps, stress-testing assumptions, resolving product decisions, and rewriting the spec.

This skill is explicitly **question-and-answer driven**. At each stage, produce findings as Q&A pairs, then pause and ask the user the open questions that materially affect the improved spec. Do not continue to the next stage until the user has answered or explicitly said "skip" / "use your recommendation."

## Input

Accept flexible input. The user may provide:
- a file path to a brief, PRD, or spec
- pasted text of a brief
- a URL (Confluence, Google Doc, Figma, etc.)
- a feature description in chat

If the input is a file path, read it. If it's a URL, fetch it with the appropriate tool (Confluence MCP for Confluence, WebFetch for public pages, etc.). If it's pasted text, use it as-is. If the brief is too sparse to analyze, ask for more context before starting Stage 1.

## Workflow

Run the four stages in order. At the end of each stage, present the Q&A output, then ask the user the decision questions for that stage. Wait for answers before continuing.

---

### Stage 1 — Analyze (find missing or undefined elements)

Review the brief as if engineering must implement it tomorrow. Identify every missing or undefined element across these categories:

- **Business rules** — logic, calculations, thresholds, ordering, precedence
- **System states** — what states exist, how transitions happen, what's valid per state
- **Edge cases** — empty inputs, max/min values, concurrent actions, boundary conditions
- **Permissions** — who can do what, role-based access, ownership rules
- **Data & integration** — sources of truth, sync behavior, required fields, external systems
- **Offline / degraded behavior** — network loss, partial failures, stale data, retries

**Output format:** Present findings as a numbered list of Q&A pairs.

```
Stage 1 — Gaps Identified

Business Rules
1. Q: What happens when a user transfers merch to a location that has zero capacity?
   Current state: Not specified
2. Q: How is the transfer quantity validated against source inventory?
   Current state: Implied but not defined

System States
3. Q: ...
```

**Then pause and ask the user:** "Which of these gaps do you want to resolve now, and which should I flag as assumptions?" Use the AskUserQuestion tool if there are 2–4 clear decisions to surface; otherwise ask in prose.

---

### Stage 2 — Stress-test (failure scenarios and ambiguity)

Assume this system will fail in real-world conditions and that two engineers will read the spec differently. Identify:

- **Failure scenarios** — what breaks and how the system should respond
- **Edge cases not caught in Stage 1** — unusual but plausible conditions
- **Ambiguous behaviors** — sentences in the brief that could be interpreted two ways
- **Divergent implementations** — places where engineers would likely make different choices without guidance
- **Race conditions and timing** — ordering, latency, concurrency

**Output format:** Q&A pairs grouped by category.

```
Stage 2 — Stress-Test Findings

Ambiguous Behaviors
1. Q: The brief says "transfer is finalized when both parties confirm." What counts as confirmation — in-app approval, email reply, or manager sign-off?
   Risk: Three valid interpretations, each with different UX

Failure Scenarios
2. Q: What happens if the receiving location rejects the transfer after it has already left the sending location?
   Risk: No recovery path defined
```

**Then pause and ask the user** for their call on the top 3–5 highest-risk ambiguities. Use AskUserQuestion when the options are discrete.

---

### Stage 3 — Decisions (resolve product questions with tradeoffs)

Based on gaps from Stage 1 and risks from Stage 2, list the **product decisions** that must be made before implementation. For each decision, provide:

1. **Decision** — the question being decided
2. **Options** — 2–3 realistic choices
3. **Tradeoffs** — impact, effort, risk, reversibility for each option
4. **Recommendation** — your preferred option and why

**Output format:**

```
Stage 3 — Product Decisions

Decision 1: How should the system handle a transfer rejection after shipment?
  Option A: Auto-create a return-transfer back to the origin
    - Impact: User sees two transactions; no manual work
    - Effort: Medium (new workflow)
    - Risk: Double-counting inventory if return fails
    - Reversibility: Easy
  Option B: Hold the items in a "pending return" state until manually resolved
    - Impact: Manual work but full control
    - Effort: Low
    - Risk: Items stuck in limbo if forgotten
    - Reversibility: Easy
  Recommendation: Option A — matches existing return flow and reduces manual work.
```

**Then pause and ask the user** to confirm or override each recommendation. Use AskUserQuestion with the options presented so the user can select directly.

---

### Stage 4 — Improved spec (buildable)

Using the user's answers from Stages 1–3, regenerate the full spec. It must include the sections defined in CLAUDE.md:

1. **Problem Statement**
2. **Goals**
3. **User Stories** (with goal, acceptance criteria, edge cases, definition of done)
4. **Acceptance Criteria**
5. **Out of Scope**

Plus these added sections that the original brief was missing:

6. **Business Rules** — explicit, numbered
7. **System States & Transitions** — with a state diagram or table if useful
8. **Permissions Matrix** — who can do what
9. **Edge Cases & Failure Handling** — explicit responses to Stage 2 findings
10. **Assumptions** — clearly labeled, with the decision source noted ("confirmed by PO", "recommended default")
11. **Open Questions** — anything the user said "skip" on or that still needs resolution

Label every assumption with one of:
- `[CONFIRMED]` — user answered this directly
- `[RECOMMENDED]` — skill recommended and user accepted
- `[ASSUMED]` — no answer yet, flagged for follow-up

**Output:** Write the improved spec back to the **original input file**. Before writing, ask the user whether to:
- **Replace** — overwrite the original with the improved spec (add a note at the top that the original has been superseded and keep the original PM/date/status metadata). Best when the improved spec is meant to supersede the original.
- **Append** — keep the original intact and append a new `## Gap Analysis — <today's date>` section at the bottom containing (a) the resolved assumptions table, (b) the open questions, (c) a diff-style summary of the business rules, state machine, permissions matrix, and edge cases that were added. Best when the original needs to stay as the source-of-record.

Use AskUserQuestion to confirm. Default recommendation: **Replace** (original is still accessible via git history).

If the original input was not a file (pasted text, URL, chat description), fall back to the prior behavior: produce the full improved spec inline and offer to save to a new file.

---

## Behavior rules

- **Do not skip stages.** Each stage builds on the last.
- **Do not invent answers.** If the user hasn't answered a question and there's no clear default, label it `[ASSUMED]` in the final spec with a brief note.
- **Respect the user's current role.** The user is a technical product owner — frame decisions around impact, effort, risk, reversibility (per CLAUDE.md).
- **Be direct.** No preamble, no "great question," no hedging. Lead with findings.
- **Use AskUserQuestion** when the user has 2–4 discrete choices per decision. Use prose questions when answers are open-ended.
- **Write the improved spec in prose + bullets**, not Q&A. The Q&A format is for stages 1–3; Stage 4 output is a normal PRD.

## When to stop early

If at any stage the user says "this is enough" or "skip to the improved spec," jump to Stage 4 and mark unanswered questions as `[ASSUMED]` or `[OPEN QUESTION]`.
