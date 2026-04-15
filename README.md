# Claude Cortex

**I built a cortex for Claude Code. Three businesses run on it.**

Claude Code is a brainstem. It reads files, runs tools, writes code. Brilliant at any single task. Amnesic between them. Nothing compounds.

Claude Cortex is the layer that wraps around it. Persistent memory that survives sessions. Follow-up loops that escalate automatically. A morning routine that turns a calendar, an inbox, and a CRM into a single HTML file of copy-paste actions ordered by friction. Drafts in your voice, not AI voice. Every conversation updates canonical files the next conversation reads from.

The brainstem handles the moment. The cortex handles the week.

If you starred [claude-focus](https://github.com/assafkip/claude-focus) for the attention hooks, this is the OS version. Same philosophy, scaled to multi-project operators.

---

## Contents

- [Receipts](#receipts)
- [30-second overview](#30-second-overview)
- [Install](#install)
- [Start with one piece](#start-with-one-piece)
- [How it works](#how-it-works)
- [What got scrubbed before shipping](#what-got-scrubbed-before-shipping)
- [Architecture](#architecture)

---

## Receipts

One laptop, three brands, one cortex:

- **11 project instances** from one shared skeleton. Change a rule once, propagate everywhere.
- **15 OSINT investigations closed** through the investigator instance.
- **10 client deliverables shipped** through the consulting instance.
- **Dozens of daily HTML schedules** generated. Every follow-up pre-drafted. Every open loop tracked.

---

## 30-second overview

What's in this repo:

- **4 plugin groups** (core, ops, design, memory-lifecycle) — modular, you can use one without the rest
- **8 agent skills** — voice enforcement, AUDHD rules, research mode with citations, design orchestration
- **40 specialist agents** — preflight, data ingest, synthesizer, content reviewer, engagement hitlist, and more
- **69 MCP tools** — instance management, loop tracking, linters, scoring, schema generators
- **25 slash commands** — `/q-morning`, `/q-debrief`, `/q-engage`, `/q-calibrate`, `/q-research`, etc.
- **8 hooks** — token guard, wiring check, session start, post-compact, auto-commit, stop logger
- **18 path-scoped rule files** — behavioral constraints that fire based on where you are in the repo

What's NOT in this repo: my actual data. All canonical memory, relationships, writing samples, and project context ship as templates. You bring your own brain.

---

## Install

```bash
npm install -g @anthropic-ai/claude-code
git clone https://github.com/assafkip/claude-cortex.git
cd claude-cortex && claude
```

First session walks you through setup: who you are, what you're building, how you write, who you know. Takes about 20 minutes. Then run `/q-morning` for your first daily action plan.

Second business on the same cortex:

```bash
./kipi new ~/projects/second-business second-business
```

Every instance shares the skeleton. Edit a rule once, pull it into every instance with `kipi update`.

---

## Start with one piece

You don't have to adopt the whole OS to get value. Lift a single part:

| Want this | Copy this |
|-----------|-----------|
| Force citation-backed answers with zero hallucination | `plugins/kipi-core/skills/research-mode/` |
| Follow-up loops that auto-escalate at 7 and 14 days | `plugins/kipi-core/kipi-mcp/src/kipi_mcp/loop_*.py` |
| Token guard that halts runaway AI runs | `q-system/.q-system/token-guard.py` |
| Voice enforcement (your voice, not AI voice) | `plugins/kipi-core/skills/founder-voice/` + samples |
| Morning HTML schedule generator | `q-system/marketing/templates/build-schedule.py` |
| AUDHD / executive-function output rules | `.claude/rules/audhd-interaction.md` |

Drop any of those into an existing Claude Code project. The cortex is modular by design because I built it that way for myself across instances.

---

## How it works

### Run `/q-morning`, get your day

The system pulls from your calendar, email, CRM, and social platforms. Reads every open loop. Checks what went cold. Produces a single HTML file:

- **Copy-paste actions sorted by friction.** 2-minute replies first, deep work later. Momentum builds before the hard stuff.
- **Every follow-up pre-written in your voice.** Fed from your writing samples, your word choices, your pet peeves.
- **Open loops with escalation.** Sent a DM 7 days ago with no reply? The follow-up is already drafted. 14 days? Forced decision: send, park, or kill.
- **Meeting prep with context.** Who you're meeting, what you discussed last time, what they care about, suggested talking points.

Open the HTML. Start at the top. Work down. Done.

### Paste a conversation. Get your next 10 actions.

Paste a transcript. The system extracts what resonated, what got pushback, what you owe them, new objections to prepare for. Then it routes each insight to the right file automatically. Talk tracks update. Relationship file updates. Follow-up email drafted and waiting in tomorrow's HTML.

After 50 conversations, the system knows your market better than you do. Because it remembers everything. You don't have to.

### Nothing gets forgotten

Every outbound action opens a loop. Every loop has a timer.

| Days open | What happens |
|-----------|-------------|
| 0-2 | Quiet. Listed in your dashboard. |
| 3-6 | Follow-up drafted. Shows in your action plan. |
| 7-13 | Flagged. Shows at the top. "This is going cold." |
| 14+ | Forced decision. Act now, park for later, or kill it. |

Loops auto-close when the system detects a response. Gmail reply? Closed. LinkedIn DM reply? Closed. You don't track anything. The system tracks everything.

### Built for ADHD. Works for everyone.

- **No decisions.** The system picks who to contact, what to say, in what order, through which channel.
- **No shame.** Never "overdue." Always "carried forward." Language matters when your brain punishes you for every dropped ball.
- **Friction-ordered.** Quick wins first. Dopamine before discipline.
- **Effort-tracked.** "You sent 4 messages today" matters more than "nobody responded yet."

This isn't a feature toggle. It's how the whole system thinks.

### A brain that compounds

- **Canonical memory.** Positioning, objections + responses that worked, competitive landscape, every relationship. Every workflow reads from this. Every conversation updates it.
- **Time-layered recall.** 48-hour scratch expires. Weekly patterns roll up. Monthly insights persist. The brain forgets what doesn't matter and strengthens what does.
- **Knowledge graph.** Links people, companies, what they said, how they relate. An insight from 3 weeks ago changes what the system suggests today.

### The AI needs scaffolding too

LLMs forget instructions from earlier in the context ("Lost in the Middle," Stanford 2023). They rush to produce output, skip boring middle steps, self-report completion without verifying. Sound familiar?

So the cortex has guardrails for the AI, not just for you:

- **Verification gate.** Before the HTML builds, a script checks the JSON output. If verification fails, the build is blocked. The AI can't bypass it.
- **Echo of Prompt.** Before each step executes, a script re-injects that step's requirements fresh into context. Combats attention drift.
- **No self-authorized skipping.** The AI cannot decide on its own to skip a step. It must ask.
- **Structured deliverables, not text summaries.** The system logs what was actually produced, not "done."

Research basis: "Lost in the Middle" (Stanford), "Context Degradation Syndrome," "LLMs Get Lost in Multi-Turn Conversation" (Laban et al. 2025).

---

## What got scrubbed before shipping

This repo is a scrubbed fork of the private system I run every day. Being honest about what that means:

**Shipped real:**
- All code, hooks, MCP tools, agent definitions, linters, scoring logic
- All skill logic (voice enforcement, AUDHD rules, research mode, design orchestration)
- All templates, schemas, workflow definitions
- All rules and path-scoped behavioral constraints

**Shipped as scaffolds (you fill them):**
- `q-system/canonical/*` — positioning, objections, talk tracks, market intel
- `q-system/my-project/*` — your profile, ICP, relationships, current state
- `plugins/kipi-core/skills/founder-voice/references/*` — your writing samples
- `instance-registry.json` — empty array, populated as you run `kipi new`

**Removed entirely:**
- My business-specific brand terms (configurable in `validator.py` via `BRAND_PATTERNS`)
- My cluster bridge system (was tied to 4 of my internal instances)
- Internal migration scripts and instance-registry contents
- `memory/` and `output/` directories (ephemeral, not meant to share)

Nothing functional was removed. If a feature exists in the code, it works.

---

## Commands

| What you want to do | Command |
|---------------------|---------|
| Generate your entire day | `/q-morning` |
| Process a conversation | `/q-debrief` (or just paste a transcript) |
| Draft a quick email or DM | `/q-draft` |
| Get engagement actions for prospects' posts | `/q-engage` |
| Plan your week's content | `/q-market-plan` |
| Update your positioning from new info | `/q-calibrate` |
| Stress-test your positioning | `/q-reality-check` |
| End-of-day health check | `/q-wrap` |
| Save context for next session | `/q-handoff` |
| Research with citations only | `/q-research <topic>` |

Full list in `q-system/.q-system/commands.md`.

---

## Connects to

Works standalone with local files. Each integration adds capability:

| Tool | What it adds |
|------|-------------|
| Notion | CRM, pipeline, relationship tracking |
| Google Calendar | Meeting detection, auto-prep |
| Gmail | Email monitoring, loop auto-close on reply |
| Apify | X/Twitter scraping (lead sourcing) |
| Reddit MCP | Reddit search, posts, comments (no auth needed) |
| Chrome | LinkedIn (profiles, posts, DMs, engagement), analytics |
| RSS feeds | Medium, Substack content (via WebFetch) |
| Slack | Notifications, approval workflows |

---

## Architecture

```
claude-cortex/
├── kipi                          # CLI: update, new, dev, list
├── plugins/                      # 4 plugin groups
│   ├── kipi-core/                # Founder OS, research mode, voice, AUDHD
│   │   ├── skills/               # 8 agent skills
│   │   └── kipi-mcp/             # 69 MCP tools
│   ├── kipi-ops/                 # Ops: ingest, synth, engagement
│   ├── kipi-design/              # Brand, UI/UX, design orchestration
│   └── memory-lifecycle/         # Working/weekly/monthly memory rotation
│
├── q-system/
│   ├── .q-system/
│   │   ├── commands.md           # 25 slash commands and workflows
│   │   ├── agent-pipeline/       # 40 specialist agents + bus protocol
│   │   ├── hooks/                # Token guard, wiring check, auto-commit
│   │   └── preflight.md
│   ├── canonical/                # Source of truth (template)
│   ├── my-project/               # Your context (template)
│   ├── marketing/                # Content templates, guardrails
│   └── methodology/              # Debrief template, operating modes
│
└── .claude/
    ├── rules/                    # 18 path-scoped behavioral rules
    ├── agents/                   # Custom agents
    └── settings.json             # Hooks, permissions, output style
```

---

## Not just for founders

The pattern works anywhere humans manage concurrent relationships and compound knowledge.

**Lawyers** — case files as canonical state, filing deadlines as loops, client conversations as debriefs.

**Sales teams** — accounts as relationships, proposals as loops, call notes as debriefs.

**Doctors** — patients as relationships, referrals and labs as loops, visit notes as debriefs.

**Consultants** — clients as relationships, deliverables as loops, stakeholder meetings as debriefs.

Fork it. Replace the canonical files with your domain. The scaffolding does the rest.

---

## Security

- `.env`, credentials, and key files blocked from read/write
- PreToolUse hooks intercept dangerous operations at runtime
- No secrets in committed files
- `rm -rf`, `sudo`, `git push --force` denied by default

---

## Contributing

Early days. If you fork this and adapt it to a domain (law, medicine, sales, academic research), open an issue with a link. Contrib hooks:

- New rule packs in `.claude/rules/`
- New agent specialists in `q-system/.q-system/agent-pipeline/agents/`
- New MCP tools in `plugins/kipi-core/kipi-mcp/`
- Bug fixes in linters, scorers, or the morning pipeline

---

## Related

[claude-focus](https://github.com/assafkip/claude-focus) is the minimal version — 3 hooks, no plugins, for a single project. Claude Cortex is the OS you graduate to when one project isn't enough.

---

## License

MIT. Fork it, ship it, teach it your brain.
