# Human Attention OS — Technical Build Specification

## 1. Objective

Build a working, local-first prototype that accepts multilingual communication, extracts commitments, routes attention, proposes or executes bounded actions, and shows a trustworthy action history.

The first implementation must demonstrate the complete vertical slice:

```text
Voice / text input
→ Sarvam processing
→ structured commitment
→ context and policy evaluation
→ human-attention routing
→ approved follow-up
→ task state tracking
→ exception briefing
```

## 2. Prototype boundary

### In scope

- Synthetic Sarvam-style organization data.
- Optional personal files and voice recordings.
- Text and voice input.
- English, Hindi, and Hinglish examples.
- Commitment extraction.
- Owner and deadline resolution.
- Confidence and risk classification.
- Human approval flow.
- Mock email, Slack, calendar, and task connectors.
- Action state machine.
- Audit history.
- Exception inbox.

### Out of scope

- Sarvam internal system access.
- Unrestricted mailbox or Slack monitoring.
- Autonomous external communication.
- Production-grade multi-tenant deployment.
- Sensitive HR, finance, legal, or customer workflows.
- Training or fine-tuning a foundation model.

## 3. Recommended stack

### Frontend

- Next.js with TypeScript.
- Tailwind CSS.
- Server-sent events for action status updates.
- Browser microphone capture for voice input.

### Backend

- Python with FastAPI.
- Pydantic models for all API contracts.
- SQLAlchemy for persistence.
- Background workers for extraction and workflow execution.

### Storage

- PostgreSQL as the primary database.
- Object storage abstraction for audio and source files.
- Append-only event table for operational history.
- Local filesystem adapter for development.

### Runtime

- Docker Compose for local development.
- Environment-based configuration.
- Structured JSON logging.
- OpenTelemetry-compatible trace IDs.

### External services

- Sarvam APIs through one internal language-runtime module.
- Mock connectors for email, Slack, calendar, and task systems.
- Real connectors only after the read-only workflow is stable.

## 4. Repository layout

```text
human-attention-os/
├── apps/
│   ├── web/                  # Next.js interface
│   └── api/                  # FastAPI application
├── packages/
│   ├── contracts/            # Shared API and event schemas
│   ├── policy-engine/        # Risk and authorization rules
│   └── connector-contract/   # Connector interfaces
├── services/
│   ├── language-runtime/     # Sarvam API abstraction
│   ├── semantic-runtime/     # Intent and commitment extraction
│   ├── workflow-runtime/     # Durable action execution
│   └── context-runtime/      # People, projects, permissions
├── data/
│   ├── fixtures/             # Synthetic organization data
│   ├── eval/                 # Labeled evaluation examples
│   └── samples/              # Safe demo audio and text
├── infra/
│   ├── docker-compose.yml
│   └── migrations/
├── docs/
├── .env.example
└── README.md
```

## 5. Runtime flow

### Input

1. User submits text, audio, transcript, or fixture data.
2. API authenticates the user and assigns a trace ID.
3. Input is stored as an immutable source event.
4. The semantic job is queued.

### Understanding

1. Audio is sent to Sarvam speech processing.
2. Language and code-mix metadata are retained.
3. The semantic runtime extracts entities, intent, commitments, owners, deadlines, and uncertainty.
4. Each field keeps provenance and confidence.

### Routing

1. Context runtime resolves people, teams, projects, and policies.
2. Policy engine calculates risk and permitted autonomy.
3. Attention Firewall routes the item to automatic execution, confirmation, clarification, delegation, or the exception inbox.

### Execution

1. Approved proposals become commands.
2. Commands are validated against policy and connector capability.
3. Workflow runtime executes them with idempotency and retries.
4. Connector results become events.
5. The action graph updates from events.

### Follow-through

1. Timers schedule reminders and status requests.
2. External evidence is reconciled.
3. Completed work is closed.
4. Blocked or overdue work is escalated.
5. The user receives a concise text or voice briefing.

## 6. Initial database tables

- `users`
- `teams`
- `projects`
- `roles`
- `policies`
- `preferences`
- `source_connections`
- `source_events`
- `semantic_proposals`
- `commitments`
- `actions`
- `action_dependencies`
- `approvals`
- `execution_commands`
- `execution_results`
- `evidence`
- `attention_items`
- `learning_records`
- `audit_events`

Every business object should include `workspace_id`, timestamps, and provenance references.

## 7. First API endpoints

```text
POST /v1/inputs
GET  /v1/inputs/{input_id}
GET  /v1/proposals
POST /v1/proposals/{proposal_id}/decision
GET  /v1/attention
GET  /v1/actions
GET  /v1/actions/{action_id}
POST /v1/voice/commands
GET  /v1/briefings/daily
GET  /v1/audit/{object_id}
```

No endpoint may directly invoke an external side effect from an unapproved model response.

## 8. Connector contract

```python
class Connector(Protocol):
    def capabilities(self) -> list[str]: ...
    def validate(self, command: Command) -> ValidationResult: ...
    def execute(self, command: Command, idempotency_key: str) -> ExecutionResult: ...
    def observe(self, external_id: str) -> ExternalState: ...
    def reconcile(self, object_id: str) -> ReconciliationResult: ...
```

The first implementation uses deterministic mock connectors with realistic latency, failures, duplicate events, and permission errors so the workflow engine is tested against real operational conditions.

## 9. Policy tiers

```text
LOW
  Internal, reversible, high-confidence, pre-authorized.

MEDIUM
  Shared project state, inferred deadline, manager escalation, or uncertain context.

HIGH
  External recipient, sensitive information, financial/legal/HR impact, or irreversible action.
```

Routing defaults:

- Low: automatic if the user has opted in.
- Medium: confirmation required.
- High: explicit human approval required.

## 10. Build order

### Milestone 1 — Foundation

- Repository structure.
- Environment configuration.
- Database schema and migrations.
- Event envelope and audit events.
- Synthetic fixtures.
- Basic web shell and API health endpoint.

### Milestone 2 — Semantic pipeline

- Input upload and text submission.
- Sarvam language-runtime adapter.
- Mock language-runtime adapter for tests.
- Commitment extraction schema.
- Proposal review screen.
- Provenance display.

### Milestone 3 — Context and routing

- Synthetic people, teams, projects, and policies.
- Entity resolution.
- Attention Firewall.
- Risk classification.
- Exception inbox.

### Milestone 4 — Confirmed execution

- Mock messaging connector.
- Mock task connector.
- Approval flow.
- Idempotent commands.
- Retry and failure states.
- Action timeline.

### Milestone 5 — Follow-through

- Durable reminders.
- Status requests.
- Evidence records.
- Completion verification.
- Overdue escalation.
- Daily briefing.

### Milestone 6 — Voice and learning

- Voice command input.
- Spoken briefing output.
- Explicit preference capture.
- Correction feedback.
- Safe inferred-preference suggestions.

## 11. Quality gates

The prototype cannot progress to the next autonomy stage unless it passes:

- No unauthorized command execution.
- Deterministic policy tests.
- Idempotency tests.
- Connector failure and retry tests.
- Provenance completeness tests.
- Permission-boundary tests.
- Labeled semantic evaluation.
- User correction flow.
- Safe handling of ambiguous ownership and deadlines.

## 12. Definition of done for the first demo

A user can submit a realistic multilingual voice or text instruction, and the system can:

1. Show the source and interpreted meaning.
2. Extract a commitment with owner and deadline.
3. Explain confidence and uncertainty.
4. Apply a policy decision.
5. Ask for confirmation when needed.
6. Execute a mock internal follow-up.
7. Create a mock task.
8. Track status and completion evidence.
9. Escalate a simulated overdue action.
10. Show a final human-attention briefing.

The demo must include at least one failure case and one case where the system correctly refuses to act without human approval.

