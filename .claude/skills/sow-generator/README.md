# SOW Generator

## Purpose
Validates a funded development estimate package and generates a customer-ready Statement of Work. Treats the Product Owner's estimate as a working hypothesis — not a source of truth — and cross-validates it against available sources (CRM, project tracking, design, discovery docs) before producing a Gap Analysis, SOW Readiness Score, and final SOW artifacts.

## Use Cases
- A customer has expressed interest in funding a feature and you need to produce a formal SOW
- An estimate package exists but you're not confident the scope, acceptance criteria, or design are fully aligned — you want a structured validation before the document goes external
- You want to identify change-order risk before a SOW is signed, not after

## Inputs
Any of the following (at minimum, a CR number or estimate summary):
- A change request number (used to pull CRM and project tracking data automatically)
- A PO estimate package (scope summary, proposed solution, acceptance criteria, hours/cost estimate, assumptions)
- A Figma link or design summary
- A prior discovery report, if one exists

## Outputs
When the readiness gate passes, the skill produces:
1. **Gap Analysis** — scope, acceptance, design, sales-expectation, and dependency gaps
2. **Challenge Questions** — targeted questions for the PO on unresolved gaps
3. **SOW Readiness Score** — 0–100 per category with a Green / Yellow / Red verdict
4. **Risk Assessment Package** — residual risks with mitigations written into the SOW
5. **Executive Summary** — one-page leadership and account-team view
6. **Internal PM Review Package** — full validation working record
7. **Customer-Ready SOW** — bounded scope, exclusions, acceptance criteria, estimate, and project closure conditions

If critical issues remain unresolved, the skill outputs a SOW Readiness Failure with required actions instead of a SOW.

## Notes
Sanitized for public sharing. In its original form, this skill integrates with Salesforce, ADO, Confluence, and Figma via MCP servers. In a general-purpose setup, those source validations are replaced by user-provided inputs. The core validation framework and output structure are fully transferable. References to specific billing rates and internal tooling have been removed from this README.
