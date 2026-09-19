# Full Deck OS Development And Implementation Plan

This plan turns the Prime Directive, operating premise, and technical architecture into testable development phases. Each phase should produce something that can be demonstrated, evaluated, and either shipped as an MVP slice or used as the foundation for the next phase.

## Planning Doctrine

Full Deck OS should be built in vertical slices, not as one giant platform build.

Each phase should prove one complete loop:

1. The CEO expresses intent or needs visibility.
2. Dealer's Table turns that into an operating request.
3. Full Deck routes the request through cards, decisions, agents, Workers, or Frappe.
4. The system returns a useful widget, decision, risk, action, or deterministic process.
5. The result is recorded, testable, and visible.

The system should start small but preserve the final architecture:

- Space Agent becomes Dealer's Table, the agentic CEO interface.
- Full Deck owns orchestration, decisions, cards, widgets, risks, maturity, and priorities.
- Frappe/ERPNext owns durable commodity business records where appropriate.
- Cloudflare Workers become deterministic skills.
- Jev provides structured decision judgment.
- The CEO remains the human authority for liability-bearing decisions.

## Phase 0: Architecture Baseline And Repo Organization

Goal: make the project buildable, navigable, and ready for product development.

Deliverables:

- Confirm the forked Space Agent repo is the working Dealer's Table codebase.
- Keep architecture packets in the repo as first-class product specifications.
- Decide where Full Deck-specific modules live inside the fork.
- Decide how the empty `/Users/darren_dean/projects/full-deck-os` workspace should relate to the Space Agent fork and Cloudflare OS lab.
- Create an implementation backlog from the current architecture docs.
- Define local development commands for Dealer's Table, Cloudflare Workers, and Frappe/ERPNext integration experiments.

Testable outcome:

- A developer can clone or open the project and understand the system direction from the Markdown architecture packets.
- The local Dealer's Table app can still run after documentation and branding changes.

Potential MVP value:

- Internal planning MVP only.

## Phase 1: Dealer's Table Brand And Interface MVP

Goal: rebrand Space Agent into a believable Full Deck CEO command surface without deep runtime rewrites.

Deliverables:

- Replace visible Space Agent naming with Dealer's Table / Full Deck OS language.
- Remove or hide astronaut, helmet, starfield, Agent Zero public links, novelty demos, and upstream public URLs from launch-facing surfaces.
- Keep internal `space.*` runtime names initially to avoid risky broad renames.
- Create a first-run Dealer's Table starter layout.
- Add the five core starter widgets as mock or semi-live widgets:
  - Company Pulse
  - Decision Required
  - Risk Profile
  - Agent Activity
  - Dealt Priorities
- Add subtle card-table visual cues without turning the product into a game.

Testable outcome:

- A CEO can open the app and understand it as a business operating command table, not Space Agent.
- The table supports free-form widget placement and agent-built surfaces.
- The app can be demoed with mock business state.

Potential MVP value:

- Marketing/demo MVP.
- Useful for screenshots, investor/customer conversations, and product validation.

## Phase 2: Full Deck Core Data Model MVP

Goal: define the internal Full Deck operating model independent of any one business system.

Deliverables:

- Define core entities:
  - Company
  - Business Deck
  - Card
  - Face-card Actor
  - Number-card Work Package
  - Widget
  - Decision
  - Risk
  - Data Source
  - Evidence
  - Deterministic Skill
  - Integration
  - Build Priority
- Implement a local or D1-backed prototype schema.
- Add the one-business-one-deck rule.
- Add maturity states:
  - unknown
  - manually entered
  - agent researched
  - document extracted
  - system connected
  - validated
  - monitored
  - optimized
- Add priority labels:
  - `critical-now`
  - `foundation`
  - `quick-win`
  - `delegate`
  - `integrate`
  - `defer`

Testable outcome:

- The system can represent one company as one deck.
- The five starter widgets can read from the same core model.
- Missing information can become both a risk and an agent work item.

Potential MVP value:

- Operating model MVP.

## Phase 3: Dealer Request To Custom Widget Pipeline

Goal: prove that the CEO can ask the Dealer to create a custom widget.

Deliverables:

- Add a request flow where the CEO asks for a widget in natural language.
- Dealer interprets the requested view, metric, risk, workflow, or decision.
- System creates a widget definition with:
  - purpose
  - owner face card
  - needed data
  - data maturity
  - refresh method
  - missing-data risks
  - evidence links
  - display contract
- Widget appears on Dealer's Table.
- If data does not exist, widget displays uncertainty and creates a work item.

Testable outcome:

- CEO asks: "Show me overdue invoice risk."
- Dealer creates a widget placeholder.
- Widget identifies needed fields and missing integrations.
- The system routes the request to Finance/King or Jack of Diamonds.

Potential MVP value:

- First true Full Deck experience MVP.

## Phase 4: Jev Decision Layer MVP

Goal: prove structured decision-making over business state.

Deliverables:

- Create a Jev decision service wrapper.
- Define typed question templates for common Full Deck decisions:
  - owner routing
  - priority classification
  - risk urgency
  - CEO approval required
  - data sufficiency
  - automation readiness
  - widget confidence
- Store Jev results with:
  - input state pointer
  - question
  - response
  - probabilities
  - confidence
  - decision route
  - timestamp
  - human override, if any
- Add thresholds for automatic action, agent review, and CEO review.

Testable outcome:

- Given a sample business state, Jev can classify priority and owner.
- Low-confidence or high-liability outcomes route to human review.
- Decision history can be displayed in a widget.

Potential MVP value:

- Decision engine MVP.

## Phase 5: Cloudflare Worker Skill MVP

Goal: prove deterministic processes as callable Worker skills.

Deliverables:

- Create a Worker skill contract:
  - name
  - description
  - inputs
  - outputs
  - permissions
  - owner card
  - decision hooks
  - failure mode
  - audit trail
  - widget surface
- Implement first sample Worker skills:
  - refresh widget state
  - calculate risk score from stored inputs
  - ingest a webhook payload
  - call Jev decision wrapper
  - call mock Frappe/ERPNext endpoint
- Register Worker skills in Full Deck state.
- Expose skill results to Dealer's Table widgets.

Testable outcome:

- Dealer or face-card actor can call a deterministic skill.
- Skill execution is recorded.
- Widget updates from skill output.

Potential MVP value:

- Deterministic process MVP.

## Phase 6: Frappe/ERPNext Gateway MVP

Goal: prove Full Deck can orchestrate a real business system without owning its records.

Deliverables:

- Stand up or connect to a Frappe/ERPNext development instance.
- Define a Frappe gateway Worker.
- Map first ERPNext resources:
  - Customer
  - Invoice
  - Payment
  - Opportunity or Lead
- Implement read-only API calls first.
- Add source-of-truth rules:
  - Frappe owns business object records.
  - Full Deck owns widget state, decision context, risk scoring, evidence pointers, and escalation status.
- Create the first ERPNext-powered widget.

Testable outcome:

- Dealer's Table can show live or fixture-backed ERPNext invoice/customer state.
- Full Deck can identify missing data or risk without modifying ERPNext.

Potential MVP value:

- ERP orchestration MVP.

## Phase 7: First End-To-End Business Function

Goal: deliver one complete business function from CEO request to connected system action.

Recommended first function: overdue invoice risk and follow-up.

Deliverables:

- CEO asks for a receivables risk widget.
- Dealer creates the widget.
- Finance face card owns the widget.
- Worker reads invoices/customers from ERPNext.
- Jev scores collection risk and escalation priority.
- Full Deck records decisions, evidence, confidence, and risk.
- Dealer's Table shows:
  - total overdue exposure
  - highest-risk accounts
  - recommended actions
  - CEO approvals required
  - follow-up status
- Approved follow-up can trigger email or WhatsApp through a communication gateway.

Testable outcome:

- One business workflow is visible, decisioned, routed, and partly automated.
- CEO can approve or reject a recommended action.
- System records what happened and why.

Potential MVP value:

- First practical customer MVP.

## Phase 8: Data Maturity And Business Assessment

Goal: make the system useful even when the company has incomplete data.

Deliverables:

- Add a business assessment flow across the deck.
- Score each face-card actor and active work package by:
  - evidence
  - data maturity
  - owner
  - risk
  - process maturity
  - deterministic readiness
- Make missing data visible as risks and work items.
- Add maturity progress to Company Pulse.
- Add build sequencing to Dealt Priorities.

Testable outcome:

- A company can start with incomplete information.
- The system prioritizes next build steps instead of overwhelming the CEO.
- Dealer can show what is unknown, why it matters, and what to do next.

Potential MVP value:

- Business onboarding MVP.

## Phase 9: Agent Work Packages And Build Cadence

Goal: make face-card actors and number-card work packages operational.

Deliverables:

- Define face-card actor prompts/contracts.
- Define number-card work-package schema.
- Implement delegation rules:
  - face card processes directly when possible
  - number card is dealt for capacity, parallelism, timing, repetition, or temporary support
  - repeated patterns can graduate to Worker skills
- Add active build queue:
  - next 3 system-building cards
  - deferred gaps
  - blocked items
  - delegated requests
  - integration tasks

Testable outcome:

- Dealer can assign work to a face-card actor.
- Face card can create work packages.
- Work packages can complete, pause, defer, or become Worker-skill candidates.

Potential MVP value:

- Agentic operating cadence MVP.

## Phase 10: Communication Gateways

Goal: connect the operating system to business communication channels.

Deliverables:

- Cloudflare Email routing and sending pattern.
- Evolution API WhatsApp gateway pattern.
- Message ingestion into Full Deck evidence and decision state.
- Message classification through Jev where appropriate.
- Approval gates for outbound communications.
- Widget surfaces for communications risk, pending replies, and follow-up status.

Testable outcome:

- Inbound messages can create state, risks, decisions, or work items.
- Outbound communication can be drafted or triggered only through approved flows.

Potential MVP value:

- Communications MVP.

## Phase 11: Worker Skill Catalog And Deterministic Conversion

Goal: formalize the path from agentic work to deterministic Workers.

Deliverables:

- Skill registry in D1.
- Worker template for deterministic skills.
- Promotion workflow:
  - repeated work identified
  - inputs/outputs known
  - decisions isolated
  - edge cases listed
  - failure modes defined
  - audit trail defined
  - CEO or system owner approves conversion
- Dealer widget showing automation candidates.

Testable outcome:

- A repeated number-card work package can be proposed as a Worker skill.
- Skill can be created, registered, invoked, monitored, and improved.

Potential MVP value:

- Process maturity MVP.

## Phase 12: Multi-Function Operating System MVP

Goal: expand from one business function to a useful operating layer.

Deliverables:

- At least three connected business functions, such as:
  - receivables risk
  - sales pipeline risk
  - delivery/SOP maturity
- Shared decision history.
- Shared risk profile.
- Shared Company Pulse.
- Cross-function priorities.
- CEO decision queue.
- Basic audit trail.

Testable outcome:

- Dealer's Table can show a meaningful operating picture across money, relationships, operations, and risk.
- CEO can use Full Deck as a daily command surface.

Potential MVP value:

- True Full Deck OS MVP.

## Phase 13: Production Hardening

Goal: make the MVP safe enough for real company usage.

Deliverables:

- Authentication and authorization model.
- Tenant/company separation.
- Secret management.
- Integration permission scopes.
- Worker observability.
- Error handling and retries.
- Audit logging.
- Backup and recovery.
- Human approval enforcement.
- Security review of agent access to business systems.
- License review for integrated open-source systems.

Testable outcome:

- The system can run for a real pilot company without uncontrolled agent access or unclear data ownership.

Potential MVP value:

- Pilot-ready MVP.

## MVP Paths

There are several valid MVP stopping points:

### MVP A: Demo And Marketing MVP

Includes:

- Phase 1
- mocked widgets
- architecture docs
- screenshots
- no live integrations

Use when the goal is selling the vision.

### MVP B: Decision Engine MVP

Includes:

- Phase 1
- Phase 2
- Phase 3
- Phase 4

Use when the goal is proving that Dealer's Table can turn CEO intent into structured business decisions.

### MVP C: Deterministic Skill MVP

Includes:

- Phase 1
- Phase 2
- Phase 3
- Phase 4
- Phase 5

Use when the goal is proving that repeated work can become Worker skills.

### MVP D: ERP Orchestration MVP

Includes:

- Phase 1 through Phase 7

Use when the goal is proving Full Deck can orchestrate Frappe/ERPNext and deliver one real business function.

### MVP E: Pilot Company MVP

Includes:

- Phase 1 through Phase 13, scoped to a narrow set of business functions.

Use when the goal is running a real company pilot.

## Recommended Build Order

The recommended path is:

1. Phase 1: Dealer's Table brand and interface MVP.
2. Phase 2: Full Deck core model.
3. Phase 3: custom widget creation pipeline.
4. Phase 4: Jev decision layer.
5. Phase 5: Worker skill contract and first skills.
6. Phase 6: Frappe/ERPNext gateway.
7. Phase 7: overdue invoice risk as the first end-to-end business function.

That sequence reaches a practical MVP without trying to build the whole company operating system at once.

## First End-To-End Slice

The first serious vertical slice should be:

**CEO asks Dealer's Table for an overdue invoice risk widget.**

Why this is the right first slice:

- It uses a common ERPNext domain.
- It matters to the CEO.
- It has money, risk, relationship, operations, and decision implications.
- It can start with mock data and later connect to ERPNext.
- It requires Jev decisions but not huge open-ended reasoning.
- It can produce deterministic Worker skills.
- It can demonstrate human approval before outbound action.

The slice should prove:

- CEO intent
- Dealer widget generation
- Frappe/ERPNext data access
- Jev risk scoring
- D1 decision/risk state
- Cloudflare Worker skill execution
- Dealer's Table display
- CEO approval
- audit trail

## Near-Term Backlog

Immediate next development tasks:

1. Decide local workspace layout for Space Agent, Cloudflare OS lab, and Full Deck-specific Worker packages.
2. Run the Space Agent fork locally and identify the first visible brand surfaces to change.
3. Define the first D1 schema for Full Deck core state.
4. Define the widget definition contract.
5. Define the Worker skill contract.
6. Define Jev question templates for priority, ownership, risk, and CEO approval.
7. Decide whether to use mock ERPNext fixtures before standing up a live ERPNext instance.
8. Build the first Dealer's Table starter widget from static/mock state.
9. Build the overdue invoice risk vertical slice.

## Non-Goals For Early Phases

Avoid these early:

- broad codebase renames from `space` to `deck`
- building a native ERP
- replacing ERPNext modules
- building every card actor at once
- connecting every communication channel
- automating outbound actions without approval gates
- trying to solve every business maturity gap in the first build

The goal is to prove the operating loop, then widen it carefully.
