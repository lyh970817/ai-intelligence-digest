---
layout: default
title: "Horizon Summary: 2026-08-23 (EN)"
date: 2026-08-23
lang: en
---

> From 102 items, 3 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Fix DeepSeek Harness session amnesia with MemOS Local Plugin](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Use Fable 5 as orchestrator to constrain Opus 5 execution](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Codex writes, Claude Code reviews](#item-ai-practitioner-3) ⭐️ 8.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Fix DeepSeek Harness session amnesia with MemOS Local Plugin](https://www.reddit.com/r/DeepSeek/comments/1vw0i8b/i_tried_fixing_deepseek_harness_forgetting/) ⭐️ 8.0/10

DeepSeek Harness loses session state, forcing manual context re-entry. The root cause is the lack of a persistent memory layer, not model reasoning limits. Installing the MemOS Local Plugin via the Cordis system adds local persistence without modifying source code or adding API keys. Installation uses a one-line bash script on macOS/Linux. On Windows, resolve \`ERR\_PNPM\_IGNORED\_BUILDS\` by running \`pnpm approve-builds --all\` in the profile folder. The plugin automatically injects stored stack rules \(e.g., Python 3.12, uv\) into new sessions. It also enforces negative constraints, such as skipping Docker Compose when instructed. Background summarization makes execution traces searchable.

reddit · r/DeepSeek · /u/Miserable-Lie28 · Aug 23, 07:25

**「Actionable steps」** Install the MemOS Local Plugin to persist stack constraints across DeepSeek Harness sessions. Use the MemOS Viewer UI to delete junk data and override outdated rules when switching project stacks.

**「Operational constraints」** Storing temporary debug logs clutters the index; regular cleanup is required. Conflicting instructions arise if old preferences are not explicitly overridden or deleted when changing stack choices. The local plugin suffices for single profiles; route memory through Memmy to sync across agents like Cursor.

**Tags**: `#agent-memory`, `#context-management`, `#workflow-automation`, `#deepseek-harness`, `#state-persistence`

---

<a id="item-ai-practitioner-2"></a>
### [Use Fable 5 as orchestrator to constrain Opus 5 execution](https://www.reddit.com/r/ClaudeCode/comments/1vvpkka/dont_downgrade_from_opus_5_just_stop_letting_it/) ⭐️ 8.0/10

The author stopped using Opus 5 as the main orchestrator in Claude Code after it repeatedly identified non-existent problems and broke their repository. They switched to a multi-agent workflow where Fable 5 acts as the high-effort orchestrator. Fable writes full specs and verifies results, while Opus 5 executes strictly within those bounds at full reasoning effort. Smaller tasks are routed to Sonnet 5 and Haiku. This setup uses CLAUDE.md for always-on rules, a router.md for routing maps, and a model-postures.md file injected via UserPromptSubmit hooks to enforce per-model constraints.

reddit · r/ClaudeCode · /u/CraveFounder · Aug 22, 22:15

**「Decouple spec-writing from execution」** Assign a dedicated orchestrator model \(e.g., Fable 5\) to write specs and verify outputs, while restricting high-reasoning models \(e.g., Opus 5\) to scoped execution roles to prevent context drift and unasked refactoring.

**「Implementation details and scope」** The author runs this workflow 8–10 hours daily on a 20x Max plan. Fable consumes a small share of tokens, keeping weekly caps manageable. The specific prompt injections include rules for Opus 5 to &\#x27;deliver the requested scope and stop before unasked work&\#x27; and for Sonnet 5 to avoid auditing surrounding systems or creating subagents.

**Tags**: `#agent-orchestration`, `#prompt-engineering`, `#workflow-design`, `#model-routing`, `#scope-control`

---

<a id="item-ai-practitioner-3"></a>
### [Codex writes, Claude Code reviews](https://www.reddit.com/r/ChatGPTCoding/comments/1vv7wm3/codex_writes_claude_code_reviews_my_experience_so/) ⭐️ 8.0/10

The author switched from using Codex for all tasks to a split workflow: Codex writes code and tests, while Claude Code reviews. The reviewer agent executes tests, runs the code, and performs mutation testing instead of only reading diffs. This setup caught issues CI missed, such as UI placeholders for non-existent backend data and tests that verified helper functions rather than product logic.

reddit · r/ChatGPTCoding · /u/Vegetable-Try807 · Aug 22, 09:36

**「Operator Takeaway」** Grant the review agent permission to execute tests and mutate code to verify behavior, rather than restricting it to static diff analysis.

**「Evidence and Limits」** The report is based on a single pet project. The author states the specific models are interchangeable; the value lies in decoupling generation from active verification.

**Tags**: `#agent-workflow`, `#code-review`, `#testing-strategy`, `#model-routing`, `#mutation-testing`

---