---
name: spec-pressure-test
description: pressure-test a product spec, feature brief, prd, or engineering handoff using dev-planning-lead-product-manager, dev-planning-sr-architect, dev-planning-sr-developer, research-qa-analyst, and dev-execution-integration-verifier. use when a spec needs to be challenged for scope clarity, technical feasibility, implementation risk, integration concerns, and testability before engineering starts.
---

Use this skill to challenge a spec from multiple angles before it reaches engineering.

This skill is for pre-handoff review. It is especially useful when a feature brief, PRD, requirements draft, or engineering handoff looks directionally strong but may still contain hidden ambiguity, technical risk, integration gaps, or testability problems.

Follow this workflow in order.

## Workflow overview

1. Understand and normalize the spec
2. Review the spec through a PM lens
3. Review the spec through a senior architecture lens
4. Review the spec through a senior developer feasibility lens
5. Review the spec through a QA and testability lens
6. Review the spec through an integration lens
7. Synthesize the findings into an engineering-readiness assessment

## Step 1: Understand and normalize the spec

Accept flexible input. The user may provide:
- a PRD
- a feature spec
- a requirements draft
- a handoff summary
- a project brief
- acceptance criteria
- workflow notes
- a pasted document fragment

First, normalize the input into a working summary with:
- problem being solved
- target user or customer
- proposed capability
- intended outcome
- key workflows
- dependencies already mentioned
- constraints already mentioned
- obvious assumptions
- areas that are still unclear

If the input is incomplete or rough, proceed anyway. Do not block unless there is too little information to identify the intended feature or change. If needed, make the best possible interpretation and explicitly label assumptions.

## Step 2: Review through a PM lens

Use `dev-planning-lead-product-manager` to evaluate the spec as a product definition artifact.

Focus on:
- whether the problem statement is clear
- whether the target user and value are defined well enough
- whether scope is coherent
- whether the spec contains hidden scope creep
- whether priorities and constraints are understandable
- whether requirements are stated as requirements rather than vague hopes
- whether non-scope and tradeoffs are sufficiently clear

This step should determine whether the spec is shaped well enough to support engineering work.

## Step 3: Review through a senior architecture lens

Use `dev-planning-sr-architect` to evaluate the technical design quality implied by the spec.

Focus on:
- system boundaries
- dependency assumptions
- interface and workflow interactions
- non-functional requirements
- performance, reliability, security, and operability concerns
- areas where the design is underdefined
- risks that could grow if engineering proceeds without more clarity

This step should identify architecture-level ambiguity and technical design concerns before implementation begins.

## Step 4: Review through a senior developer feasibility lens

Use `dev-planning-sr-developer` to stress-test implementation practicality.

Focus on:
- whether the work is buildable as written
- missing technical details
- hidden complexity
- sequencing issues
- data or state-handling ambiguity
- edge cases
- where engineers are likely to make conflicting assumptions
- where the spec is too vague to implement consistently

This step should expose the practical engineering risks between design intent and real delivery.

## Step 5: Review through a QA and testability lens

Use `research-qa-analyst` to evaluate whether the spec is verifiable.

Focus on:
- whether acceptance criteria are clear and testable
- missing success and failure conditions
- edge cases and alternate flows
- unclear permissions, validation rules, or state transitions
- whether QA and UAT would know how to validate the work
- where ambiguity would create rework, disagreement, or weak release confidence

This step should ensure the spec can actually be tested and validated.

## Step 6: Review through an integration lens

Use `dev-execution-integration-verifier` to evaluate the spec for cross-system and dependency risk.

Focus on:
- service or system boundaries
- external dependencies
- contract assumptions
- data flow between systems
- error propagation and fallback expectations
- environment or configuration dependencies
- ownership gaps across teams or systems
- failure modes that are implied but not addressed

If the spec has little or no meaningful integration component, keep this section concise and say so clearly.

## Step 7: Synthesize the final assessment

Synthesize all findings into a clear engineering-readiness assessment.

Explicitly identify:
- the strongest parts of the spec
- the biggest gaps
- hidden risks
- blockers vs refinements
- assumptions that need validation
- what must be clarified before engineering starts
- what can be resolved during implementation without excessive risk

Do not merely stack reviews together. Resolve overlap, highlight patterns, and turn the findings into a practical pre-handoff recommendation.

## Output format

Use this exact section structure unless the user asks for something different:

# Spec Pressure Test

## 1. Spec summary
- problem
- target user or customer
- proposed capability
- intended outcome
- key workflows
- known dependencies
- key assumptions

## 2. PM review
Summarize the most important findings from `dev-planning-lead-product-manager`.

## 3. Architecture review
Summarize the most important findings from `dev-planning-sr-architect`.

## 4. Implementation feasibility review
Summarize the most important findings from `dev-planning-sr-developer`.

## 5. QA and testability review
Summarize the most important findings from `research-qa-analyst`.

## 6. Integration review
Summarize the most important findings from `dev-execution-integration-verifier`.

## 7. Cross-cutting risks and gaps
Identify patterns that appear across multiple perspectives.

## 8. Blockers vs refinements
Separate:
- blockers before engineering starts
- important refinements
- lower-risk follow-ups

## 9. Engineering-readiness verdict
State clearly whether the spec is:
- ready
- mostly ready with targeted fixes
- not ready yet

Explain why.

## 10. Recommended next step
Recommend the most appropriate next action, such as:
- proceed to engineering handoff
- revise scope
- clarify open questions
- define missing acceptance criteria
- resolve integration assumptions
- improve technical design detail first

## Synthesis rules

- Do not assume a well-written spec is a complete spec.
- Do not ignore missing non-functional requirements.
- Do not let architecture concerns drown out product clarity issues, or vice versa.
- Distinguish blockers from improvements.
- Make ambiguity visible.
- Focus on what engineering needs in order to build confidently.
- Keep the output practical for a technical PM preparing handoff.
- If multiple reviewers identify the same issue, elevate it as a cross-cutting concern.
- If the spec is strong, say so clearly, but still identify residual risks honestly.

## Good use cases

Use this skill for:
- feature specs
- PRDs before engineering review
- engineering handoff drafts
- high-risk feature proposals
- integration-heavy requirements
- complex workflow changes
- any spec that feels nearly ready but should be challenged first

## Not ideal for

This skill is less useful for:
- raw discovery notes
- early brainstorming without a proposed direction
- final code review
- sprint task decomposition
- detailed API contract design
- post-implementation validation

Use other skills for those workflows.