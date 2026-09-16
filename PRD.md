# Human Attention OS — First-Principles PRD

## 1. First principle

As AI becomes capable of handling more communication and execution, human attention becomes the scarce resource.

> **Humans should spend their time and energy on what requires human judgment. AI should handle the rest.**

Human Attention OS is a context-aware execution layer that protects human attention. It understands what is happening across an organization, handles predictable communication and follow-through, and involves people only when their judgment, creativity, empathy, accountability, or relationships are genuinely needed.

This is a pre-AGI product, but the principle remains relevant as AI becomes more capable: humans must learn to live and work alongside AI without spending their lives coordinating it.

## 2. The Sarvam insight

India’s AI-native organizations will not be built only around English, keyboards, dashboards, and standardized software workflows.

They will be multilingual, voice-heavy, code-mixed, distributed, and connected through many channels. Language diversity should not create operational fragmentation.

> **Sarvam can make organizational execution language-independent: people communicate naturally, while AI converts intent into common executable actions.**

This is the Sarvam-native opportunity—not another English-first meeting assistant, but a multilingual language-to-execution layer for organizations.

```text
Any language / voice / channel
            ↓
Sarvam understands intent and context
            ↓
Common executable action
            ↓
AI coordinates and follows through
            ↓
Human attention only when necessary
```

## 3. Product definition

Human Attention OS is a Sarvam-native system that learns what matters to people and organizations, handles everything operationally predictable, and surfaces only high-value human work.

It is not:

- a meeting-notes product;
- a new chat platform;
- a project-management replacement;
- a generic AI employee;
- an employee-surveillance system.

It is an **attention allocation and execution layer** that sits above existing communication and work systems.

## 4. The problem

People spend too much time on work around work:

- writing routine messages;
- repeating context;
- coordinating across teams;
- finding owners;
- scheduling and rescheduling;
- chasing updates;
- asking for status;
- copying information between tools;
- escalating overdue work;
- deciding which notifications deserve attention.

Existing AI tools often summarize communication. They do not reliably carry predictable work through to completion or decide whether an item deserves human attention in the first place.

## 5. Core product insight: the Human Attention Firewall

The system should not only automate work after it reaches a human. It should decide whether that work deserves to reach a human at all.

Every incoming request, message, meeting invite, escalation, or task is evaluated against context, urgency, value, risk, and the person’s role.

The system can:

- resolve it automatically;
- delegate it;
- batch it;
- defer it;
- decline or remove it;
- ask one focused clarification question;
- surface it to the right human with the relevant context.

```text
Incoming communication
        ↓
AI understands language, intent, context, and risk
        ↓
Resolve / delegate / batch / defer / decline
        ↓
Human attention only when justified
```

## 6. Initial users and wedge

### Initial users

Start with **Sarvam Strategy & Operations**, then validate with Partnerships and Sales.

These teams are the right starting point because they coordinate across functions, manage many follow-ups, work across multiple tools, and can measure operational improvement.

### First workflow

Automate **cross-functional initiative follow-through**:

```text
Conversation
→ commitment identified
→ owner and deadline assigned
→ follow-up sent
→ progress checked
→ completion evidence verified
→ delay escalated
→ action closed
```

This begins where existing meeting AI usually stops.

### Hero outcome

> **Routine communication happens without human involvement, while overdue and blocked work decreases.**

## 7. MVP scope

The MVP accepts approved inputs from meeting notes, transcripts, recordings, email threads, and Slack or internal chat messages.

It then:

1. Identifies commitments, decisions, requests, owners, deadlines, dependencies, and uncertainty.
2. Converts commitments into structured actions.
3. Uses company and personal context to propose the correct owner and priority.
4. Drafts or sends low-risk internal follow-ups.
5. Creates tasks in one connected task system.
6. Requests status updates at context-aware times.
7. Verifies completion through explicit confirmation and system evidence.
8. Escalates blocked or overdue work.
9. Provides a daily human-attention briefing.

## 8. Interaction model

- **Voice:** delegate work, give updates, ask questions, and report completion.
- **Text:** correct, clarify, and instruct the system.
- **Web:** review actions, context, permissions, and exceptions.
- **Background automation:** handle approved routine work.
- **Exception inbox:** show decisions, risks, ambiguity, blocked work, and high-value human actions.

The primary experience is not an activity feed. It is a focused view of what actually needs the person.

## 9. Context and learning

The system needs a permissioned context layer containing people and roles, teams and reporting relationships, projects and priorities, responsibilities and ownership patterns, policies and approval rules, communication preferences, deadlines and dependencies, connected systems and available actions, and relevant documents and approved conversation history.

It learns at two levels:

### Personal context

What an individual prefers to automate, review, delay, delegate, or escalate.

### Organizational context

How Sarvam works, who owns what, which workflows exist, and what policies apply.

Learning signals include explicit approvals, corrections, rejections, user instructions, repeated edits, ignored notifications, accepted suggestions, delegation patterns, and response behavior.

Explicit instructions are stronger than inferred behavior. Inferences remain provisional until confirmed.

## 10. Autonomy and trust

### Automatic

- Low-risk internal reminders
- Routine status checks
- Approved follow-up messages
- Task creation
- Daily summaries
- Low-risk scheduling
- Updates to connected task systems

### Confirmation required

- Ambiguous ownership
- Changed deadlines
- Important internal messages
- Manager escalations
- Shared project updates

### Human approval required

- External communication
- Customer or partner commitments
- Financial, legal, HR, or hiring actions
- Sensitive information
- Irreversible actions
- High-impact decisions

The system must not guess when uncertainty could create operational, reputational, or safety risk.

Required controls include explicit user and administrator permissions, role-based access, visible source context, confidence scores, a complete action audit trail, easy correction and undo where possible, retention and deletion controls for audio and transcripts, and zero tolerance for unauthorized actions.

## 11. Sarvam-native architecture

```text
Sarvam speech, language, translation, and voice capabilities
                         ↓
Context, memory, permissions, and policy layer
                         ↓
Intent, commitment, risk, and attention classification
                         ↓
Action and workflow execution layer
                         ↓
Connected company tools
                         ↓
Exception inbox and human feedback
```

Sarvam’s differentiation is the combination of Indian-language speech and text understanding, voice-first interaction, code-mixed communication, translation and transliteration, language-independent intent extraction, enterprise permissions and context, and reliable execution and follow-through.

The product should dogfood Sarvam’s own models and Voice Agent capabilities internally, then become a reference architecture for multilingual enterprise operations.

## 12. What to build now

- A simple internal web application.
- Voice input and spoken summaries.
- Approved meeting, email, and Slack inputs.
- Structured commitment extraction.
- Owner, deadline, priority, and dependency detection.
- Follow-up drafting.
- One task-system integration.
- Status collection and evidence-based completion.
- Adaptive reminders.
- Escalation rules.
- Exception inbox.
- Personal and organizational feedback loops.
- Audit history and permissions.

## 13. What not to build now

- A replacement for Slack, email, or project-management tools.
- A generic autonomous AI employee.
- Continuous monitoring of private conversations.
- Autonomous external communication.
- Sensitive finance, HR, legal, hiring, or customer decisions.
- Every department and workflow at once.
- Every Indian language on day one.
- A standalone telephony or WhatsApp platform.
- A custom foundation model.
- A universal knowledge graph before validating the workflow.
- Dozens of integrations before one workflow shows measurable value.
- Automation that increases message volume instead of protecting attention.

## 14. Pilot plan

### Phase 0 — Discover

Interview 8–12 Strategy & Operations users. Map recurring coordination work, current tools, delays, approval patterns, and the baseline time spent on follow-ups.

### Phase 1 — Observe

Process approved inputs in read-only mode. Extract actions and propose owners, deadlines, messages, and escalation rules. No autonomous actions.

### Phase 2 — Assist

Allow users to approve messages, create tasks, request updates, and schedule reminders. Add audit logs, corrections, and user feedback.

### Phase 3 — Execute safely

Allow low-risk internal actions to run automatically when permissions, confidence, and reversibility thresholds are satisfied.

### Phase 4 — Expand

Validate with Partnerships or Sales. Only then decide whether to make this an internal operating layer, a Sarvam reference application, or a broader platform capability.

## 15. Success metrics

### Outcome metrics

- Reduction in time spent on routine follow-ups.
- Reduction in overdue commitments.
- Reduction in ownerless actions.
- Faster time from conversation to execution.
- Percentage of routine communication handled automatically.
- Percentage of escalations that genuinely require human attention.
- User-reported reduction in cognitive load.

### Quality and trust metrics

- Correct owner assignment rate.
- Correct deadline and intent extraction rate.
- False escalation rate.
- User correction and override rate.
- Unauthorized action rate: target zero.
- Audio or transcript privacy incidents: target zero.

## 16. Intern-sized deliverable

The project should deliver one credible vertical slice, not the whole vision:

> **One multilingual communication source → structured commitments → confirmed follow-up → status tracking → completion verification → overdue escalation → human-attention briefing.**

The highest-value contribution is to identify the right internal workflow, design the context and permission model, dogfood Sarvam’s capabilities, measure before-and-after impact, and produce a prototype that Sarvam could credibly show to an enterprise customer.

## 17. Final product promise

> **Automate what is predictable. Translate intent across language and context. Escalate what is consequential. Protect human attention.**

