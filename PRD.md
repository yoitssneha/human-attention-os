# Human Attention OS — PRD

## 1. Product brief

Human Attention OS is a Sarvam-native internal system that reduces coordination overhead by turning everyday communication into reliable execution. It handles predictable communication and operational follow-through, and involves people only when judgment or accountability is required.

This first version is an internal dogfooding product for Sarvam—not a general-purpose AI employee and not a replacement for existing workplace tools.

## 2. User and problem

### Primary user

Sarvam employees and managers who spend time chasing updates, converting conversations into tasks, sending routine follow-ups, and finding the context needed to make decisions.

### Problem

Important work is distributed across meetings, chats, email, documents, and informal conversations. People spend too much time coordinating the work instead of doing the work. Existing AI tools usually summarize communication; they do not reliably carry routine actions through to completion.

## 3. Product hypothesis

If Sarvam employees can communicate naturally with a context-aware assistant, and that assistant can safely execute predictable follow-through, then employees will spend less time on coordination and more time on high-value judgment and execution.

## 4. MVP scope

### Core workflow: conversation to closure

The MVP focuses on internal meetings and follow-ups:

1. Ingest an approved meeting transcript, notes, or voice recording.
2. Transcribe and identify the language using Sarvam APIs.
3. Extract decisions, action items, owners, deadlines, dependencies, and uncertainty.
4. Present the proposed actions for confirmation.
5. Send a concise follow-up to the relevant people.
6. Track status and ask for updates through an approved channel.
7. Escalate overdue or blocked items to the correct owner or manager.
8. Provide a daily summary of completed, blocked, overdue, and human-attention items.

### Supported interaction

- Text-first web interface for the initial pilot.
- Voice input and spoken summaries using Sarvam speech APIs.
- English, Hindi, and Hinglish initially; expand only after evaluation.
- Human confirmation before external or high-impact actions.

### Initial integrations

Use the fewest integrations necessary for a meaningful pilot:

- One meeting/transcript source.
- One internal messaging channel.
- One task or issue tracker.
- A lightweight internal context store for people, teams, projects, and permissions.

The exact tools should be selected based on what Sarvam already uses and can safely expose to a prototype.

## 5. What is feasible now

| Capability | MVP decision | Reason |
|---|---|---|
| Multilingual speech-to-text | Build | Directly aligned with Sarvam’s APIs |
| Translation, transliteration, and code-mixed input | Build selectively | Strong Sarvam differentiation |
| Action and deadline extraction | Build | Clear value and technically manageable |
| Drafting follow-up messages | Build | Low-risk with confirmation |
| Task creation and reminders | Build | Makes the product operational, not just summarization |
| Overdue escalation | Build with rules | Deterministic and measurable |
| Daily attention/exception briefing | Build | Demonstrates the core vision |
| Context-aware responses | Build narrowly | Start with structured company context |
| Voice command to create an action | Build as a pilot feature | Strong product identity, but limit commands |
| Fully autonomous routine follow-through | Pilot carefully | Requires permissions, logging, and confidence thresholds |

## 6. What is not feasible for the first version

- Understanding all company knowledge without curated sources.
- Replacing Slack, email, project management, CRM, or ERP systems.
- Acting autonomously across every company system.
- Making sensitive HR, finance, legal, hiring, or customer commitments.
- Perfectly inferring ownership when the conversation is ambiguous.
- Building a general-purpose agent for every employee workflow.
- Supporting every Indian language on day one.
- Monitoring every private conversation by default.
- Measuring productivity by surveillance or employee activity tracking.
- Building a standalone telephony or WhatsApp platform before proving the workflow.

## 7. What we should build

### A. Context layer

Create a permissioned, structured representation of:

- people and roles;
- teams and reporting relationships;
- projects and priorities;
- common workflows;
- approved communication channels;
- action ownership and escalation rules.

The system should retrieve only the context needed for a task and clearly show its source.

### B. Action layer

Represent every extracted commitment as a durable object:

```json
{
  "title": "Send enterprise demo proposal",
  "owner": "person_id",
  "due_date": "2026-10-02",
  "status": "needs_confirmation",
  "source": "meeting_id",
  "confidence": 0.91,
  "escalation_rule": "manager_after_2_days_overdue"
}
```

### C. Human-attention layer

The main interface should not be an activity feed. It should be an exception inbox containing:

- decisions waiting for the user;
- blocked or overdue work;
- ambiguous ownership or deadlines;
- actions requiring approval;
- high-impact changes;
- relevant context and recommended next steps.

### D. Safety and trust layer

- Explicit permissions by user and system.
- Confirmation thresholds based on action risk.
- Full audit trail for every automated action.
- Confidence scores and visible source context.
- Easy undo or correction where possible.
- No silent sending of sensitive messages.
- Clear retention and deletion controls for audio and transcripts.

## 8. What we should not build

- A new chat platform.
- A new project-management system.
- A broad autonomous “AI employee.”
- A custom foundation model.
- A universal company knowledge graph before validating use cases.
- A polished consumer app before internal dogfooding.
- Dozens of connectors before one workflow shows measurable value.
- Automation that optimizes message volume instead of human attention.

## 9. Success metrics

### Pilot outcome metrics

- Reduction in time spent creating and sending follow-ups.
- Percentage of extracted actions confirmed as correct.
- Percentage of actions completed on time.
- Reduction in overdue or ownerless actions.
- Time from conversation end to action creation.
- Number of routine coordination messages handled automatically.
- Percentage of escalations that genuinely require human attention.

### Guardrail metrics

- Incorrect owner assignment rate.
- Incorrect deadline or intent rate.
- Unauthorized action rate: target zero.
- User correction and override rate.
- False escalation rate.
- Audio/transcript privacy incidents: target zero.

## 10. Pilot plan

### Phase 0 — Discovery and baseline

Interview 8–12 Sarvam employees across functions. Map recurring coordination workflows and establish a baseline for follow-up time, overdue actions, and approval delays.

### Phase 1 — Read-only intelligence

Process approved transcripts or notes. Extract decisions and actions, but do not send or update anything automatically. Measure extraction quality and user trust.

### Phase 2 — Confirmed execution

Allow users to approve drafted messages, create tasks, and schedule reminders. Add audit logs and corrections.

### Phase 3 — Bounded autonomy

Permit low-risk actions to execute automatically when confidence and permissions meet defined thresholds. Keep high-impact actions human-approved.

### Phase 4 — Internal expansion decision

Decide whether the product should remain an internal operating layer, become a customer reference application, or evolve into a broader platform capability.

## 11. Intern-sized deliverable

The first project should deliver a working vertical slice, not the whole vision:

> **One multilingual conversation source → structured actions → confirmed follow-up → status tracking → overdue escalation → attention briefing.**

The intern’s highest-value contribution is to identify the right operational workflow, design the context and permission model, measure the before/after impact, and produce a credible Sarvam-native prototype.

## 12. Product boundary

The product succeeds when it makes people less busy with communication—not when it automates the maximum number of actions.

The governing rule is:

> **Automate what is predictable. Escalate what is consequential. Protect human attention.**

