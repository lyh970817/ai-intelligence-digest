---
layout: default
title: "Horizon Summary: 2026-09-28 (EN)"
date: 2026-09-28
lang: en
---

> From 108 items, 3 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Cursor &\#x27;Loading chats&\#x27; hang caused by 52 GB state.vscdb](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Claude Code Effort Parameter Workflow](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Git worktrees isolate code but not runtime state for parallel agents](#item-ai-practitioner-3) ⭐️ 8.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Cursor &\#x27;Loading chats&\#x27; hang caused by 52 GB state.vscdb](https://www.reddit.com/r/cursor/comments/1wsihxw/cursor_stuck_on_loading_chats_after_reboot_root/) ⭐️ 8.0/10

Cursor IDE hung on &quot;Loading chats&quot; after a reboot. The root cause was a 52 GB \`state.vscdb\` SQLite file containing ~2.7 million rows in the \`cursorDiskKV\` table. Moving the database file aside restored instant performance. The issue persisted despite force-quits and relaunches, indicating local storage bloat rather than network or API failures.

reddit · r/cursor · /u/jasonlixuzhen · Sep 28, 15:58

**「Maintenance Action」** Prefer exporting chats, deleting large threads, and running garbage collection over raw SQL DELETE and VACUUM commands. VACUUM requires free space equal to the database size, which may be unavailable when the file is already bloated.

**「Evidence Details」** The \`cursorDiskKV\` table held 2,731,416 rows, while \`ItemTable\` had only 976 rows. Agent transcript JSONL files totaled 728 MB, confirming the database as the primary storage consumer. Restoring the old database later worked quickly, suggesting the failure mode is intermittent or dependent on cache initialization.

**Tags**: `#debugging`, `#ide-maintenance`, `#sqlite-bloat`, `#agent-state`, `#performance`

---

<a id="item-ai-practitioner-2"></a>
### [Claude Code Effort Parameter Workflow](https://www.reddit.com/r/ClaudeCode/comments/1wsbmp2/claude_code_official_docs_effort_with_opus_55_and/) ⭐️ 8.0/10

Anthropic documentation states that changing the &\#x27;effort&\#x27; level in Claude Code no longer breaks the prompt cache. Effort acts as a time budget where higher levels cause the model to test more, check its own work, and make more internal calls. Vague prompts benefit significantly from high effort, while detailed specs reduce the need for it. For example, a vague fitness app prompt took 1.5 minutes on low effort and 67 minutes on max, whereas a full spec yielded similar times across all levels. High effort catches missed edge cases but does not correct fundamental task misunderstandings.

reddit · r/ClaudeCode · /u/BuffaloConscious7919 · Sep 28, 11:06

**「Operator Takeaway」** Use the loop: interview and spec on low effort, build and iterate on low effort, then test and verify on high effort. Switch settings anytime using /effort.

**「Evidence and Limits」** Benchmark data comes from internal Anthropic runs with safety features off and five tries per task. Tasks were extreme, such as building a game console chip or writing formal math proofs. Results may not match public leaderboards. Security and hardware tasks showed large gains from increased effort, while rule-heavy admin work showed minimal movement.

**Tags**: `#agent-workflow`, `#cost-optimization`, `#prompt-engineering`, `#claude-code`

---

<a id="item-ai-practitioner-3"></a>
### [Git worktrees isolate code but not runtime state for parallel agents](https://www.reddit.com/r/ChatGPTCoding/comments/1wrvhfb/git_worktrees_solved_our_parallelagent_file/) ⭐️ 8.0/10

The author uses Git worktrees to prevent parallel coding agents from editing the same checkout. This isolation does not extend to runtime processes or data. Different worktrees can share APIs, databases, workers, storage services, and ports. Shared resources cause conflicts: frontend changes may rely on existing API contracts, experimental migrations risk shared data, and second workers against the same queue alter test results. The team treats four elements separately: the worktree code, the processes tests reach, the data those processes change, and post-merge checks. They maintain a small registry in Git&\#x27;s common directory to track which worktree started a service, including its PID, port, URL, and declared database state. Integration and browser QA tests start only the processes they need. Feature work runs in parallel; integration tests run serially on the combined tree.

reddit · r/ChatGPTCoding · /u/Jhon\_ST · Sep 27, 20:58

**「Actionable step」** Use Git worktrees for code isolation but implement a separate registry to track service PIDs, ports, and database states per worktree. Serialize integration and browser QA tests to ensure they exercise the correct API and data.

**「Limitations」** The registry helps with discovery and process checks but does not verify API compatibility. A healthy endpoint may still serve the wrong API version, and a free port is not necessarily reserved. The approach requires careful management of experimental migrations and shared queues.

**Tags**: `#agent-orchestration`, `#git-workflows`, `#test-environment-management`, `#parallel-development`

---