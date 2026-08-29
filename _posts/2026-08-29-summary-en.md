---
layout: default
title: "Horizon Summary: 2026-08-29 (EN)"
date: 2026-08-29
lang: en
---

> From 121 items, 5 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Six Design Patterns for Efficient Agentic Graphs](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Codex + MCP workflow for large Unity projects](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Replace LLM memory with program analysis](#item-ai-practitioner-3) ⭐️ 8.0/10
4. [Claude Code Context Re-reads Dominate Token Usage and Cost](#item-ai-practitioner-4) ⭐️ 8.0/10
5. [DeepSeek API cache retention reduces reprocessing costs for long tool calls](#item-ai-practitioner-5) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Six Design Patterns for Efficient Agentic Graphs](https://www.reddit.com/r/ChatGPTCoding/comments/1w1n0l7/how_to_build_agentic_graphs/) ⭐️ 8.0/10

The author shares six lessons from four months of building agentic graphs. First, run dependent checks sequentially rather than in parallel to avoid cache invalidation and duplicated work when tasks loop back. Second, allow agents to escalate conflicting feedback to a human or manager agent instead of forcing them to resolve it autonomously, which prevents infinite loops. Third, offload static checks like linting and testing to script nodes so the LLM only processes relevant failures, saving tokens. Fourth, route tasks to cheaper models for simple roles like QA while reserving strong models for planning. Fifth, monitor context usage and preemptively compact sessions when thresholds are reached \(e.g., 71% for workflows\) to prevent costly cache misses. Sixth, ensure nodes are idempotent so that returning a task to a previous stage continues work from the current state rather than restarting from scratch.

reddit · r/ChatGPTCoding · /u/Nek\_12 · Aug 29, 13:46

**「Actionable Steps」** Enforce sequential dependencies for review stages, move static checks to script nodes, implement escalation paths for conflicting agent feedback, assign models based on task complexity, set up speculative compaction at ~71% context usage for workflows, and configure nodes to resume work rather than restart when receiving returned tasks.

**「Context and Constraints」** The author uses Kent, an open-source orchestrator, and notes that some features like native model routing per edge and continuation modes are specific to this tool. The compaction thresholds \(88% for regular sessions, 71% for workflows\) are heuristic values derived from the author&\#x27;s measurements. The advice applies to directed graphs with cycles, branches, and scripts.

**Tags**: `#agentic-workflows`, `#graph-design`, `#cost-optimization`, `#context-management`, `#workflow-patterns`

---

<a id="item-ai-practitioner-2"></a>
### [Codex + MCP workflow for large Unity projects](https://www.reddit.com/r/codex/comments/1w1jf2t/using_codex_mcp_directly_inside_a_large_unity/) ⭐️ 8.0/10

The author uses Codex connected to a Unity project via MCP to enable project-aware inspection and modification. The workflow avoids manual context pasting by asking Codex to inspect relevant systems before modifying files. Prompts focus on explaining execution paths and implementing the smallest possible change to preserve existing architecture. The author uses Codex to refactor duplicated logic, act as a &quot;code archaeologist&quot; to explain forgotten systems, and trace debugging paths across multiple scripts. Codex also builds Unity editor tools for bulk validation and content consistency checks. The author mandates self-verification prompts after implementation, such as inspecting affected call sites for regressions. Architecture-wide changes, save systems, and performance-sensitive loops require careful human review.

reddit · r/codex · /u/Suspicious\_Neck\_4069 · Aug 29, 10:53

**「Enforce inspect-before-modify and self-verification loops」** Require agents to inspect existing implementations and explain execution paths before generating code. After implementation, prompt the agent to inspect all affected call sites for regressions and duplicated logic.

**Tags**: `#agent-workflow`, `#context-management`, `#refactoring-strategy`, `#validation-tooling`, `#prompt-engineering`

---

<a id="item-ai-practitioner-3"></a>
### [Replace LLM memory with program analysis](https://pwning.systems/posts/llm-memory-program-analysis/) ⭐️ 8.0/10

The author replaces unreliable LLM memory with deterministic program analysis. The workflow extracts code into ASTs or graphs. This structured data handles complex reasoning tasks. The LLM focuses on translation and interpretation rather than logic retention.

hackernews · matt\_d · Aug 28, 23:27 · [Discussion](https://news.ycombinator.com/item?id=49485416)

**「Action」** Offload logic retention to formal structures like ASTs or graphs. Restrict the LLM to translating between natural language and these structured representations.

**「Community feedback」** Commenters corroborate the approach by placing LLMs only at the terminals of request fulfillment. One user applies this by converting requests to Datalog and interpreting results back to natural language. Another stores facts in a Postgres knowledge graph to avoid re-scraping. A critic notes that &\#x27;is\_a&\#x27; representations may eventually require quantifiers, referencing the historical complexity of Cyc.

**Tags**: `#agent-architecture`, `#program-analysis`, `#reliability-patterns`, `#structured-output`, `#workflow-design`

---

<a id="item-ai-practitioner-4"></a>
### [Claude Code Context Re-reads Dominate Token Usage and Cost](https://www.reddit.com/r/ClaudeCode/comments/1w15lg2/for_every_token_claude_code_writes_it_rereads_360/) ⭐️ 8.0/10

The author measured 34,215 API calls across 637 sessions. Context re-reads \(cache reads\) accounted for 98.5% of billed tokens. Cache writes were 1.2%. Model output was 0.3%. Fresh input rounded to 0.0%. This equals 360 tokens re-read for every token written. The per-session median was 97.6%, with the p10 at 91.2% and p90 at 99.1%. Weighted by relative price, re-read context comprised 77.3% of the cost. The usage block repeats identically on every line of the same API call, once per content block. Summing per line overcounts by 69% because there are 1.69 lines per call in this corpus.

reddit · r/ClaudeCode · /u/duqaxxx · Aug 28, 22:56

**「Deduplicate Logs by Request ID」** Deduplicate API usage logs by requestId to avoid a 69% overcounting error when analyzing session costs.

**「Data Scope and Unknowns」** The data comes from logs in ~/.claude/projects using an open-source tool. The author does not know whether subscription rate limits count tokens the same way.

**Tags**: `#cost-optimization`, `#agent-debugging`, `#context-management`, `#log-analysis`, `#claude-code`

---

<a id="item-ai-practitioner-5"></a>
### [DeepSeek API cache retention reduces reprocessing costs for long tool calls](https://www.reddit.com/r/DeepSeek/comments/1w1l2rp/thoughts_on_deepseek_api/) ⭐️ 7.0/10

The author reverted to DeepSeek API because its context cache retains data for about an hour. Competitors like Alibaba hold cache for only 5 minutes. When a tool call, such as code execution, exceeds the retention window, the system must reprocess the full context. This reprocessing incurs unseen inference costs that outweigh base token price differences. Long-running tool calls are common in LLM-driven development.

reddit · r/DeepSeek · /u/Interesting-Print366 · Aug 29, 12:19

**「Action」** Route coding agent tasks with expected tool call durations over 5 minutes to DeepSeek to avoid full-context reprocessing costs.

**「Limits」** The one-hour retention figure is based on the author&\#x27;s experience and may vary. The comparison specifically cites Alibaba&\#x27;s 5-minute window as a counterexample. The author notes disappointment with recent price increases but finds the caching advantage decisive.

**Tags**: `#model-routing`, `#cost-optimization`, `#context-caching`, `#agent-workflows`, `#deepseek`

---