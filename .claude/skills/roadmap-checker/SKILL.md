---
name: roadmap-checker

description: Check whether a project request, Salesforce change request (CR), or feature idea is already covered by something on the team's Azure DevOps (ADO) roadmap. Use this skill whenever the user mentions a CR, change request, project intake, new feature ask, "is this on the roadmap," "are we already doing this," "does this match our roadmap," or pastes a Salesforce CR / project description and asks if it overlaps with planned work. Also use when the user names a specific ADO Epic ID and wants to see what Features sit underneath it. The skill uses the ADO MCP server to find Epics flagged Roadmap=True (custom field or "Roadmap" tag), pulls their child Features, and reports matches with reasoning and direct ADO links.

---

Roadmap Checker
Helps a funded-dev project manager decide whether an incoming request — usually a Salesforce CR, project intake, or stakeholder ask — is already represented on the team's ADO roadmap. The Roadmap flag lives at the Epic level, so the skill pulls Roadmap Epics and walks down to their child Features for the full picture.

This skill assumes the Azure DevOps MCP server is connected. All ADO access goes through MCP tools — no PATs, no Python scripts, no az CLI.

When to trigger
Trigger when the user:

Pastes or summarizes a Salesforce CR, project request, or stakeholder ask and wants to know if it's already planned
Asks "is this on the roadmap?", "are we already doing this?", "what's slated for X area?"
Names a specific Epic ID and wants to see its Features (e.g., "what's under Epic 1088069?")
Wants a snapshot of all Roadmap=True Epics and what they cover
What "on the roadmap" means in this ADO instance
Based on the team's process template:

Epic work items can be flagged for the roadmap two ways. Check both:
A custom boolean field, typically Custom.Roadmap (shows as "Roadmap: True" in the Project Tracking section of the Epic form)
A tag with the literal text Roadmap
Features sit underneath these Epics via the standard parent/child hierarchy (System.LinkTypes.Hierarchy-Forward).
Other useful Epic fields visible on the form: System.AreaPath, System.IterationPath, Custom.InitiativeName, Custom.ProductArea, Custom.DeliveryStage, Microsoft.VSTS.Scheduling.StartDate, Microsoft.VSTS.Scheduling.TargetDate, Custom.ReadyForDevelopment (the "Ready" toggle), Microsoft.VSTS.Common.Priority.
If the WIQL query for Custom.Roadmap = True returns nothing or errors with an unknown-field message, the custom field reference name is different in this org — fall back to filtering by the Roadmap tag alone and tell the user.

Required setup (one-time check)
The user needs the Azure DevOps MCP server connected in Claude Code. If it isn't, the ADO tools won't be available in the tool list and the skill should tell the user:

"I don't see ADO MCP tools available. Install/enable the Azure DevOps MCP server (https://github.com/microsoft/azure-devops-mcp) in Claude Code first, then re-run."

When the MCP is connected, ADO tools appear with names like mcp__ado__wit_query_by_wiql, mcp__ado__wit_get_work_item, mcp__ado__wit_get_work_items_batch_by_ids, etc. Exact names vary by MCP build — list available tools first if uncertain.

Workflow
Step 1: Understand the request
Ask the user to share the CR/project text or the Epic ID, then identify the key signals:

Functional area (e.g., Transfer Merchandise, Daily Review, store ops, returns, pricing)
Action verbs (edit, create, view, delete, integrate, automate)
Product area (matches Custom.ProductArea values like "ERP - Enterprise Retail")
Specific named features the requester used that might also appear in Epic/Feature titles
If the user only gave a one-liner, ask one clarifying question — what part of the system does this touch? — before searching. No more than one.

Step 2: Identify the project and Epic field
Before the first WIQL run in a session, confirm the project name. Use the ADO MCP's project list tool (commonly mcp__ado__core_list_projects) if not already known. Based on the screenshot in this team's instance, area paths look like PDI\Retail\Team Monster, suggesting the project is PDI, but confirm rather than assume.

Step 3: Query Roadmap Epics with WIQL
Call the WIQL tool (commonly mcp__ado__wit_query_by_wiql) with this query first:

SELECT [System.Id], [System.Title], [System.State], [System.AreaPath],
       [System.IterationPath], [System.Tags],
       [Microsoft.VSTS.Scheduling.StartDate], [Microsoft.VSTS.Scheduling.TargetDate],
       [Microsoft.VSTS.Common.Priority]
FROM WorkItems
WHERE [System.TeamProject] = @project
  AND [System.WorkItemType] = 'Epic'
  AND [System.State] <> 'Removed'
  AND ([Custom.Roadmap] = true OR [System.Tags] CONTAINS 'Roadmap')
ORDER BY [Microsoft.VSTS.Scheduling.TargetDate] ASC
If this fails with an unknown-field error on Custom.Roadmap, retry with just the tag clause:

WHERE [System.TeamProject] = @project
  AND [System.WorkItemType] = 'Epic'
  AND [System.State] <> 'Removed'
  AND [System.Tags] CONTAINS 'Roadmap'
Tell the user which query succeeded so they know whether the field-based filter worked.

WIQL responses return only IDs plus the columns named in SELECT. To see full Epic details (description, all custom fields), pass the IDs to the batch-get tool (commonly mcp__ado__wit_get_work_items_batch_by_ids) with $expand=All or an explicit field list including System.Description, Custom.Roadmap, Custom.InitiativeName, Custom.ProductArea, Custom.DeliveryStage.

Step 4: Pull child Features for each Epic
For each Roadmap Epic, get its children. Two options depending on what the MCP exposes:

Option A — direct relations: call mcp__ado__wit_get_work_item with $expand=Relations for each Epic, then filter relations where rel == "System.LinkTypes.Hierarchy-Forward" and pull the target IDs. Batch-get those IDs for Feature titles/states.

Option B — WIQL with link query: some MCPs support queryType: "tree" WIQL. If available:

SELECT [System.Id], [System.Title], [System.WorkItemType], [System.State]
FROM WorkItemLinks
WHERE [Source].[System.Id] IN (<epic-ids>)
  AND [System.Links.LinkType] = 'System.LinkTypes.Hierarchy-Forward'
  AND [Target].[System.WorkItemType] = 'Feature'
MODE (MustContain)
Either approach is fine — pick whichever the MCP supports cleanly. Capture for each Feature: ID, Title, State, AreaPath, TargetDate.

Step 5: Match the request against roadmap items
With Epics + Features in hand, judge match strength against the user's request:

Strong match — Epic or Feature title/description directly names the same functionality (e.g., user asks about "editing transfer merchandise" and Epic 1088069 is "RSM: Daily Review - Edit Transfer Merchandise"). Note state — Waiting/Active means planned; Closed means shipped.
Partial match — Same product area or adjacent functionality (e.g., user asks about transfer receiving, roadmap covers transfer editing). Worth flagging as related.
No match — Different domain. Don't list these.
Be honest about confidence. If two roadmap items both partially fit, list both.

Step 6: Present results
Output a markdown table followed by short reasoning. Format:

## Roadmap matches for: <user's request in one line>

| Match | Epic / Feature | ID | State | Target | Link |
|-------|----------------|----|----|--------|------|
| Strong | RSM: Daily Review - Edit Transfer Merchandise (Epic) | 1088069 | Waiting | 5/1/2026 | [open](https://dev.azure.com/<org>/<project>/_workitems/edit/1088069) |
| Partial | <feature title> | <id> | Active | <date> | [open](...) |

### Reasoning
- **1088069** is a strong match — the request describes the same Edit Transfer Merchandise workflow Patricia owns. State is Waiting, target 5/1/2026, so it's planned but not started — your CR may want to attach to this Epic rather than spin up new work.
- **<id>** is a partial match because <reason>...

### Recommendation
<one short paragraph: attach to existing Epic, file as new work, or needs PM follow-up>
If nothing matches, say so plainly and list the closest 2–3 Roadmap Epics for routing context.

Get the org and project for link construction from the MCP project info call, or ask the user once and remember within the session.

Step 7: Reuse within a session
Roadmap data doesn't change minute-to-minute. If the user checks a second CR in the same session, reuse the Epic/Feature data already pulled rather than re-querying — unless the user says "re-check" or "I just added an Epic," in which case re-run Step 3.

Common follow-ups
"Show me everything under Epic X" — call wit_get_work_item for that Epic with relations expanded, batch-get its Features, present the same table format scoped to one Epic.
"What's the full Roadmap right now?" — run Step 3 alone, present every Roadmap Epic in a table grouped by Custom.InitiativeName if present, with target dates.
"Export this as a report" — write the markdown table + reasoning to a file (e.g. roadmap-match-<short-request>.md) and present it to the user.
"What's not on the roadmap but should be?" — out of scope; that's a planning discussion.
Field reference name quirks
ADO custom field reference names don't always match display labels. If Custom.Roadmap errors as unknown:

Fall back to [System.Tags] CONTAINS 'Roadmap' (the tag is visible in the screenshot near the comments — it's the same Epic, double-tagged).
To find the real reference name, fetch any Epic with $expand=All and look at the field keys returned — anything starting with Custom. whose value is a boolean and label is "Roadmap" is the right one. Tell the user the corrected reference name so they can update this skill.
Same goes for Custom.InitiativeName, Custom.ProductArea, Custom.DeliveryStage — these are the most likely names based on the form labels but may differ.

What this skill does NOT do
Doesn't create, edit, comment on, or transition work items — read-only.
Doesn't replace PM judgment. A "strong match" still needs a human to confirm scope alignment with the requester.
Doesn't pull from Salesforce. The user pastes the CR text; the skill doesn't reach into Salesforce.
Doesn't make recommendations about funding, staffing, or prioritization — only surfaces what's already planned.