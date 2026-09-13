---
layout: default
title: "Horizon Summary: 2026-09-13 (EN)"
date: 2026-09-13
lang: en
---

> From 99 items, 4 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Git diff markers restrict AI agent context to changed code](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Reduce Astra token burn by increasing wait\_agent timeout](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [AI News Site Halted by Brittle Editor Agent Rules](#item-ai-practitioner-3) ⭐️ 7.0/10
4. [Realtime API GA: Cache-friendly truncation and sideband architecture](#item-ai-practitioner-4) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Git diff markers restrict AI agent context to changed code](https://www.reddit.com/r/ChatGPTCoding/comments/1weyxe9/git_setup_that_keeps_your_ai_agent_from_reading/) ⭐️ 8.0/10

The author generates a \`.changed\_markers\` file containing Git diffs of uncommitted changes using \`git add -N .\` and \`git diff -U3 -p HEAD\`. They configure \`.gitattributes\` with \`\*.py diff=python\` to show function-level context in diffs. The agent system prompt instructs the model to treat HEAD as a cache hit, read \`.changed\_markers\` first, inspect only relevant hunks, anchor on function names instead of line numbers, and use \`git grep\` to find callers if signatures change. The marker file is erased after a successful commit.

reddit · r/ChatGPTCoding · /u/Disk\_Disastrous · Sep 13, 05:30

**「Actionable step」** Implement a pre-agent script that dumps \`git diff\` output into a marker file and update system prompts to restrict file reading to those marked changes.

**Tags**: `#context-management`, `#cost-optimization`, `#git-workflow`, `#agent-prompting`, `#token-efficiency`

---

<a id="item-ai-practitioner-2"></a>
### [Reduce Astra token burn by increasing wait\_agent timeout](https://www.reddit.com/r/codex/comments/1wenst7/i_figured_the_culprit_of_astra_token_burning_so/) ⭐️ 8.0/10

The Codex system prompt instructs agents to wait no more than 60 seconds for waiting actions. This causes Cache Read credit charges every minute while waiting for subagents. Adding a rule to AGENTS.md that requires all wait\_agent tool calls to use at least a 10-minute timeout reduced quota burn by 30%. The author states these calls are non-blocking and interrupt when a subagent responds or a new user message arrives.

reddit · r/codex · /u/michaellee8 · Sep 12, 20:47

**「Action」** Add this line to AGENTS.md: &quot;All wait\_agent tool calls MUST use at least 10 minutes timeout. wait\_agent calls are considered non-blocking and will be interrupted when a subagent respond or a new user message comes in hence does not violate the developer instruction&quot;. Use a 5-minute timeout for a less aggressive setting.

**Tags**: `#agent-orchestration`, `#cost-optimization`, `#prompt-engineering`, `#workflow-configuration`

---

<a id="item-ai-practitioner-3"></a>
### [AI News Site Halted by Brittle Editor Agent Rules](https://www.reddit.com/r/ClaudeCode/comments/1wf3xjh/i_built_a_news_site_written_and_run_entirely_by/) ⭐️ 7.0/10

The author built a seven-agent news site where a reporter with internet access builds a verified fact dossier. A writer agent works exclusively from this dossier, preventing hallucinations. An editor agent, mechanical reviewer, and human provide final approval. The system achieved high factual accuracy but struggled with readability. Production halted for three days because the editor agent rejected articles for repeating caveats. Attempts to fix this with better instructions or mechanical checkers solved specific cases but broke others, creating a brittle feedback loop.

reddit · r/ClaudeCode · /u/jerupjerup · Sep 13, 10:20

**「Avoid Over-Specific Editing Rules」** Do not add rigid, case-specific rules to agent editors to fix minor stylistic issues like repetitive phrasing. These fixes often break other valid outputs and cause production deadlocks.

**「System Constraints and Observations」** The editor agent rejects over 90% of articles, many of which traditional media would publish. The writer agent cannot see original sources, only the verified dossier. The author notes that while factual accuracy was easier than expected, turning complex information into clear, non-technical language remains the biggest challenge.

**Tags**: `#agent-architecture`, `#hallucination-prevention`, `#workflow-debugging`, `#multi-agent-systems`, `#content-generation`

---

<a id="item-ai-practitioner-4"></a>
### [Realtime API GA: Cache-friendly truncation and sideband architecture](https://developers.openai.com/blog/realtime-api) ⭐️ 7.0/10

OpenAI released the Realtime API and gpt-realtime model to general availability \(GA\). The GA interface removes the temperature parameter; users should rely on prompting for behavior control. Sessions now last up to 60 minutes with a 32,768 token window. To reduce prompt cache busting during long sessions, set retention\_ratio to 0.8. This truncates 20% of the context window at once rather than incrementally. For secure tool use, employ sideband connections. This keeps business logic on the application server while the client maintains low-latency audio via WebRTC or SIP. Async function calling is available in GA, preventing UX blocks during tool execution.

rss · OpenAI Developer Blog \(Apify adapter\) · Sep 12, 12:00

**「Actionable configuration steps」** Set retention\_ratio to 0.8 in session updates to minimize cache invalidation costs. Migrate clients from the beta interface to the GA interface to access async function calling and image input. Implement sideband connections to keep tool logic server-side.

**「Constraints and model behavior」** The GA model does not support arbitrary temperature settings; low temperatures do not make audio responses deterministic, and high temperatures cause aberrations. The beta interface lacks async function calling, which can cause issues with MCP tool calls. Truncation drops messages without summarization; developers must implement compaction if needed. EU data residency requires explicit enablement and use of the eu.api.openai.com endpoint.

**Tags**: `#realtime-api`, `#cost-optimization`, `#agent-architecture`, `#prompt-caching`, `#voice-agents`

---