---
layout: default
title: "Horizon Summary: 2026-11-09 (EN)"
date: 2026-11-09
lang: en
---

> From 116 items, 4 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Five design rules for unattended AI coding agents](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [LiveNerf benchmarks miss token-efficiency drops in agentic workflows](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Hide AI PR details behind HTML &lt;details&gt; tags](#item-ai-practitioner-3) ⭐️ 8.0/10
4. [Local ledger persists agent sessions for context handoffs](#item-ai-practitioner-4) ⭐️ 8.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Five design rules for unattended AI coding agents](https://www.reddit.com/r/ChatGPTCoding/comments/1xrsu8g/lessons_from_running_ai_coding_agents_unattended/) ⭐️ 8.0/10

The author automated a manual loop of planning, building, and reviewing code into an open-source tool. Five design rules emerged from this process. First, separate the planner from the builder using different system prompts and working directories; the planner writes plans and reviews, while the builder writes code. Second, make every phase a git commit to create an audit trail and enable reverts. Use separate git worktrees for parallel lanes so agents do not share a checkout. Third, verify each phase against explicit acceptance criteria using a checker other than the agent that performed the work, as passing tests does not guarantee requirement coverage. Fourth, assume crashes by storing jobs in a SQLite queue with renewable leases, allowing workers to resume mid-phase after restarts and pause before hitting usage limits. Fifth, treat prompt caching as a design constraint by placing stable context in the system prompt and volatile context in the user prompt to avoid paying full price for per-call data.

reddit · r/ChatGPTCoding · /u/premjethwa · Nov 9, 14:19

**「Actionable steps」** Split agent roles into distinct planner and builder instances with separate prompts and directories. Enforce git commits at every phase boundary and use independent checkers for acceptance criteria. Implement job queues with leases to handle crashes and segregate stable versus volatile context in prompts to optimize caching costs.

**Tags**: `#agent-orchestration`, `#workflow-design`, `#reliability-patterns`, `#prompt-engineering`, `#version-control`

---

<a id="item-ai-practitioner-2"></a>
### [LiveNerf benchmarks miss token-efficiency drops in agentic workflows](https://www.reddit.com/r/ClaudeCode/comments/1xrqsbc/nerf_debates_and_benchmarks_such_as_livenerf_two/) ⭐️ 8.0/10

Public LiveNerf benchmarks show stable accuracy for Opus over 47 days. Personal multi-agent logs reveal Opus output tokens per reply jumped from ~420 to ~1,150 on Nov 4–5, while Sonnet and Haiku tokens remained flat. The author verified identical system prompts, tools, Claude Code version \(2.1.309\), and model IDs during the spike. LiveNerf uses single-turn exam questions without tools, ignoring token cost. It also runs on one account, potentially missing staged rollouts, and requires two consecutive 10-day windows of score drops to flag a nerf.

reddit · r/ClaudeCode · /u/KAMIKAZEE93 · Nov 9, 12:47

**「Monitor tokens-per-reply with control agents」** Track output tokens per reply in your agent logs rather than relying solely on accuracy scores. Use Sonnet or Haiku as control agents on the same tasks to isolate model-specific drift from task complexity changes.

**「Scope and verification limits」** The finding relies on a single user&\#x27;s logs and account. The author confirmed no changes to project scope or configuration during the observed period. LiveNerf&\#x27;s methodology intentionally filters short-term fluctuations, which may delay detection of sudden behavioral shifts like increased verbosity.

**Tags**: `#agent-evaluation`, `#model-monitoring`, `#token-efficiency`, `#benchmark-critique`, `#workflow-debugging`

---

<a id="item-ai-practitioner-3"></a>
### [Hide AI PR details behind HTML &lt;details&gt; tags](https://simonwillison.net/2026/Nov/9/details-summary/) ⭐️ 8.0/10

Simon Willison hides verbose AI-generated PR descriptions in GitHub using HTML &lt;details&gt;&lt;summary&gt; tags. He writes a concise, human-curated summary as the &lt;summary&gt; content. The full agent output goes inside the &lt;details&gt; block. GitHub renders this as a collapsed heading with an expansion arrow. This lets reviewers see the high-level intent without reading the full &quot;slop&quot; immediately.

rss · Simon Willison - Coding Agents · Nov 9, 04:25

**「Action」** Wrap AI-generated PR descriptions in &lt;details&gt;&lt;summary&gt; tags. Place a short, human-written explanation in the &lt;summary&gt; tag to serve as the visible preview.

**「Constraints」** GitHub Markdown supports these tags natively. The author notes he still wishes GitHub added a dedicated editor button for this pattern, implying manual typing is required.

**Tags**: `#code-review`, `#agent-workflow`, `#github-practices`, `#prompt-output-formatting`

---

<a id="item-ai-practitioner-4"></a>
### [Local ledger persists agent sessions for context handoffs](https://www.reddit.com/r/codex/comments/1xrhwy9/i_built_a_local_ledger_for_codex_claude_code_and/) ⭐️ 8.0/10

The author released Wisdom, a local tool that records full sessions for Claude Code, Codex, and Pi. It stores every prompt, command output, and file diff in a .wisdom/ folder within the project. Agents use a skill to read this ledger, allowing them to find the specific turn that changed a file and understand the intent behind it. This enables a new agent to pick up work where a previous one stopped without manual summarization or re-explanation.

reddit · r/codex · /u/Fit-Fail-3369 · Nov 9, 04:06

**「Action」** Install Wisdom globally and connect it to your project using npm install -g wisdom and wisdom connect to enable automatic session logging for agent handoffs.

**Tags**: `#agent-handoffs`, `#context-management`, `#debugging-workflow`, `#session-persistence`, `#multi-agent-coordination`

---