---
name: integration-readiness-review
description: review a feature, project, or spec for integration readiness using dev-execution-integration-verifier, dev-execution-api-developer, research-db-analyst, dev-planning-sr-architect, and research-qa-analyst. use when work depends on multiple systems, external vendors, service boundaries, data movement, or contract assumptions and the goal is to identify integration risks, ownership gaps, data issues, and validation needs before engineering or release.
---

Use this skill to pressure-test integration-heavy work before engineering starts or before release confidence is assumed.

This skill is for cross-system review. It is especially useful when a feature, workflow, or project depends on multiple services, vendors, APIs, databases, environments, or teams and you need to identify whether the work is actually ready from an integration standpoint.

Follow this workflow in order.

## Workflow overview

1. Understand and normalize the integration context
2. Review the end-to-end integration flow
3. Evaluate backend and API contract assumptions
4. Evaluate data dependencies and data quality risks
5. Evaluate architecture and non-functional integration concerns
6. Evaluate QA and validation readiness
7. Synthesize the final integration-readiness assessment

## Step 1: Understand and normalize the integration context

Accept flexible input. The user may provide:
- a feature spec
- a PRD
- an engineering handoff
- API notes
- workflow descriptions
- vendor requirements
- architecture notes
- data mapping details
- current-state and future-state flow descriptions
- a pasted document fragment

First, normalize the material into a working summary with:
- problem being solved
- target user or business process
- systems involved
- proposed end-to-end flow
- data being created, updated, moved, or read
- known dependencies
- known external or vendor touchpoints
- known constraints
- obvious assumptions
- areas that are still unclear

If the input is incomplete or rough, proceed anyway. Do not block unless there is too little information to identify the systems or workflows involved. If needed, make the best possible interpretation and explicitly label assumptions.

## Step 2: Review the end-to-end integration flow

Use `dev-execution-integration-verifier` to analyze whether the proposed workflow is viable across systems.

Focus on:
- end-to-end data and control flow
- handoffs between systems
- dependency timing and sequencing
- ownership of each integration touchpoint
- retries, fallbacks, and timeout handling
- what happens when one system partially fails
- environment and configuration dependencies
- assumptions that are not yet explicit but would matter in delivery or release

This step should establish whether the real integrated workflow holds together, not just whether the interfaces look plausible.

## Step 3: Evaluate backend and API contract assumptions

Use `dev-execution-api-developer` to review the backend and contract implications.

Focus on:
- request and response expectations
- contract completeness
- validation rules
- auth and permission requirements
- idempotency, pagination, filtering, and error semantics when relevant
- versioning or backwards-compatibility concerns
- contract assumptions that may break downstream consumers
- missing backend detail that would create integration risk

If the proposal has little or no meaningful API or service contract component, keep this section concise and say so clearly.

## Step 4: Evaluate data dependencies and data quality risks

Use `research-db-analyst` to review the data implications of the integration.

Focus on:
- key entities and relationships involved in the flow
- system-of-record assumptions
- data mapping concerns
- nullability, uniqueness, and integrity risks
- transformation or synchronization risks
- downstream reporting implications
- data quality or lineage issues that could affect the integration
- whether multiple systems appear to own the same concept inconsistently

This step should identify whether the integration is data-safe, not just technically possible.

## Step 5: Evaluate architecture and non-functional integration concerns

Use `dev-planning-sr-architect` to assess the deeper design implications.

Focus on:
- service boundaries
- dependency coupling
- reliability and resiliency concerns
- scalability implications
- security and access-control concerns
- observability, logging, and supportability needs
- deployment or environment risks
- whether the integration design is underdefined in ways that could create operational pain later

This step should identify system-level weaknesses that may not be visible in a feature-only review.

## Step 6: Evaluate QA and validation readiness

Use `research-qa-analyst` to determine whether the integration can be validated confidently.

Focus on:
- critical test scenarios
- success and failure paths
- data reconciliation needs
- permission and workflow validation
- environment-specific testing concerns
- edge cases involving retries, duplicates, partial failures, and stale data
- whether QA and UAT would know how to verify the integration
- what validation is missing before release confidence is justified

This step should make sure the integration is verifiable, not just theoretically correct.

## Step 7: Synthesize the final integration-readiness assessment

Synthesize all findings into a clear integration-readiness assessment.

Explicitly identify:
- what looks sound
- where the biggest risks are
- ownership gaps
- contract gaps
- data risks
- failure mode concerns
- blockers vs manageable risks
- assumptions that must be validated before engineering or release
- what needs to be clarified, tested, or redesigned

Do not merely stack the agent reviews together. Resolve overlap, highlight reinforcing concerns, and produce one practical readiness judgment.

## Output format

Use this exact section structure unless the user asks for something different:

# Integration Readiness Review

## 1. Integration summary
- problem
- target workflow or business process
- systems involved
- proposed end-to-end flow
- data involved
- known dependencies
- key assumptions

## 2. End-to-end integration review
Summarize the most important findings from `dev-execution-integration-verifier`.

## 3. Backend and API contract review
Summarize the most important findings from `dev-execution-api-developer`.

## 4. Data and system-of-record review
Summarize the most important findings from `research-db-analyst`.

## 5. Architecture and non-functional review
Summarize the most important findings from `dev-planning-sr-architect`.

## 6. QA and validation review
Summarize the most important findings from `research-qa-analyst`.

## 7. Cross-cutting integration risks
Identify patterns or risks that appear across multiple perspectives.

## 8. Blockers vs manageable risks
Separate:
- blockers before engineering or release
- high-priority risks
- manageable follow-ups

## 9. Integration-readiness verdict
State clearly whether the work is:
- ready
- mostly ready with targeted fixes
- not ready yet

Explain why.

## 10. Recommended next step
Recommend the most appropriate next action, such as:
- proceed with integration planning
- clarify ownership
- define missing contracts
- validate data mappings
- add failure-mode handling
- improve test coverage
- redesign a risky dependency pattern

## Synthesis rules

- Do not assume a connected workflow is a validated workflow.
- Do not treat interface shape as proof that the integration will work end to end.
- Do not ignore data quality, system-of-record, or ownership ambiguity.
- Distinguish blockers from ordinary implementation follow-up.
- Make assumptions explicit.
- Elevate repeated concerns that appear across reviewers.
- Focus on operational reality, not just design intent.
- Keep the output practical for a technical PM, architect, or engineer preparing integration-heavy work.
- If the integration appears strong, say so clearly, but still identify residual risk and validation needs.

## Good use cases

Use this skill for:
- third-party integrations
- multi-service workflows
- vendor-dependent features
- API and event-driven flows
- data synchronization projects
- cross-team system changes
- release reviews for integration-heavy work

## Not ideal for

This skill is less useful for:
- raw discovery notes
- pure UI-only features
- early brainstorming without defined systems
- final code review
- sprint task decomposition
- non-technical customer value debates

Use other skills for those workflows.