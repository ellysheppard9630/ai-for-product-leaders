---
name: discovery-to-prd
description: turn messy discovery inputs into a structured prd-ready output using dev-planning-researcher, research-planner, research-db-analyst, research-qa-analyst, and dev-planning-lead-product-manager. use when the input is a mix of notes, stakeholder asks, research findings, workflow problems, data questions, or early requirements and the goal is to synthesize them into a clear product direction, requirement structure, open questions, and prd-ready recommendations.
---

Use this skill to transform messy discovery into a structured, decision-useful product requirements draft.

This skill is for early-to-mid stage product work, before engineering handoff. It is especially useful when the input is incomplete, fragmented, contradictory, or spread across multiple sources and you need to turn it into a clearer PRD direction.

Follow this workflow in order.

## Workflow overview

1. Understand and normalize the discovery input
2. Run technical and requirements discovery analysis
3. Synthesize the research into themes and gaps
4. Evaluate data implications
5. Evaluate QA and testability implications
6. Shape the findings into product direction
7. Produce a PRD-ready output

## Step 1: Understand and normalize the discovery input

Accept flexible input. The user may provide:
- rough notes
- stakeholder requests
- research findings
- current-state workflow descriptions
- problem statements
- meeting notes
- support themes
- user pain points
- data questions
- early requirements
- pasted document fragments

First, normalize the material into a working summary with:
- problem being discussed
- target user or customer
- current pain points or unmet needs
- known business goals
- proposed ideas or requirements already mentioned
- known constraints
- obvious assumptions
- unresolved questions

If the input is messy, incomplete, or contradictory, proceed anyway. Do not block unless there is no identifiable product problem at all. If needed, make the best possible interpretation and clearly label assumptions.

## Step 2: Run discovery analysis

Use `dev-planning-researcher` to analyze the input as a discovery problem.

Focus on:
- what is already known
- what is only assumed
- what is missing
- what themes are emerging
- what questions still matter before a good PRD can be written
- whether the input reflects a real problem, a requested solution, or both

This step should orient the work toward structured product understanding rather than just summarizing notes.

## Step 3: Run research synthesis and planning

Use `research-planner` to consolidate the discovery findings into decision-useful structure.

Focus on:
- grouping findings into themes
- identifying contradictions
- highlighting blockers and dependencies
- showing what research is sufficient vs still incomplete
- recommending what should be clarified before finalizing a PRD
- organizing the input into a logical planning sequence

This step should turn scattered discovery into a usable planning foundation.

## Step 4: Evaluate data implications

Use `research-db-analyst` when the proposal has any data, reporting, workflow, or system-of-record implications.

Focus on:
- key entities, fields, or data relationships implied by the proposal
- data dependencies that affect requirements
- reporting or downstream impacts
- data quality or completeness risks
- whether important business logic depends on poorly understood data structure
- what data assumptions need validation before writing strong requirements

If the proposal has little or no meaningful data component, keep this section concise and say so clearly.

## Step 5: Evaluate QA and testability implications

Use `research-qa-analyst` to identify what would make the eventual requirements hard or easy to validate.

Focus on:
- whether the likely feature direction is testable
- missing acceptance conditions
- edge cases already implied by discovery
- unclear workflow branches
- permission, validation, or state-transition concerns
- what needs to be clarified now to avoid weak PRD language later

This step should improve requirement quality before engineering sees anything.

## Step 6: Shape the findings into product direction

Use `dev-planning-lead-product-manager` to turn the discovery into product structure.

Focus on:
- defining the likely problem statement
- clarifying target user and user value
- identifying likely scope and non-scope
- separating actual requirements from ideas, assumptions, and preferences
- highlighting tradeoffs and prioritization pressure
- recommending the most coherent direction for a PRD draft

This step should convert analysis into product decision framing.

## Step 7: Produce the final PRD-ready output

Synthesize the findings from all agents into a structured output that a technical PM can use to begin or improve a PRD.

The result should not pretend every unknown is resolved. It should make uncertainty visible while still creating a practical and usable requirements draft direction.

The final output must help answer:
- what problem are we solving
- for whom
- why it matters
- what the likely requirements are
- what constraints or dependencies exist
- what still needs clarification before engineering handoff

## Output format

Use this exact section structure unless the user asks for something different:

# Discovery to PRD

## 1. Discovery summary
- problem or opportunity
- target user or customer
- business context
- current pain points
- proposed direction
- key assumptions

## 2. Findings by theme
Group the discovery into the most important themes.

## 3. Confirmed facts vs assumptions
Separate:
- confirmed facts
- likely assumptions
- unresolved questions

## 4. Data and workflow implications
Summarize the most important findings from `research-db-analyst`.

## 5. QA and testability considerations
Summarize the most important findings from `research-qa-analyst`.

## 6. Product direction
Summarize how `dev-planning-lead-product-manager` would frame the problem, target user, value, and likely scope.

## 7. PRD-ready requirement draft
Provide a first-pass requirement structure, including:
- objective
- target user
- user need
- proposed capability
- expected outcomes
- constraints
- dependencies

## 8. Scope and non-scope
Provide a best-effort draft of:
- in scope
- out of scope
- likely later-phase items

## 9. Open questions and risks
List the most important unanswered questions and planning risks.

## 10. Recommended next step
Recommend the most appropriate next action, such as:
- write the full PRD
- validate assumptions with stakeholders
- clarify data dependencies
- define acceptance criteria
- narrow scope before proceeding

## Synthesis rules

- Do not treat stakeholder asks as fully formed requirements.
- Do not treat assumptions as facts.
- Do not simply summarize notes; synthesize them into decision-useful structure.
- Preserve ambiguity where it matters, but do not let ambiguity prevent progress.
- Keep the output practical for a technical PM writing a PRD.
- Favor clarity, scope definition, and requirement quality over verbosity.
- If multiple interpretations are possible, state the leading interpretation and note the alternatives.
- If the discovery suggests the wrong problem is being solved, say so clearly.

## Good use cases

Use this skill for:
- messy discovery notes
- early feature exploration
- stakeholder requirement intake
- product problem framing
- turning research into a PRD outline
- organizing fragmented findings before spec writing
- preparing product direction before engineering involvement

## Not ideal for

This skill is less useful for:
- final architecture design
- implementation planning
- story decomposition
- API contract design
- detailed integration verification
- late-stage delivery coordination

Use other skills for those later-stage workflows.