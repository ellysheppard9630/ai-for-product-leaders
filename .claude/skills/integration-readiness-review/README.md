# Integration Readiness Review

## Purpose
Pressure-tests integration-heavy work before engineering starts or before release confidence is assumed. Reviews cross-system workflows, API contracts, data dependencies, architecture concerns, and validation readiness in a single structured pass, then delivers a clear integration-readiness verdict.

## Use Cases
- A feature depends on multiple systems, vendors, or APIs and you want to know if the integration is actually ready before engineering picks it up
- A release is approaching and you need to assess whether integration assumptions are sound or whether there are gaps that could cause failures in production
- A workflow spans team or system boundaries and ownership, contracts, or failure modes are still ambiguous

## Inputs
Any of the following:
- A feature spec or PRD with integration dependencies
- An engineering handoff with service or API touchpoints
- API notes or vendor requirements
- Workflow descriptions covering multiple systems
- Architecture notes or data mapping details

## Outputs
A structured assessment covering:
1. Integration summary (systems, flow, data, dependencies, assumptions)
2. End-to-end integration review (handoffs, sequencing, failure modes, ownership)
3. Backend and API contract review (request/response expectations, validation, versioning)
4. Data and system-of-record review (entity relationships, mapping risks, quality issues)
5. Architecture and non-functional review (resiliency, security, observability, deployment risks)
6. QA and validation review (test scenarios, failure paths, environment concerns)
7. Cross-cutting integration risks appearing across multiple perspectives
8. Blockers vs manageable risks vs follow-ups
9. Integration-readiness verdict (ready / mostly ready / not ready yet)
10. Recommended next step

## Notes
Sanitized for public sharing. Internal agent role names (e.g., `dev-execution-integration-verifier`, `research-db-analyst`) are part of the skill's multi-agent orchestration framework and require a compatible Claude Code environment to execute.
