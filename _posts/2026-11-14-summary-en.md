---
layout: default
title: "Horizon Summary: 2026-11-14 (EN)"
date: 2026-11-14
lang: en
---

> From 105 items, 4 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Mobile automation MCP server uses diff-based UI updates and pruned tool descriptions](#item-ai-practitioner-1) ⭐️ 9.0/10
2. [DeepSeek UE5 Workflow with Architecture Maps and Strict Rules](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Sync agent memory across tools with symlinks and stale-path checks](#item-ai-practitioner-3) ⭐️ 8.0/10
4. [Nightshift plugin structures long-running agent workflows](#item-ai-practitioner-4) ⭐️ 8.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Mobile automation MCP server uses diff-based UI updates and pruned tool descriptions](https://www.reddit.com/r/ClaudeCode/comments/1xvla12/i_gave_claude_code_a_phone/) ⭐️ 9.0/10

The author built phonedriver, an MCP server that lets Claude Code control Android or iPhone apps. The agent reads the screen as a numbered list of UI elements and taps by number. After each tap, the system returns only the lines that changed. This diff-based approach reduced screen read time to 13 ms, compared to 2.2 seconds for \`adb shell uiautomator dump\`. In testing, Sonnet 5.5 passed 27 of 27 runs on 658k tokens, while mobile-mcp passed 17 of 18 on 4.57M tokens. The author also hid unused arguments from tool descriptions, reducing their size from 10,987 characters to 5,107 without breaking functionality.

reddit · r/ClaudeCode · /u/Puzzled-Stick9170 · Nov 13, 22:07

**「Actionable insight」** Remove unused arguments from tool descriptions to reduce token consumption and context load. The source reports this cut tool definition size by ~53% with no loss in functionality.

**「Evidence and limits」** Performance metrics come from nine phone jobs using Sonnet 5.5 and a comparison with mobile-mcp. The bug hunt test involved two planted bugs and nine benchmark runs. The pizza order test used Opus 5.5 on dominos.co.uk. The author notes that phonedriver holds any tap on Pay or Place order and asks for confirmation first.

**Tags**: `#agent-tooling`, `#token-optimization`, `#mobile-automation`, `#mcp-patterns`, `#cost-control`

---

<a id="item-ai-practitioner-2"></a>
### [DeepSeek UE5 Workflow with Architecture Maps and Strict Rules](https://www.reddit.com/r/DeepSeek/comments/1xw7fyb/from_claude_to_deepseek_game_dev_in_ue5/) ⭐️ 8.0/10

A developer switched from Claude to DeepSeek for Unreal Engine 5.4.4 C++ development. The workflow relies on a strict guideline referenced in every message. An \`Architecture\_Map.md\` file tracks project structure and updates with changes. A \`claude.md\` file \(used as a skills file\) contains rules to reduce hallucinations. The model uses Flash 1017 Max. The developer reports 97% cache hit percentages and recompacts context at 50% usage. Total cost so far is 50 cents. The setup avoids complex commands to maintain ease of access.

reddit · r/DeepSeek · /u/MorbilyABeast · Nov 14, 17:04

**「Actionable Steps」** Implement a &\#x27;skills file&\#x27; that the model references in every message. Include an architecture map in Markdown and enforce critical rules: no placeholders, no phantom variables, never guess architecture, state exact file placement, and show contextual lines for edits. Require the model to read the architecture map before modifying code. Recompack context when usage reaches 50%.

**「Constraints and Observations」** The author states DeepSeek is &\#x27;not As good as something like opus 5.5&\#x27; but suitable for their workflow. The method depends on maintaining a live \`Architecture\_Map.md\`. The author uses a specific harness configuration to mimic Claude&\#x27;s interface. Cache hit rates hover around 97%.

**Tags**: `#prompt-engineering`, `#context-management`, `#cost-optimization`, `#agent-workflow`, `#code-generation`

---

<a id="item-ai-practitioner-3"></a>
### [Sync agent memory across tools with symlinks and stale-path checks](https://www.reddit.com/r/cursor/comments/1xw2iqy/sharing_one_project_memory_across_cursor_claude/) ⭐️ 8.0/10

Place AGENTS.md at the repo root. Run ln -s AGENTS.md CLAUDE.md so Cursor, Codex, and Claude Code read the same file. Record rejected options in docs/decisions.md to prevent re-proposal. End each session by appending five key decisions to that file. After a rename or refactor, run a grep-based script to list paths cited in AGENTS.md and docs/decisions.md that no longer exist.

reddit · r/cursor · /u/ibitneo · Nov 14, 13:33

**「Action」** Symlink CLAUDE.md to AGENTS.md and run the provided grep script after refactors to catch stale file references.

**「Limits」** The script only checks whether a referenced path still exists. It does not flag cases where code moved and an old plan no longer makes sense.

**Tags**: `#agent-memory`, `#context-management`, `#workflow-automation`, `#refactoring`, `#multi-tool-integration`

---

<a id="item-ai-practitioner-4"></a>
### [Nightshift plugin structures long-running agent workflows](https://www.reddit.com/r/codex/comments/1xvp9b3/nightshift_a_plugin_for_longrunning_coding_agents/) ⭐️ 8.0/10

Nightshift is a free, MIT-licensed plugin for Codex, Claude Code, and Cursor. It separates planning from execution to manage long-running coding tasks. The planning phase keeps project code read-only while the agent and user define a punch list with clear definitions of done. The execution phase works through items or toward a goal within set time or token limits. A clock-out gate prevents the agent from stopping with unfinished items. The system persists state on disk, allowing progress to survive context compaction, session restarts, or switches between supported agents. Each task generates a receipt that records delivered work, rejected attempts, running checks, duration, and token usage. Users specify evidence types such as screenshots or test outputs during planning. A watchman process handles recovery from crashes, stalls, or API outages.

reddit · r/codex · /u/orwamahmoud · Nov 14, 01:05

**「Actionable step」** Adopt the plan-receipt-review structure by defining explicit evidence requirements and definitions of done before starting long-running agent tasks, even if not using the Nightshift plugin.

**Tags**: `#agent-workflow`, `#context-management`, `#auditability`, `#long-running-tasks`

---