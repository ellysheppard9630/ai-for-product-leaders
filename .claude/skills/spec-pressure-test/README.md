# Spec Pressure Test

## Purpose
Challenges a feature spec, PRD, or engineering handoff from five independent angles — product management, senior architecture, senior developer feasibility, QA, and integration — before it reaches engineering. Surfaces blockers, hidden risks, and refinement needs in a single pass.

## Use Cases
- A spec looks nearly ready but you want it challenged before handing it off — you'd rather find the gaps now than during sprint planning
- A high-risk or integration-heavy feature needs a structured pre-handoff review across multiple disciplines
- You want to know whether a spec is engineering-ready or what specifically needs to be fixed first

## Inputs
Any of the following:
- A PRD or feature spec
- A requirements draft
- An engineering handoff summary
- Acceptance criteria
- Workflow notes or a pasted document fragment

## Outputs
A structured assessment covering:
1. Spec summary
2. PM review (scope clarity, requirement quality, non-scope definition)
3. Architecture review (system boundaries, design risk, non-functional concerns)
4. Implementation feasibility review (buildability, hidden complexity, sequencing)
5. QA and testability review (acceptance criteria quality, edge cases, validation gaps)
6. Integration review (cross-system risk, contract assumptions, failure modes)
7. Cross-cutting risks appearing across multiple perspectives
8. Blockers vs refinements vs lower-risk follow-ups
9. Engineering-readiness verdict (ready / mostly ready / not ready yet)
10. Recommended next step

## Notes
Sanitized for public sharing. Internal agent role names (e.g., `dev-planning-sr-architect`, `research-qa-analyst`) are part of the skill's multi-agent orchestration framework and require a compatible Claude Code environment to execute.
