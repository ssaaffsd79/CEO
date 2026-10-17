---
description: Bootstrap and run a lightweight multi-agent development team. Use when starting or adopting a project, planning work, coordinating implementation and optional QA, brainstorming with distinct perspectives, or preserving context across sessions.
name: ai-team-orchestration
---
# AI Team Orchestration

Use three stable agents:

| Agent | Purpose |
|---|---|
| `@ai-team-producer` | Clarify scope, plan proportionately, coordinate, and merge |
| `@ai-team-dev` | Implement, test, self-review, and prepare the pull request |
| `@ai-team-qa` | Independently test behavior when dedicated QA is useful |

Nova, Sage, and Milo are perspectives inside the Dev agent, not mandatory project layers.

## Default Workflow

**Plan -> Implement -> Test -> optional review or QA -> Merge -> update project state**

Keep the workflow proportional:

- Skip formal planning for small, obvious changes.
- Use a short plan for multi-step or cross-cutting work.
- Add independent review or QA when risk, uncertainty, or repository policy justifies it.
- Let branch protection, required checks, permissions, and merge queues enforce repository merge policy.

## Start or Adopt a Project

1. Read existing repository instructions and documentation.
2. Discover the actual stack, architecture, commands, deployment model, and risks.
3. Create or update `PROJECT_BRIEF.md` only when durable cross-session context is useful. Start from the [project brief template](./references/project-brief-template.md) and omit irrelevant sections.
4. For substantial work, create a concise plan from the [sprint plan template](./references/sprint-plan-template.md).
5. Use a separate branch or clone when parallel sessions could conflict, following the repository's own Git policy.

## Execute

### Producer

- Define the outcome, constraints, acceptance criteria, and explicit exclusions.
- Choose review and QA based on risk rather than ceremony.
- Keep durable project state concise and current.

### Dev

- Follow repository conventions and implement the smallest complete solution.
- Run relevant checks and inspect the final diff.
- Open or update the pull request with summary, verification, and limitations.

### QA

- Use only when dedicated behavioral verification adds value.
- Test the requested change and important regressions.
- Report reproducible findings and verify fixes.

## Brainstorms

Use the [brainstorm format](./references/brainstorm-format.md) for product or architecture decisions that benefit from competing perspectives. For ordinary implementation choices, let Dev decide using repository conventions.

## Context Recovery

Before ending a long or interrupted session:

1. Update the active plan or progress note if one exists.
2. Record material decisions, blockers, and the next action in repository context.
3. Use a cold-start prompt such as:

```text
Read the repository instructions, then read whichever sources exist for this
work: the active issue or request, PROJECT_BRIEF.md, and the active plan or
progress note.
Continue from the recorded next action.
```

## Tool and Model Inheritance

The bundled agents intentionally omit `tools` and `model` frontmatter:

- available built-in, MCP, and extension tools remain usable;
- developers keep control of model selection;
- role boundaries are defined by instructions and normal trust, permission, authentication, and approval controls.

If the environment exposes too many tools, deselect irrelevant tools or MCP servers, or use VS Code virtual-tool management. Do not add a machine-specific plugin allowlist.

## Principles

- Prefer working software and clear handoffs over process artifacts.
- Follow repository policy instead of embedding universal Git commands.
- Preserve unknown work and ask before destructive or privileged actions.
- Keep bugs and important decisions in durable project systems, not only chat.
- See [anti-patterns](./references/anti-patterns.md) for concise lessons.

## 在 CubeLV 使用

`@ai-team-producer` / `@ai-team-dev` / `@ai-team-qa` 是角色名稱，預設由同一個 AI 依序扮演：先問清楚範圍，再動手實作，風險高時才獨立驗證。若要真的拆成獨立員工，到 AI 公司建立對應 agent 並把這顆技能掛上去。

出處：github.com/ssaaffsd79/CEO，`ai-team-orchestration/`，2026-10-17 取回；參考檔已內嵌於文末。

# Appended reference files

## references/anti-patterns.md

# Anti-Patterns

| Avoid | Prefer | Why |
|---|---|---|
| One agent owns planning, implementation, testing, and approval | Keep Producer, Dev, and optional QA responsibilities distinct | Independent perspectives reduce blind spots without requiring ceremony for every change. |
| Hardcoded tool or model allowlists | Inherit the developer's enabled tools and selected model | Extensions and MCP tools remain available without plugin updates. |
| A mandatory process for every change | Scale planning, review, and QA to risk | Small changes stay fast; high-impact changes receive more scrutiny. |
| Universal Git command recipes | Follow repository contribution and branch policy | Projects use different remotes, protections, and merge strategies. |
| Rewriting shared history or discarding unknown work | Preserve work and coordinate destructive actions | Parallel sessions and contributors may depend on existing state. |
| Large plans that duplicate project documentation | Record only outcomes, constraints, decisions, and next actions | Concise context is easier to maintain and recover. |
| Bugs and decisions kept only in chat | Use the repository's issue tracker and durable context | Future sessions can discover them. |
| QA fixes application source | QA reports behavior; Dev implements fixes | Separation preserves independent verification. |
| Treating every automated suggestion as a requirement | Assess relevance, confidence, scope, and practical risk | Review should improve the product, not expand scope without limit. |

## Role responsibilities (Do / Don't)

- Producer
  - Do: Clarify outcome, constraints, acceptance criteria, and explicit exclusions; coordinate reviewers and merge policy.
  - Don't: Implement or ship code changes that should be reviewed by Dev.

- Dev
  - Do: Implement the smallest complete solution, run listed verification, include tests, and prepare the PR with verification steps.
  - Don't: Merge without required checks, failing tests, or without documenting risks and decisions.

- QA (optional)
  - Do: Independently verify behavior, file reproducible issues, and confirm fixes after Dev applies them.
  - Don't: Modify application source as a shortcut for failing verification — report and hand back to Dev.

## Decision logging guidance

- Record material decisions in a DECISIONS.md or the repository issue tracker with: title, date, owner, decision summary (1 line), rationale, and link to related PR/issue.
- Keep entries short and searchable; record the next action when a decision defers work.

## references/brainstorm-format.md

# Brainstorm Format

Use this format to produce real creative debate — not generic "the team agrees" output. The key is naming each agent explicitly with a distinct personality and perspective.

## Prompt Template

```
You are orchestrating a brainstorm with the [PROJECT NAME] team.
Each member has a DISTINCT voice, perspective, and expertise.
They should DEBATE, build on each other's ideas, and CHALLENGE weak concepts.
This is a creative session — no idea is too wild in Phase 1.

### Kira (Product Designer)
- Thinks about: user delight, accessibility, "would this be fun?"
- Tendency: pushes for features that spark joy, pushes back on anything that feels like homework

### Milo (Experience/Design Perspective)
- Thinks about: accessibility, presentation, content, cohesion, "does this feel right?"
- Tendency: advocates for user experience, sometimes at odds with engineering feasibility

### Nova (Client/Interaction Perspective)
- Thinks about: user-facing behavior, interaction, state, "can we actually build this?"
- Tendency: pragmatic, flags scope risks, suggests simpler alternatives

### Sage (Core/Service Perspective)
- Thinks about: domain logic, data, services, integrations, security, "where do risks live?"
- Tendency: security-first, sometimes over-engineers, good at spotting edge cases

### Remy (Producer)
- Thinks about: timeline, scope, "will this ship?"
- Tendency: cuts scope aggressively, keeps the team focused on deliverables

### Ivy (QA Engineer)
- Thinks about: testability, edge cases, "what breaks when the user does X?"
- Tendency: pessimistic about reliability, asks uncomfortable "what if" questions

Phase 1 — Free Ideation:
Each agent pitches 2-3 raw ideas from their perspective.
Wild ideas welcome. No filtering.

Phase 2 — Discussion & Refinement:
Agents debate, combine, and critique ideas.
They reference each other by name: "Kira, that's great but..."
They push back on weak points.
At least 2 genuine disagreements.

Phase 3 — Final Pitches:
3-5 polished concepts.
Each concept includes: name, description, pros, cons, estimated effort.
Team vote with brief justification from each voter.

Write the result to one concise design note unless the project needs separate artifacts.
```

## Tips

- **Name each agent** — "you are the full team" produces bland consensus
- **Define tendencies** — gives the LLM permission to disagree
- **Require disagreements** — "at least 2 genuine disagreements" prevents groupthink
- **Keep the output proportional** — one note is usually enough
- **Customize personas** — adjust for your domain (e.g., replace Kira with a Data Scientist for ML projects)

## Mini-Brainstorm (Quick Version)

For smaller decisions (e.g., "how should we implement the scoreboard?"):

```
Run a team brainstorm about [TOPIC].
Each agent speaks separately with their own perspective.
They should debate and disagree.
Write results to docs/[topic]-design.md.
```

## Team Consilium

Before major sprints, validate the plan:

```
Run a team consilium on the Sprint N plan.
Each agent reviews from their perspective:
- Kira: Is it fun / useful? Missing features?
- Nova: Technically feasible? Scope risks?
- Sage: Security concerns? API design issues?
- Milo: Visual consistency? Design system gaps?
- Ivy: Testable? Edge cases?
- Remy: Timeline realistic? What to cut?

Flag issues and suggest fixes.
```

## Sample agent prompts (minimal)

- Producer (short):
```
You are Remy, the Producer. Summarize the outcome, constraints, and acceptance criteria in 4 lines max. List required reviewers and whether QA is needed. End with the single next action.
```

- Dev (short):
```
You are Nova+Sage (Dev). Given the plan, produce an implementation checklist: files to change, tests to add, and verification commands. Keep it actionable.
```

- QA (short):
```
You are Ivy (QA). List 6 focused test scenarios (happy path + 5 edge cases) and the exact steps to reproduce each. Include expected results.
```

## references/project-brief-template.md

# PROJECT_BRIEF.md Template

Use this only when the project benefits from durable context across sessions. Keep it concise and omit irrelevant sections.

```markdown
# PROJECT_BRIEF.md - [Project Name]

> Last updated: [date]

## 1. Goal and Users

[What the project is, who it serves, and the outcome it should create.]

## 2. Current Scope

**In scope**
- [outcome]

**Out of scope**
- [explicit exclusion]

## 3. Stack and Architecture

- Runtime/language: [value]
- Frameworks/libraries: [value]
- Data/services: [value]
- Deployment: [value or not applicable]
- Tests/checks: [verified commands]

[Short architecture description or diagram when useful.]

## 4. Key Files

| Area | Path | Purpose |
|---|---|---|
| [area] | `[path]` | [purpose] |

## 5. How to Work

- Setup: [verified command or link]
- Run: [verified command or link]
- Test: [verified commands]
- Deploy: [verified process or not applicable]
- Repository rules: [links to contribution/security instructions]

## 6. Safety and Constraints

- [secrets/privacy/data rules]
- [compatibility or reliability invariant]
- [operational constraint]

## 7. Current State

**Working**
- [item]

**Known issues**
- [issue/link]

**Next**
- [next outcome]

## 8. Team and Handoff

- Producer: scope, coordination, and merge
- Dev: implementation and verification
- QA: optional independent behavioral verification

## Onboarding checklist (add to brief)

- Setup verified: `npm ci` / `pip -r requirements.txt`
- Tests run: `npm test` / `pytest -q`
- Lint pass: `npm run lint`
- Where to find CI logs and deploy dashboards

## Where to record decisions

- Add short entries to DECISIONS.md or create an issue with the decision tag. Each entry should include: title, date, owner, 1-line summary, rationale, and link to PR/issue.

Record material decisions, blockers, and the next action here or in the active plan. Use GitHub Issues or the repository's tracker for bugs and follow-up work.
```

## references/sprint-plan-template.md

# Work Plan Template

Use this for substantial work. Small, clear changes can proceed directly from the issue or request.

```markdown
# [Work Item] - Plan

## Goal

[One observable outcome.]

## Context

- Relevant issue/request: [link or summary]
- Repository instructions: [links]
- Important constraints: [list]

## In Scope

- [deliverable]

## Out of Scope

- [explicit exclusion]

## Tasks

1. [task]
2. [task]
3. [task]

## Acceptance Criteria

- [ ] [observable behavior]
- [ ] Relevant repository checks pass (example: `npm run lint`, `npm test`)
- [ ] Tests covering the change are added or validated
- [ ] Documentation/context is updated when behavior or operation changed

## Verification

- Automated: [commands or checks]
  - Example: `npm ci && npm run test` or `pytest -q`
  - Example: `npm run lint && npm run build`
- Manual: [focused scenarios, if useful]
- Independent review: required / optional / not needed - [reason]
- QA: required / optional / not needed - [reason]

## PR Checklist (add to PR body)

- Branch name follows repo policy (e.g., `feat/`, `fix/`, or `chore/`)
- Description: short summary, why, and acceptance criteria
- Verification steps included (commands & manual checks)
- Tests added or existing tests updated
- Relevant docs/PROJECT_BRIEF updated if behavior changed
- Reviewers: @team or specific owners
- Required checks: list CI jobs that must pass
- Release notes / changelog entry: yes/no

## Risks and Decisions

- [risk or material decision]

## QA risk matrix (when to require QA)

- High impact × High uncertainty = QA required
- High impact × Low uncertainty = QA recommended
- Low impact × High uncertainty = QA recommended
- Low impact × Low uncertainty = QA optional

## Next Action

[owner and immediate next step]
```

## Progress Note

For long-running work, keep a short progress note:

```markdown
# [Work Item] - Progress

- Completed: [items]
- In progress: [item]
- Blocked: [issue or none]
- Decisions: [material decisions]
- Verification so far: [results]
- Next action: [specific action]
```

## Dev Handoff

```text
Read the repository instructions, PROJECT_BRIEF.md when present, and this plan.
Implement the in-scope work, run the listed verification, update durable context
when needed, and prepare a pull request. Do not merge.
```
