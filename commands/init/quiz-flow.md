# Interactive Quiz Flow

## Overview

The quiz is optional enrichment that runs after auto-detection and user confirmation. Every question is skippable. The quiz should take under 2 minutes if the user engages with all questions.

---

## Entry Point

After the user confirms the detection summary:
══════════════════════════════════════════════════════════
Would you like to provide additional context?
All questions are optional — press Enter to skip any.
(This helps produce more relevant scans and tickets.)

[Y / n]
══════════════════════════════════════════════════════════

If No: skip all questions, use defaults, proceed to config generation.
If Yes: present questions in order below.

---

## Questions

### Q1: Boundary Adjustments

Only ask if boundaries were detected.

Detected boundaries:

/apps/web — TypeScript, React (frontend)
/services/api — Python, FastAPI (backend)
/packages/shared — TypeScript (library)
Adjust these? [Enter to skip]
• Add a boundary: type path, language, framework, type
• Remove: type number to remove
• Edit: type number to edit
• Done: press Enter

---

### Q2: Team Priorities
How would you prioritize these categories for your project?
(Reorder by typing numbers, or Enter to use defaults)

Default order:

Security
Testing
Architecture
Performance
Code Quality
Observability
DevOps/CI/CD
Documentation
Dependencies
Accessibility
Standards
Data
Your order (e.g., "3,1,2,5,4,6,7,8,9,10,11,12"): [Enter to use defaults]

---

### Q3: Ticketing Tool
What ticketing tool does your team use?

Jira
Azure DevOps
Linear
GitHub Issues
GitLab Issues
Other
[Enter to skip]
Selection: ___

Project key or identifier: ___
URL (optional): ___

---

### Q4: Documentation Tool
Where does your team keep documentation?

Confluence
Notion
GitBook
In-repo (/docs)
Wiki (GitHub/GitLab)
Other
[Enter to skip]
Selection: ___

Space/workspace URL (optional): ___

---

### Q5: Standards & Style Guides
Do you have existing style guides or standards documents?
(Provide paths or URLs — these will be referenced during scans)

• Path or URL: ___
• Add another? [Y/n]

[Enter to skip]

---

### Q6: Rulesets
Do you have existing ruleset files to include?
(Markdown files defining team conventions per boundary/framework)

These go in .project-ingest/rulesets/ and are referenced during scans.

• Path to copy from: ___
• Add another? [Y/n]

[Enter to skip — you can add these later]

---

### Q7: Default Behavior Mode
When commands encounter uncertainty, should they:

Stop and ask (interactive)
Flag and continue (autonomous)
[Enter for autonomous (default)]

Selection: ___

---

### Q8: Additional Context
Anything else the team should know about this project?
(Known issues, history, migration context, constraints, etc.)

[Free text — Enter to skip]

---

## Defaults for Skipped Questions

| Question | Default |
|----------|---------|
| Boundaries | Use detected boundaries as-is |
| Priorities | Security, Testing, Architecture, Performance, Code Quality, Observability, DevOps/CI/CD, Documentation, Dependencies, Accessibility, Standards, Data |
| Ticketing | Not configured |
| Documentation | Not configured |
| Standards | None referenced |
| Rulesets | None |
| Behavior mode | autonomous |
| Additional context | None |

---

## Quiz Completion

After all questions (or skips):
══════════════════════════════════════════════════════════
✓ Got it. Generating configuration...
══════════════════════════════════════════════════════════

Proceed to config generation.