# Full Deck OS Customization Decisions

This document scrutinizes the Space Agent fork as a foundation for Full Deck OS. It separates what should remain, what should be changed, and what should be removed for an ultimate Full Deck customization.

Note: earlier notes use `Full Deck OS`; if the intended name is `Full Desk OS`, the same decisions apply, but every product string should use one final spelling consistently before implementation.

## Strategic Fit

Space Agent fits Full Deck OS best as an agentic business architecture runtime, not as a branded public product to preserve. The strong fit is architectural:

- browser-first agent runtime
- modular app surfaces delivered through `/mod/...`
- layered `L0` firmware, `L1` group customware, and `L2` user customware
- spaces/widgets as user-buildable work canvases
- local and hosted operation through Node server plus Electron desktop packaging
- agent-readable docs and skills through `AGENTS.md` and `SKILL.md`
- user/group persistence, local history, rollback, and admin recovery surfaces

The weak fit is the product wrapper:

- "Space Agent" name
- space/astronaut metaphor
- Agent Zero ecosystem links
- generic demo spaces
- playful first-run tone
- public domain and release pipeline tied to `space-agent.ai` and `agent0ai/space-agent`

## Prime Directive

Full Deck OS exists to help a business owner or CEO turn a principle, intention, opportunity, constraint, or desired outcome into a fully functioning business operating system.

The system should not merely answer questions, make recommendations, or display information. Its job is to guide the business from wherever it currently is, including nothing more than an idea, into a mature, process-oriented company with clear roles, accountable agents, reliable data, measured risks, repeatable workflows, and deterministic operating processes wherever deterministic processing is possible.

The CEO begins by stating what they want the business to become, what they believe, what they are trying to accomplish, or what problem they want the business to solve. Full Deck OS interprets that intent through the full operating deck: relationships, money, operations, and risk. The face cards act as the primary business actors. They assess what exists, identify what is missing, expose risks, determine what decisions are required, and guide the CEO through the sequence of building the business architecture.

The system must be sensitive to the current maturity of the company. A business with no SOPs, no clean data, and no connected systems should not be treated like a mature company with structured operations and validated reporting. Full Deck OS should recognize the difference between unknown, manual, partially documented, agent-researched, system-connected, validated, monitored, and optimized business functions. Missing data is not merely an inconvenience; it becomes a risk, a work item, and a priority decision.

The face cards should do as much work as they can directly. When the work is too large, too specialized, too time-sensitive, too repetitive, or better handled in parallel, the face cards may deal number-card work packages. Those number cards are not separate departments or permanent actors. They are temporary or active capacity assigned to help the face cards move work forward through execution, research, collection, analysis, documentation, follow-up, or repeated cadence.

The long-term direction is not to keep everything agentic forever. Full Deck OS should continuously look for work that can be made deterministic. Once a workflow becomes understood, stable, validated, and repeatable, it should be converted into a system job, automation, integration, checklist, policy, SOP, or other deterministic process. Agents should then move upward in the stack: supervising exceptions, monitoring outcomes, improving processes, escalating risk, and guiding decisions instead of repeatedly performing work the system can now handle predictably.

The CEO should not be overwhelmed by the whole business all at once. Full Deck OS must prioritize. It should decide what needs attention now, what is foundational, what is a quick win, what can be delegated, what should be integrated, and what should wait. The system's responsibility is to sequence the buildout of the business operating system in a way that respects the CEO's available attention, the business's maturity, the urgency of risks, and the practical availability of data and resources.

The Dealer's Table is the command surface where this guidance becomes visible. It should show the CEO the current state of the business, the active decisions, the highest risks, the work being handled by agents, the missing data, and the next priorities. It is not merely a dashboard. It is the workspace where the CEO participates in the business, approves direction, accepts human liability, and interacts with the agent-run operating architecture.

In its mature form, Full Deck OS should become the commander and operating architecture of the business. The CEO remains the human owner, authority, contact point, and liability holder, but the business itself is increasingly run through structured agents, deterministic processes, validated data, escalation rules, and continuous improvement loops.

## Product Role In Full Deck OS

Recommended role: `Full Deck OS` should be the operating layer. The forked Space Agent runtime becomes the execution substrate inside it.

Recommended terminology:

- `spaces` become `workspaces`, `boards`, or `decks`
- `widgets` become `tools`, `cards`, `blocks`, or `panels`
- `customware` becomes `business architecture layer`, `operating layer`, or `system layer`
- `agent` becomes `architect`, `operator`, or `agentic workspace assistant`
- `admin mode` becomes `Control Room`, `System Admin`, or `Recovery Console`

The underlying code can keep internal names such as `space.current` and `space.spaces` during the first phase to reduce risk. Public UI and docs should stop exposing the space metaphor.

## Keep

These should remain because they are core to the Full Deck OS concept.

- Browser-first runtime: keep as the main differentiator. Full Deck OS should let the agent build and alter live business workspaces.
- Layered `L0/L1/L2` model: keep. This maps well to firmware, business/team templates, and user-specific customization.
- Spaces/widgets engine: keep the runtime, but re-language and redesign it. It is the strongest fit for modular business systems.
- User/group sharing model: keep. It supports business teams and client/workspace separation.
- Admin/recovery mode: keep, but rename and restyle. This is valuable for a serious OS-like product.
- Time travel/local history: keep and feature more prominently. Rollback is a business safety story.
- Desktop packaging: keep. A branded Full Deck OS desktop app is useful for launch and demos.
- `AGENTS.md`/`SKILL.md` architecture: keep. It is aligned with agentic business architecture and maintainable automation.
- Browser-control/runtime APIs: keep. These can power research, workflow automation, client dashboards, and operational tools.
- Self-hosting path: keep. This can matter for privacy-conscious clients and agency/internal deployments.

## Change

These should be modified, not removed.

| Area | Current State | Decision | Rationale |
| --- | --- | --- | --- |
| Product name | Space Agent | Change to final Full Deck/Full Desk OS name | The current name fights the business architecture positioning. |
| Visual identity | Astronaut, helmet, starfield | Replace with Full Deck system mark and architecture/control visuals | The current visuals feel toy-like and space-themed. |
| Public shells | `/login`, `/enter`, `/admin`, `/share_space` use Space Agent metadata | Rewrite and restyle | These are first-impression launch surfaces. |
| App copy | Browser-first AI runtime and spaces language | Reframe as agentic business architecture OS | Preserve capability, change market category. |
| Dashboard welcome | Generic resources and demos | Replace with Full Deck onboarding and business examples | First-run should teach the business architecture workflow. |
| Example spaces | Daily news, crypto, retro arcade, Agent Zero videos | Replace most with business-first templates | The examples should prove business value, not general novelty. |
| Resource links | Agent Zero, Space Agent repo, Discord, X, YouTube | Replace with Full Deck links or remove until ready | Avoid sending users into upstream identity. |
| Release artifacts | `Space-Agent-*` installers | Change to Full Deck naming | Required before public desktop release. |
| App IDs | `com.spaceagent.desktop` | Change before first Full Deck release | App ID should be stable once shipped. |
| Hosted share URL | `share.space-agent.ai` | Change or disable until Full Deck share receiver exists | Avoid leaking upstream brand and domain. |
| Docs/contracts | Many docs instruct future agents to preserve Space Agent wording | Rewrite after visible brand pass | Prevent future work from recreating old identity. |

## Remove

These should be removed from the ultimate customization unless there is a deliberate reason to keep them in a hidden developer appendix.

- Astronaut mascot as a product avatar.
- Helmet favicon and desktop icon.
- Starfield/space public backdrop.
- Agent Zero public attribution as primary hero/social proof.
- Agent Zero videos demo space.
- DeepWiki link to the upstream repo as an in-app resource.
- Upstream Discord, YouTube, X links from public or authenticated UI.
- Retro arcade as a default first-run demo.
- Crypto dashboard as a default first-run demo, unless Full Deck has a finance-specific target market.
- Rickroll/demo novelty widgets from first-run paths.
- Public copy that says the product is about "spaces" as the main metaphor.
- Public release links pointing to `agent0ai/space-agent`.

## Maybe Keep As Developer-Only

These may remain in repo history or internal docs but should not appear in launch UI.

- Upstream credits in `NOTICE` or README acknowledgements, especially because the source is MIT licensed.
- Internal compatibility references to legacy `space-agent` paths during migration.
- `space.*` JavaScript runtime namespace in code, at least in phase one.
- The word `space` for low-level code paths where renaming would create unnecessary breakage.
- Existing test histories that mention Space Agent, unless they affect visible output.

## Business-First Replacement Examples

Default templates should demonstrate Full Deck's business architecture promise.

- `Operating System Map`: company offers, owners, workflows, and tools in one board.
- `Client Delivery Hub`: intake, milestones, assets, blockers, and next actions.
- `SOP Builder`: process map, checklist generator, training notes, and version history.
- `Offer Architecture`: audience, promise, proof, pricing, funnel, and delivery model.
- `Content Operations`: idea capture, production board, publishing calendar, repurposing queue.
- `Automation Planner`: trigger/event map, apps, data handoffs, risks, and implementation plan.
- `Executive Command Center`: KPIs, decisions, meeting cadence, priorities, and open loops.

## Recommended Final Architecture

Full Deck OS should feel like a serious business operating surface:

1. `Dealer's Table`: the main free-form command table where the CEO views, arranges, and asks agents to build operating widgets.
2. `One Business Deck`: the single operating deck for the company; departments, clients, products, campaigns, and maturity stages are views or filters over the same deck, not separate sub-decks.
3. `Cards` or `Widgets`: free-form table objects, each a tool, data view, automation, document, browser surface, research brief, risk view, or decision window.
4. `Dealer`: the orchestration intelligence that deals work, escalations, decisions, resources, and agent assignments onto the table.
5. `Agents`: stand-ins for business functions or human roles, such as sales, ops, finance, support, delivery, research, compliance, and content.
6. `System Layers`: firmware, team templates, and user customization mapped from `L0/L1/L2`.
7. `History`: rollback and audit trail as a first-class safety feature.
8. `Templates`: curated business architecture starters replacing novelty demos.

## Dealer's Table Layout Decision

Do not turn the front-facing interface into a fixed dashboard with permanent hard-coded zones. Space Agent's strongest native affordance is free-form widget creation and placement, so Dealer's Table should preserve that freedom.

Launch should provide a curated starting table with CEO-grade widgets already dealt onto it, while letting the CEO and agents add, remove, move, resize, and rebuild widgets freely.

The CEO should also be able to instruct the Dealer, or table agent, to create a custom widget for whatever view, metric, risk, decision, workflow, or operating question the CEO wants to see. The Dealer should interpret the request, determine what information is needed, identify which face cards, number-card work packages, deterministic jobs, data sources, or external integrations are required, and coordinate the agents necessary to gather, validate, and maintain that information.

A custom widget should become a live business instrument on the Dealer's Table, not just a one-time answer. It should continue to provide the requested visibility, update from available data where possible, show uncertainty or missing information where the system is incomplete, and create agent work or risk items when the needed information does not yet exist.

Recommended starting widgets:

- Company pulse: health metrics, priorities, and open loops.
- Decision required: items that need human authority, approval, or liability acceptance.
- Risk profile: business risks shown by likelihood, impact, trend, and escalation status; logarithmic scaling may help existential risks stand out.
- Agent activity: active agents, responsibilities, blockers, completions, and next actions.
- Research briefs: compact sourced context for decisions.
- Architecture map: offers, departments, workflows, tools, automations, dependencies, and owners.
- Dealt cards: highest-priority business objects currently in play.

The visual style should be a command table first, with subtle card-table cues in the background: muted felt green, faint placement marks, restrained card geometry, and a serious executive dashboard foreground.

## Data Population And Business Maturity Model

Dealer's Table must not assume the business already has clean, complete, connected data. A company can enter Full Deck OS at any maturity stage:

- starting from the ground up with little or no formal data
- operating with scattered notes, spreadsheets, SOPs, emails, calendars, and tribal knowledge
- partially digitized with some tools and documents but weak structure
- mature enough to connect live operational systems
- fully instrumented and ready for optimization

The agents should stimulate and build the data foundation over time. Missing, weak, inaccessible, or non-digital information is not just an inconvenience; it is an operational risk and should create agent work.

Recommended model:

1. Agents assess each business function for available data, source quality, ownership, freshness, structure, and decision usefulness.
2. Each widget can display confidence and data maturity, not just the visible metric or card.
3. Missing information becomes a risk when it prevents the OS or CEO from making a reliable decision.
4. Missing information also becomes an action for agents: find it, request it, digitize it, structure it, validate it, or build a process to keep it current.
5. The system should support manual entry, agent-maintained records, uploaded files, extracted documents, connected integrations, and later fully live data feeds.
6. As the business matures, widgets should graduate from manually maintained to connected/live without changing the CEO-facing table metaphor.

This means the opening Dealer's Table can start with partially manual widgets, but every widget should be designed around a future data lifecycle:

- unknown
- manually entered
- agent researched
- document extracted
- system connected
- validated
- monitored
- optimized

The Risk Profile widget should explicitly include data risks, such as "No current cash forecast," "SOP exists only in someone's head," "Client delivery status is spread across messages," or "Sales pipeline data is stale." These risks should feed agent assignments and decision cards.

## Prioritization And Build Sequencing

Full Deck OS must avoid trying to build the entire business system at once. Discovering many missing processes, weak data sources, stale documents, and disconnected tools should not cause every agent to engage simultaneously.

The operating system needs a priority system that sequences business-system development with the CEO rather than overwhelming them.

Principles:

- The CEO has limited attention, decision capacity, and liability bandwidth.
- Internal teams may need time to gather records, answer questions, digitize SOPs, or validate agent findings.
- External systems may require API setup, credentials, vendor access, exports, or integration work.
- Some missing information is urgent because it blocks high-risk decisions; other missing information can wait.
- Agent work should be organized into focused operating campaigns, not an unbounded swarm.

Recommended prioritization model:

1. Triage gaps by risk, decision dependency, business value, effort, data availability, and CEO attention required.
2. Convert the highest-priority gaps into a small active queue of build cards.
3. Limit concurrent agent campaigns so the CEO sees a manageable number of decisions and requests.
4. Route information requests to the right human or system owner instead of defaulting every gap to the CEO.
5. Prefer minimum useful data first, then deepen toward fully connected/live data after the business function is understood.
6. Re-score priorities as new information arrives, risks change, or agents complete work.

Useful priority labels:

- `critical-now`: blocks an immediate executive decision or exposes serious business risk.
- `foundation`: needed before later systems or automations can be trusted.
- `quick-win`: low effort, high clarity, useful for building momentum.
- `delegate`: needs an internal person or team to gather/validate information.
- `integrate`: needs an external API, export, credential, or vendor connection.
- `defer`: known gap, but not worth CEO or agent focus yet.

The Dealer should maintain an active build cadence, such as "next 3 system-building cards," instead of dealing every possible improvement onto the table at once.

This should appear in the starter widgets:

- Decision Required should show only the decisions that truly need CEO authority now.
- Agent Activity should show active campaigns and paused/deferred campaigns separately.
- Risk Profile should distinguish urgent operating risks from known-but-deferred data gaps.
- Dealt Priorities should include the current build queue, not the full backlog.
- Company Pulse should summarize maturity progress without turning every weakness into an emergency.

## Implementation Decisions

Phase 1 should change visible brand without deep runtime renames.

- Keep internal repo path and JS runtime names while changing UI, docs, assets, and package metadata.
- Change `productName`, `appId`, release artifact names, README, page metadata, icons, and public shell visuals before launch.
- Replace default examples with business templates before showing the product to prospects.
- Replace the first-run space with a curated Dealer's Table starter layout made from free-form CEO-grade widgets rather than a rigid fixed dashboard.
- Keep compatibility references for `space.*` APIs in developer docs until a separate technical rename is justified.

Phase 2 can rename technical concepts only if the product direction is stable.

- Consider `space.spaces` to `deck.decks` or similar only after launch proof.
- Consider path renames only when test coverage and migration scripts are ready.
- Avoid broad code-level renames before the launch brand pass; the risk is high and the user-visible benefit is low.

## Decision Summary

Use Space Agent as the engine, not the brand.

Keep the runtime architecture, layered customization model, desktop packaging, admin safety systems, and agent-editable workspace concept. Change the public product identity, first-run experience, visual system, release metadata, and copy. Remove the astronaut, space theme, Agent Zero public links, novelty demos, and upstream-branded URLs from launch-facing surfaces.
