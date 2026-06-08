# Gap Analysis

## Purpose
Turns a rough project brief, PRD, or feature spec into a buildable specification by running a four-stage question-and-answer process: identify gaps, stress-test assumptions, resolve product decisions, and rewrite the spec. Pauses at each stage to get your input before continuing.

## Use Cases
- A spec looks directionally right but you're not confident it's buildable — you want a structured challenge before handing it to engineering
- A brief has obvious holes (missing business rules, undefined permissions, no failure handling) and you need to surface and resolve them systematically
- You want to produce an improved, assumption-labeled spec without doing the analysis manually

## Inputs
Any of the following:
- A file path to a brief, PRD, or spec
- Pasted text of a feature description
- A URL pointing to a Confluence page or public doc

## Outputs
A structured improved spec containing all of the following additions over the original:
- Numbered business rules
- System states and transition table
- Permissions matrix
- Explicit edge case and failure handling
- Assumptions labeled as `[CONFIRMED]`, `[RECOMMENDED]`, or `[ASSUMED]`
- Open questions list

The improved spec is written back to the original input file (replace or append — your choice).

## Notes
Sanitized for public sharing. This skill is explicitly interactive — it asks you questions at each stage and waits for answers before proceeding. Skipping to the final spec is supported; unanswered questions are flagged as `[ASSUMED]`.
