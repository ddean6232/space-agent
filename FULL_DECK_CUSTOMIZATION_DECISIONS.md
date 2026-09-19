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

1. `Control Room`: main dashboard for workspaces, systems, recent changes, and team/client areas.
2. `Decks`: rebranded spaces, each representing a business system, client hub, or workflow.
3. `Cards` or `Blocks`: rebranded widgets, each a tool, data view, automation, document, or browser surface.
4. `Architect`: the agent persona, focused on building, documenting, and improving business systems.
5. `System Layers`: firmware, team templates, and user customization mapped from `L0/L1/L2`.
6. `History`: rollback and audit trail as a first-class safety feature.
7. `Templates`: curated business architecture starters replacing novelty demos.

## Implementation Decisions

Phase 1 should change visible brand without deep runtime renames.

- Keep internal repo path and JS runtime names while changing UI, docs, assets, and package metadata.
- Change `productName`, `appId`, release artifact names, README, page metadata, icons, and public shell visuals before launch.
- Replace default examples with business templates before showing the product to prospects.
- Keep compatibility references for `space.*` APIs in developer docs until a separate technical rename is justified.

Phase 2 can rename technical concepts only if the product direction is stable.

- Consider `space.spaces` to `deck.decks` or similar only after launch proof.
- Consider path renames only when test coverage and migration scripts are ready.
- Avoid broad code-level renames before the launch brand pass; the risk is high and the user-visible benefit is low.

## Decision Summary

Use Space Agent as the engine, not the brand.

Keep the runtime architecture, layered customization model, desktop packaging, admin safety systems, and agent-editable workspace concept. Change the public product identity, first-run experience, visual system, release metadata, and copy. Remove the astronaut, space theme, Agent Zero public links, novelty demos, and upstream-branded URLs from launch-facing surfaces.
