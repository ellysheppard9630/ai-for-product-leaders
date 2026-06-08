# Roadmap Checker

## Purpose
Checks whether an incoming feature request, change request, or project idea is already covered by something on the team's ADO roadmap. Surfaces matching Epics and child Features, explains the match strength, and recommends whether to attach to existing work or file net-new.

## Use Cases
- A customer submits a feature request and you want to know if it's already planned before responding
- A stakeholder asks "are we already doing this?" and you need a fast, sourced answer
- You want a snapshot of all roadmap Epics and what they cover across a product area

## Inputs
Any of the following:
- A pasted change request or project description
- A one-line feature ask or stakeholder request
- A specific ADO Epic ID to drill into its child Features
- A product area name to scan for related planned work

## Outputs
- A markdown table of matching Epics and Features with match strength (Strong / Partial), state, target date, and direct ADO links
- Reasoning for each match
- A recommendation: attach to existing work, file as new, or escalate to PM for scope clarification

## Notes
Sanitized for public sharing. Requires an Azure DevOps MCP server connected in Claude Code. The skill queries ADO read-only — it does not create, edit, or transition work items. Internal field references (e.g., `Custom.Roadmap`, `Custom.ProductArea`) reflect one team's ADO process template and may need adjustment for other organizations.
