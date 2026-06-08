---
name: scope-trim-and-mvp
description: trim feature or project scope to a more practical mvp using dev-planning-lead-product-manager, dev-planning-sr-developer, dev-planning-lead-architect, customer-bad-skeptic, and customer-good-advocate. use when an idea feels too large, too risky, too ambiguous, or too expensive and the goal is to preserve the core customer value while reducing complexity, delivery risk, and unnecessary scope.
---

Use this skill to reduce a feature, project, or product idea to a more realistic and valuable MVP.

This skill is for scope shaping and prioritization. It is especially useful when an idea seems directionally good but feels too large, too vague, too expensive, too risky, or too complex to deliver confidently in its current form.

Follow this workflow in order.

## Workflow overview

1. Understand and normalize the proposal
2. Identify the strongest customer value
3. Identify the strongest customer objections and friction
4. Evaluate product scope and prioritization
5. Evaluate engineering practicality and delivery risk
6. Evaluate architectural weight and complexity
7. Synthesize a trimmed MVP and phased recommendation

## Step 1: Understand and normalize the proposal

Accept flexible input. The user may provide:
- a rough feature idea
- a PRD
- a feature spec
- a project summary
- stakeholder asks
- a roadmap concept
- a workflow problem
- a pasted document fragment

First, normalize the material into a working summary with:
- problem being solved
- target user or customer
- proposed capability
- expected outcome
- major workflows or components
- obvious value claims
- obvious complexity drivers
- known constraints
- obvious assumptions
- anything still unclear

If the input is incomplete, messy, or contradictory, proceed anyway. Do not block unless there is too little information to identify the intended idea. If needed, make the best possible interpretation and explicitly label assumptions.

## Step 2: Identify the strongest customer value

Use `customer-good-advocate` to identify what is genuinely valuable in the proposal.

Focus on:
- the core customer problem worth solving
- the most meaningful outcomes for users
- the strongest adoption drivers
- what part of the idea customers would actually care about
- what value should be preserved even if scope must shrink
- which customer segments are most likely to benefit

This step should identify the real value kernel that must not be lost during scope reduction.

## Step 3: Identify the strongest customer objections and friction

Use `customer-bad-skeptic` to identify what customers would resist, ignore, distrust, or find too complicated.

Focus on:
- confusing or low-value parts of the proposal
- extra steps, friction, or workflow disruption
- features that feel overbuilt or unnecessary
- weak value relative to effort or complexity
- likely adoption barriers
- reasons a customer may ignore the feature entirely
- where the proposal tries to do too much at once

This step should identify what can be cut, delayed, simplified, or reframed.

## Step 4: Evaluate product scope and prioritization

Use `dev-planning-lead-product-manager` to determine what belongs in MVP versus later phases.

Focus on:
- core problem to solve first
- in-scope vs out-of-scope boundaries
- requirements that are essential vs optional
- whether the feature is trying to solve multiple problems at once
- where phasing would improve clarity and delivery confidence
- which tradeoffs are most acceptable
- how to preserve meaningful value while narrowing scope

This step should define a cleaner product shape, not just a smaller one.

## Step 5: Evaluate engineering practicality and delivery risk

Use `dev-planning-sr-developer` to identify what makes the proposal hard to implement and what could be safely deferred.

Focus on:
- hidden complexity
- sequencing issues
- ambiguous workflows
- risky dependencies
- edge cases that expand scope disproportionately
- requirements that are too vague to build efficiently
- work that should be split into safer increments
- which parts are likely to create churn or delay if included in MVP

This step should help trim scope based on practical delivery reality.

## Step 6: Evaluate architectural weight and complexity

Use `dev-planning-lead-architect` to identify where the proposal is carrying unnecessary solution weight for an MVP.

Focus on:
- architectural overreach
- premature scalability or extensibility work
- overly broad system boundaries
- dependencies that increase complexity too early
- technical decisions that may be justified later but not in MVP
- where a simpler initial solution shape would be sufficient
- how to reduce long-term harm while still simplifying near-term delivery

This step should prevent the MVP from turning into a disguised full-platform build.

## Step 7: Synthesize the final MVP recommendation

Synthesize all findings into a trimmed, more realistic MVP recommendation.

Explicitly identify:
- the core value that must be preserved
- the scope that should be removed, deferred, or simplified
- the minimum viable workflow
- what belongs in MVP
- what belongs in a later phase
- what should be dropped entirely
- the tradeoffs being accepted
- what risks remain even after trimming

Do not simply cut features mechanically. Preserve the strongest customer value while reducing complexity, ambiguity, and delivery risk as much as possible.

## Output format

Use this exact section structure unless the user asks for something different:

# Scope Trim and MVP

## 1. Proposal summary
- problem
- target user or customer
- proposed capability
- expected outcome
- key assumptions
- obvious complexity drivers

## 2. Core customer value
Summarize the most important findings from `customer-good-advocate`.

## 3. Customer friction and objections
Summarize the most important findings from `customer-bad-skeptic`.

## 4. Product scope review
Summarize the most important findings from `dev-planning-lead-product-manager`.

## 5. Engineering practicality review
Summarize the most important findings from `dev-planning-sr-developer`.

## 6. Architecture complexity review
Summarize the most important findings from `dev-planning-lead-architect`.

## 7. Recommended MVP
Describe the best trimmed version of the proposal, including:
- the core problem solved
- the minimum viable workflow
- the must-have capabilities
- the intentional constraints of MVP

## 8. Defer, phase, or drop
Separate the remaining ideas into:
- defer to later phase
- phase in after validation
- drop entirely

## 9. Tradeoffs and residual risks
Explain what value is preserved, what is being sacrificed, and what risks still remain.

## 10. Recommended next step
Recommend the most appropriate next action, such as:
- write the MVP spec
- validate the narrower concept with customers
- split the project into phases
- remove low-value complexity
- stop or rethink the proposal

## Synthesis rules

- Do not preserve scope just because it was originally requested.
- Do not reduce scope so aggressively that the core customer value disappears.
- Distinguish must-have value from nice-to-have ambition.
- Prefer one strong, usable workflow over multiple partial workflows.
- Make tradeoffs explicit.
- Use customer value and delivery practicality together, not separately.
- Treat phasing as a deliberate product strategy, not a dumping ground.
- Keep the output practical for a technical PM deciding what should actually get built first.
- If the proposal is already appropriately scoped, say so clearly and explain why.

## Good use cases

Use this skill for:
- oversized feature proposals
- roadmap items that feel too broad
- projects with too many stakeholder asks
- MVP definition
- phase-one scoping
- value-preserving simplification
- deciding what to build first

## Not ideal for

This skill is less useful for:
- raw discovery without a proposed direction
- final architecture design
- deep integration verification
- detailed API design
- sprint task decomposition
- post-implementation review

Use other skills for those workflows.