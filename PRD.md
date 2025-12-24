# PRD: Ironclad Priority Dashboard ("IronQueue")

## 1. Problem Statement
Non-lawyer admins (Sales) lack visibility into the Legal queue, especially during end-of-quarter spikes. Legal teams are overwhelmed and lack a data-driven way to prioritize deals based on both "effort" (redline density) and "value" (strategic importance).

## 2. Goals
- Provide transparency to Sales on where their deals sit in the queue.
- Automate "effort" estimation by counting redlines via Ironclad API.
- Enable Sales to "pitch" for priority by providing structured metadata.
- Provide Legal Managers with a suggested priority list with manual override capability.

## 3. Functional Requirements
### 3.1. Dashboard View
- List of active Ironclad workflows.
- Display "Difficulty Score" (calculated from redlines).
- Display "Priority Score" (calculated from Sales metadata).
- Display current queue position.
- **Real-time Status Alerts:** Visual indicators showing if a deal is currently "Blocked by Legal" vs. "Waiting on Sales/Counterparty".

### 3.2. Priority Metadata (Sales Input)
- Fields: Deal Size ($), Strategic Value (High/Med/Low), Target Close Date.
- Logic: Updates the "Priority Score" in the local database.
- Action: Post a summary of this metadata as an attachment/comment back to the Ironclad workflow.

### 3.3. Difficulty Scoring (Automated)
- Integration: Fetch document versions from Ironclad.
- Metric: Count additions/deletions/comments (redlines) to determine a numerical difficulty score.

### 3.4. Prioritization Engine
- Algorithm: A weighted formula: `(Value + Strategic Weight) / Difficulty`.
- Override: Legal Managers can manually move a deal to the top or bottom, which flags it as "Manually Prioritized."

## 4. Technical Constraints
- **Backend:** Python (managed by `uv`).
- **Database:** Local SQL database (SQLite/PostgreSQL) for metadata and override states.
- **API:** Ironclad API for workflow and document retrieval.
- **Principles:** TigerStyle (Deterministic scoring), No Magic (explicit manual overrides).

## 5. Out of Scope for V1
- Automatic writing to Ironclad custom fields (only attachments/comments).
- User authentication (initially internal-only/trusted network).
