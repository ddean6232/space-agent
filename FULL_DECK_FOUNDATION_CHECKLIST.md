# Full Deck OS Minimum Viable Foundation Checklist

This checklist defines the minimum foundation that should be in place before product code changes begin. It is the readiness gate for implementation.

The purpose is to prevent the project from starting UI, agent, or integration work before the required operating substrate exists.

## Foundation Rule

Do not begin product implementation until the foundation is clear enough to support the first vertical slice.

Foundation complete means:

- Dealer's Table can run locally.
- The canonical project layout is decided.
- The Cloudflare account for Full Deck infrastructure is selected.
- ERPNext/Frappe is available as the foundational business application substrate.
- Full Deck's own state, storage, and skill runtime strategy is defined.
- Jev access is available or has a clear setup path.
- Secrets and credentials have a safe handling plan.
- The first vertical slice is agreed.

## 1. Canonical Project Layout

Decide where the system actually lives locally and in GitHub.

Required:

- Space Agent fork is confirmed as the Dealer's Table codebase.
- Cloudflare OS lab is treated as reference/runtime research unless deliberately adopted.
- `/Users/darren_dean/projects/full-deck-os` is assigned a clear role: parent workspace, future monorepo, documentation hub, or unused placeholder.
- The relationship between Space Agent, Full Deck Worker packages, Frappe integration code, and Cloudflare OS lab is documented.
- GitHub fork and branch strategy is documented.

Readiness test:

- A developer can identify which repo to edit for Dealer's Table, Worker skills, Frappe gateway work, and architecture docs.

## 2. Cloudflare Account Decision

Choose the Cloudflare account that owns Full Deck infrastructure.

Required:

- Cloudflare account name and account ID selected.
- Wrangler is configured to use the selected account without interactive ambiguity.
- Token permissions confirmed for the needed services:
  - Workers
  - D1
  - R2
  - Queues
  - Workflows
  - AI / Workers AI / AI Gateway as needed
  - Email routing/sending
  - secrets
- Naming convention for Full Deck resources is selected.
- Dev/staging/prod resource separation is defined.

Readiness test:

- A non-interactive Wrangler command can list or create resources for the selected Full Deck account.

## 3. ERPNext/Frappe Foundation

ERPNext/Frappe must exist before serious orchestration work starts.

Required:

- Development ERPNext/Frappe instance exists.
- Access method is selected:
  - local Docker
  - hosted Frappe/ERPNext
  - cloud VM
  - other managed instance
- API access method is confirmed.
- Admin/API credentials are stored securely.
- First company is configured.
- Basic modules are available:
  - customers
  - invoices
  - payments
  - leads/opportunities
- Frappe/ERPNext source-of-truth boundaries are documented.

Readiness test:

- A simple API request can read at least one ERPNext/Frappe business object from the development instance.

## 4. Full Deck Core Data Store

Full Deck needs its own state separate from ERPNext/Frappe records.

Required:

- D1 database strategy is selected.
- Initial schema plan exists for:
  - companies
  - cards
  - widgets
  - decisions
  - risks
  - skills
  - integrations
  - evidence
  - audit records
- Migration approach is selected.
- Local/dev/prod separation is defined.
- Source-of-truth rules are clear:
  - Frappe owns commodity business records.
  - Full Deck owns orchestration, decision context, risks, widgets, skills, and evidence pointers.

Readiness test:

- A minimal schema can be applied locally or to a development D1 database.

## 5. Object And Evidence Storage

Full Deck needs durable storage for documents, SOPs, uploads, evidence bundles, generated reports, screenshots, and artifacts.

Required:

- R2 bucket strategy is selected.
- Bucket naming convention is selected.
- Access policy is defined.
- Evidence pointer pattern between D1 and R2 is defined.
- Retention expectations are documented.

Readiness test:

- A development Worker can write a test artifact and store a pointer to it in Full Deck state.

## 6. Deterministic Skill Runtime

Cloudflare Workers are the deterministic skill layer.

Required:

- Worker project/package location is selected.
- Worker skill contract is defined.
- Local development command is known.
- Deployment command is known.
- Environment and secrets strategy is defined.
- Logging and audit strategy is defined.
- First skill target is selected.

Readiness test:

- A sample Worker skill can run locally and return structured output.

## 7. Async And Long-Running Work

Some Full Deck work cannot happen inside a single request.

Required:

- Queue strategy is selected for async jobs.
- Workflow strategy is selected for durable multi-step processes.
- Cron strategy is selected for repeated checks.
- Retry and failure policy is documented.
- Dead-letter or failure review pattern is defined.

Readiness test:

- A sample async job can be enqueued, processed, and recorded.

## 8. Jev Decision Layer

Jev must be available as the structured decision model.

Required:

- TypeSafe.AI account/API key is available or setup path is clear.
- SDK/API approach is selected.
- First decision wrapper design is defined.
- Initial question templates are defined for:
  - priority
  - owner/card routing
  - risk urgency
  - CEO approval required
  - data sufficiency
  - automation readiness
- Confidence thresholds are defined for:
  - automatic action
  - agent review
  - CEO review

Readiness test:

- A sample Jev request can return a typed result and confidence against test state.

## 9. Dealer's Table Baseline

The Space Agent fork must run cleanly before it is branded or modified.

Required:

- Local install works.
- Dev server command is known.
- Build command is known.
- First-run flow is understood.
- Widget/spaces architecture is understood enough to modify safely.
- Existing test or smoke-test path is known.

Readiness test:

- Dealer's Table baseline can be started locally and viewed before product modifications begin.

## 10. Integration Gateway Pattern

External systems should be called through controlled gateways, not raw agent access.

Required:

- Frappe gateway pattern is defined.
- Communication gateway pattern is defined.
- Permission-scope model is defined.
- Worker-mediated calls are required for system actions.
- Agents do not receive raw ERP/API credentials.
- Audit records are created for meaningful actions.

Readiness test:

- A sample gateway call can be described end-to-end from Dealer request to Worker to external system and back.

## 11. Secrets And Environment Management

No implementation should begin without a secrets strategy.

Required:

- Local `.dev.vars` or equivalent strategy is selected.
- Cloudflare secrets plan is selected.
- ERPNext credentials plan is selected.
- TypeSafe/Jev key plan is selected.
- Evolution API key plan is reserved for the communications phase.
- No secrets are committed to the repo.
- Rotation/revocation expectations are documented.

Readiness test:

- Required development secrets can be loaded locally without committing them.

## 12. First Vertical Slice Agreement

Agree on the first slice before changing product code.

Recommended first slice:

**Overdue invoice risk widget**

Expected architecture:

- ERPNext/Frappe supplies invoice and customer data.
- Cloudflare Worker fetches and normalizes the data.
- Jev scores risk and priority.
- D1 stores decision and risk state.
- R2 can store evidence bundles if needed.
- Dealer's Table displays the widget.
- CEO approves any outbound follow-up.

Readiness test:

- The team agrees this is the first serious vertical slice, or replaces it with an equally narrow slice.

## 13. MVP Boundary

Define what "foundation complete" means.

Foundation is complete when:

- ERPNext/Frappe development instance exists.
- Cloudflare account is selected and non-interactive Wrangler use works.
- D1/R2/Workers/Queues/Workflows strategy is defined.
- Jev access is available or setup path is explicit.
- Dealer's Table runs locally.
- First vertical slice is selected.
- Secrets strategy is in place.
- No product code changes are required to prove foundation readiness except documentation or configuration scaffolding.

## Foundation Decision Log

Record decisions here as they are made:

| Area | Decision | Date | Notes |
| --- | --- | --- | --- |
| Canonical repo/workspace | TBD | TBD | Decide role of `/Users/darren_dean/projects/full-deck-os`. |
| Cloudflare account | TBD | TBD | Select one account ID for Full Deck resources. |
| ERPNext/Frappe runtime | TBD | TBD | Local Docker, hosted, VM, or managed. |
| Full Deck D1 database | TBD | TBD | Name and environment plan. |
| R2 bucket strategy | TBD | TBD | Name and access policy. |
| Worker package location | TBD | TBD | Inside Space Agent fork, separate package, or future monorepo. |
| Jev access | TBD | TBD | TypeSafe account/API key. |
| First vertical slice | Overdue invoice risk widget | Proposed | Confirm or replace. |

## Summary

The minimum viable foundation is:

Dealer's Table running, Cloudflare account selected, ERPNext/Frappe available, Full Deck state/storage planned, Jev available, Worker skill runtime defined, secrets strategy set, and the first vertical slice agreed.
