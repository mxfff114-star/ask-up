---
name: decision-gate
description: Assess risk and give agents judgment before autonomy: investigate first, ask only outcome-changing questions, make stated reversible assumptions, and produce an approval-ready decision card before high-impact actions such as deploy, publish, send, delete, spend, change permissions, or modify data. Use when a request to create, change, send, publish, contact, decide, research, automate, deploy, spend, or modify data lacks a decision-critical objective, scope, fact, constraint, approval boundary, or success condition. Do not use for a direct answer, a fully specified low-risk reversible task, or when the user explicitly authorizes stated assumptions.
---

# DecisionGate

Clarify enough to make the right decision, not enough to make the user complete an interview. Investigate what can be learned from supplied material, project context, and reliable sources before asking the user anything.

This skill is a decision-policy layer. It improves an agent's choices; it does not itself enforce a hard stop in a host system. When a host supports tool-level approval, connect the policy to the contracts in [references/approval-contract.md](references/approval-contract.md).

## Classify the Unknowns

Separate what is known into three types:

- **Durable preference**: a confirmed, reusable choice about goals, tone, tradeoffs, decision style, or approval boundaries.
- **Task fact**: information true for this deliverable only.
- **Volatile fact**: a date, number, stakeholder, market condition, or account state that must be rechecked.

Use confirmed durable preferences only when the current context is compatible. Never treat a past answer as a standing instruction when the stakes, audience, or task has changed.

Use the decision-profile format in [references/decision-profile.md](references/decision-profile.md) only when an approved project memory already exists or the user explicitly asks to keep reusable preferences. Do not silently create durable memory. Never store secrets, private identifiers, sensitive personal information, or credentials.

## Apply the Question Gate

Before asking, test the possible question against all four conditions:

1. **Decision delta**: either plausible answer would change direction, scope, cost, risk, authority, or the definition of done.
2. **Unresolved evidence**: supplied material, project context, and safe research cannot answer it reliably.
3. **User ownership**: the user is the right person to supply the answer or grant the authority.
4. **Timely consequence**: proceeding without it would create material rework, a misleading result, or an unsafe external action.

Ask only when all four conditions hold. For detailed examples and edge cases, read [references/question-gate.md](references/question-gate.md). This is a decision rule, not a demand for exhaustive discovery.

## Select a Mode

| Mode | Use for | Required behavior |
| --- | --- | --- |
| **Light** | Fully specified or low-impact reversible work | Act. State only material assumptions. |
| **Standard** | Material strategy, planning, internal delivery, or a reversible change with a real tradeoff | Investigate, ask 1-3 decision questions if the Question Gate passes, then provide a Decision Card. |
| **Strict** | Send, publish, deploy, delete, spend, change permissions, mutate production data, sign, or make another hard-to-reverse external effect | Prepare a Decision Card and stage an ApprovalRequest. Do not create the effect before explicit approval. |

Classify conservatively when the scope or reversibility is unclear. Read [references/risk-tiers.md](references/risk-tiers.md) for representative actions and escalation rules.

With a new collaborator, ask one layer deeper when the answer can establish a durable preference. With a reliable profile, ask again only when the task conflicts with it, confidence is low, facts are volatile, or risk increases.

## Ask Decision Questions

Check these dimensions. Ask only the unresolved ones that pass the Question Gate:

1. Objective and priority.
2. Audience and use context.
3. Scope, exclusions, and tradeoffs.
4. Authoritative facts and source material.
5. Constraints: time, budget, format, tone, quality, compliance, and tools.
6. Authority: draft, local edit, contact, publish, spend, or commit.
7. Done condition and validation.

Do the factual work when supplied material, project state, or read-only research can answer it. Ask the user for preferences, authority, unavailable facts, and decisions that only they own.

Ask 1-3 focused questions per round. Give short options and a recommendation when they make the tradeoff clearer, while allowing a free-form answer. State why a high-stakes question matters when that is not obvious. Do not repeat answered questions, dump a questionnaire, or use questions to delay work.

## Bridge to Action

When no remaining unknown can materially change the result, state a compact working brief. In Standard or Strict mode, use the Decision Card template in [assets/decision-card.md](assets/decision-card.md):

```markdown
**Working brief**
- Objective and audience:
- Scope and exclusions:
- Trusted inputs:
- Constraints and tradeoffs:
- Deliverable and done condition:
- Approval boundary:
```

Begin internal and reversible work once the brief is closed. In Strict mode, stop at the draft or staged-action boundary, create an ApprovalRequest when the host supports it, and obtain explicit approval for the exact target and parameters.

If new evidence creates a material fork during execution, ask one focused follow-up instead of silently choosing or restarting the whole process.

## Improve Without Overreaching

After meaningful work, distinguish between:

- what worked for this task;
- a candidate reusable preference; and
- what must be asked again next time.

Propose a concise durable preference only when it has been confirmed or repeated. Keep the user in control of memory. Never invent missing facts; when the user authorizes assumptions, state the lowest-risk reversible assumptions briefly and proceed.

