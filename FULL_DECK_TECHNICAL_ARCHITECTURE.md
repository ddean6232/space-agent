# Full Deck OS Technical Architecture

This document defines the working technical architecture for Full Deck OS. It assumes Full Deck OS is an orchestration and decision operating layer, not a monolithic ERP suite.

## Core Doctrine

Full Deck OS should orchestrate the best-fit business systems rather than rebuild every business function directly.

The product should own:

- the Prime Directive
- the Dealer's Table
- the one-business-deck model
- face-card actors and number-card work packages
- decision orchestration
- widget generation
- data maturity and risk visibility
- agent coordination
- deterministic Worker skills
- business-system prioritization and escalation

Commodity business functions should normally be provided by mature open-source or API-backed systems. Full Deck should wrap, observe, score, and orchestrate those systems through well-defined skills.

## Recommended Business Application Substrate

The preferred business application substrate is Frappe/ERPNext.

ERPNext provides mature business modules such as accounting, CRM, HR, manufacturing, order management, and asset management. Frappe provides the underlying framework: DocTypes, permissions, forms, APIs, hooks, background jobs, and application extension points.

The strategic fit:

- Frappe's DocType model maps well to structured business objects.
- ERPNext reduces the need to rebuild commodity ERP functions.
- Frappe's REST/RPC APIs give Full Deck a clean integration path.
- Frappe apps can hold operational business records while Full Deck holds decision context, orchestration state, and CEO-facing widgets.
- Frappe can be customized for company-specific business objects without forcing all customization into Full Deck itself.

## Full Deck Architecture Versus Frappe Architecture

The central boundary question is: what becomes Frappe architecture and what becomes Full Deck architecture?

### Frappe/ERPNext Should Own

Frappe/ERPNext should own durable business application records and workflows when the function is a mature, common business domain.

Examples:

- customers
- suppliers
- contacts
- leads and opportunities
- quotations
- sales orders
- purchase orders
- invoices
- payments
- accounting ledgers
- inventory
- assets
- HR records
- projects
- support tickets
- standard ERP reports
- company-specific DocTypes that behave like ordinary business records

Frappe should also own business application UI when users need a full operational module rather than a CEO-facing widget.

### Full Deck Should Own

Full Deck should own orchestration, judgment, visibility, and system-building logic.

Examples:

- Prime Directive execution
- Dealer's Table
- CEO-requested custom widgets
- one-business-deck model
- face-card ownership
- number-card work-package delegation
- Jev decision questions
- prioritization and build sequencing
- business maturity scoring
- missing-data risk
- cross-system operating state
- agent assignments
- escalation rules
- decision history
- deterministic Worker skill catalog
- conversion of repeated agent work into Cloudflare Workers

Full Deck should not become a clone of ERPNext. It should become the command and orchestration layer above ERPNext and other best-fit systems.

## Cloudflare As Deterministic Skill Layer

Cloudflare Workers are the deterministic skill layer of Full Deck OS.

In agentic terms, a Worker is a mature callable skill. It receives structured input, performs a bounded deterministic function, and returns structured output or updates state.

Examples:

- refresh a Dealer's Table widget
- ingest an email
- process a WhatsApp webhook
- classify an incoming request
- call ERPNext to create an invoice
- retrieve open receivables
- update a risk score
- enqueue document extraction
- sync a CRM record
- trigger a Frappe workflow
- call Jev for a typed decision
- route a task to a face-card actor

The maturity path should be:

1. A face-card actor handles ambiguous work.
2. Number-card work packages support capacity, timing, repetition, or parallelism.
3. The system learns the inputs, outputs, permissions, data sources, and edge cases.
4. The process becomes a Cloudflare Worker skill.
5. Agents monitor exceptions, improve the process, and escalate decisions.

## Cloudflare Infrastructure Map

Recommended Cloudflare responsibilities:

- Workers: deterministic skills, APIs, webhooks, widget refreshers, integration adapters.
- Durable Objects: live Dealer's Table sessions, collaborative widget state, agent coordination state, long-lived interaction state.
- D1: structured Full Deck state, decisions, risks, cards, widgets, job definitions, audit records, skill registry, integration mappings.
- R2: documents, SOPs, generated reports, uploaded files, screenshots, artifacts, large evidence bundles.
- Vectorize: semantic retrieval over SOPs, documents, prior decisions, business knowledge, and evidence.
- Queues: async work such as extraction, sync jobs, webhook processing, research tasks, and retryable integrations.
- Workflows: durable multi-step processes that may run across minutes, hours, or days.
- Cron Triggers: scheduled deterministic checks and recurring business tasks.
- Email Routing/Email Workers: inbound and outbound email processing where appropriate.

## Jev Decision Layer

Jev is the structured decision layer, not a general chat layer.

Jev evaluates typed questions against state and returns structured answers such as choices, scores, yes/no probabilities, probability distributions, and confidence. Full Deck code should use those results to route work, prioritize actions, and decide when a human must review.

Jev should be used for narrow decision primitives:

- Choice: choose an owner, next action, route, priority, card, skill, or workflow.
- Score: score maturity, risk, urgency, business value, evidence quality, readiness, or confidence.
- Noul: answer yes/no likelihood questions such as whether CEO approval is required or whether a workflow is ready for automation.

Complex business judgment should be decomposed into atomic typed questions and recomposed in Full Deck code. The weighting, thresholds, and routing logic should remain explicit and auditable.

## Decision-First Business Operations

Most of business can be modeled as making decisions with information and data.

Full Deck should therefore treat every operating function as a decision loop:

1. Observe business state from Frappe, ERPNext, communications, documents, APIs, human input, and prior decisions.
2. Structure the state into D1, R2, Vectorize, and integration-specific mappings.
3. Ask typed Jev questions where judgment is needed.
4. Route the outcome through code to a Worker skill, Frappe action, agent, number-card work package, or CEO decision.
5. Act through deterministic Workers or connected systems.
6. Record the decision, confidence, evidence, owner, timestamp, and outcome.
7. Mature repeated actions into Workers and reduce future agent burden.

## Integration Pattern With Frappe/ERPNext

Full Deck should integrate with Frappe through a controlled gateway rather than letting agents call ERPNext freely.

Recommended pattern:

1. A Dealer/Table request or scheduled Worker needs business data or action.
2. Full Deck resolves the relevant face card, business function, and permission scope.
3. A Cloudflare Worker skill calls a Frappe gateway.
4. The gateway uses Frappe REST/RPC APIs or a dedicated Frappe app endpoint.
5. Frappe remains the system of record for the business object.
6. Full Deck stores the decision context, evidence pointer, confidence, and widget state.

Example:

- CEO asks for an overdue invoice risk widget.
- Dealer creates a widget definition.
- Finance face card owns the widget.
- Worker skill calls ERPNext for invoices and customers.
- Jev scores collection risk and escalation priority.
- D1 stores widget state, risk records, decision recommendations, and evidence pointers.
- Dealer's Table shows the CEO what needs attention.
- If follow-up is deterministic, a Worker triggers email or WhatsApp through the approved communication gateway.

## Frappe App Versus Full Deck Worker

Use a Frappe app when:

- the feature is a durable business application record
- users need rich operational screens inside ERPNext/Frappe
- the feature belongs close to ERPNext permissions, workflows, or DocTypes
- the data should live primarily in MariaDB/Postgres behind Frappe
- the function extends ERPNext's normal business modules

Use a Full Deck Cloudflare Worker when:

- the task is a bounded deterministic skill
- the process crosses multiple systems
- the task powers a Dealer's Table widget
- the task is event-driven or webhook-driven
- the task needs Cloudflare-native scale, scheduling, queues, or edge execution
- the process is a mature version of repeated agent work
- the action should remain part of Full Deck's orchestration layer

Use Jev when:

- the system needs structured judgment
- a typed decision can route work
- confidence should determine automation versus human review
- the decision can be decomposed into atomic choices, scores, or yes/no probabilities

Use a human CEO decision when:

- liability must be accepted
- confidence is too low
- the decision changes strategy, money, reputation, legal exposure, or high-stakes customer relationships
- the system lacks enough evidence to act safely

## Open-Source Component Evaluation Rule

For each business function, Full Deck should evaluate best-fit open-source or API-backed systems before building native functionality.

Questions:

1. Is this function core to Full Deck's identity, or a commodity business function?
2. Does Frappe/ERPNext already solve it well enough?
3. Does another open-source system solve it better for the target business?
4. Does the system expose a stable API?
5. Can a Cloudflare Worker safely wrap the function as a skill?
6. Who should be the source of truth: Full Deck, Frappe, or the external system?
7. What decisions does this function create?
8. What data must Full Deck mirror for widgets, risks, and prioritization?
9. What is the failure mode if the external system is down?
10. Is the license compatible with Full Deck's deployment model?
11. Does the system support multi-company, multi-tenant, or client-separated use?
12. What would make us replace it later?

The default answer should be integration first, native build second.

## Initial Technology Roles

| Layer | Preferred Technology | Role |
| --- | --- | --- |
| CEO workspace | Dealer's Table / Space Agent fork | Front-facing command table and widget surface |
| Business application substrate | Frappe/ERPNext | Commodity ERP/CRM/business records and operational modules |
| Deterministic skills | Cloudflare Workers | Mature business processes and integration actions |
| Long-running processes | Cloudflare Workflows | Durable multi-step business processes |
| Live state | Durable Objects | Sessions, collaboration, agent coordination, widget state |
| Structured orchestration state | D1 | Full Deck cards, widgets, decisions, risks, jobs, audit records |
| Documents/artifacts | R2 | Files, SOPs, generated outputs, evidence bundles |
| Semantic memory | Vectorize | Retrieval over business knowledge and evidence |
| Async processing | Queues | Ingestion, sync, extraction, retryable work |
| Decision model | TypeSafe Jev | Typed choices, scores, nouls, confidence |
| Communications | Cloudflare Email, Evolution API, other gateways | Email, WhatsApp, and later channel integrations |

## Architecture Summary

Full Deck OS should orchestrate the business.

Frappe/ERPNext should hold mature business records and commodity operational modules.

Cloudflare Workers should become deterministic skills.

Jev should make structured decisions over business state.

Agents should build, inspect, improve, and handle exceptions until the work matures into deterministic processes.

The CEO should see the result through Dealer's Table: decisions, risks, widgets, priorities, and the operating state of the company.

## References

- Frappe Framework architecture: https://docs.frappe.io/framework/user/en/basics/architecture
- Frappe REST/RPC API: https://docs.frappe.io/framework/user/en/guides/integration/rest_api
- Frappe DocType model: https://docs.frappe.io/framework/user/en/basics
- Frappe hooks: https://docs.frappe.io/framework/user/en/python-api/hooks
- Frappe background jobs: https://docs.frappe.io/framework/user/en/api/background_jobs
- ERPNext modules: https://docs.erpnext.com/index
- TypeSafe.AI introduction: https://docs.typesafe.ai/introduction
