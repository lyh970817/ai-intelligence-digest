---
layout: default
title: "Horizon Summary: 2026-09-10 (EN)"
date: 2026-09-10
lang: en
---

> From 118 items, 4 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Structured tickets drive high agent PR merge rates](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [GPT-6 Astra quota burn rate exceeds GPT-5.6 Sol due to cache TTL and client bugs](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Autoprompt skill raises DeepSeek V4 Flash Terminal-Bench score to 82.02%](#item-ai-practitioner-3) ⭐️ 8.0/10
4. [Realtime API GA: Context Truncation and Sideband Patterns](#item-ai-practitioner-4) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Structured tickets drive high agent PR merge rates](https://www.reddit.com/r/ChatGPTCoding/comments/1wcnkuo/my_wife_used_to_send_me_every_small_fix_for_our/) ⭐️ 8.0/10

The author built an agent that reads Linear tickets and opens GitHub PRs. The workflow requires a strict ticket structure: a title describing the behavior change, 2-4 sentences of context naming relevant files, checkable acceptance criteria, and constraints on reuse and scope. This approach yielded 52 merged PRs out of 56 for the marketplace app and 237 merged out of 250 for the author&\#x27;s backlog. The author states that ticket quality matters more than model choice, noting that rejected PRs usually resulted from asking for the wrong thing rather than agent error.

reddit · r/ChatGPTCoding · /u/rathcom · Sep 10, 16:10

**「Enforce structured ticket fields」** Require agents to consume tickets with four specific fields: behavior-focused title, brief context with file names, checkable acceptance criteria, and explicit constraints. Do not rely on model capability to infer scope from vague requests.

**「Operational constraints」** The system only works with Linear and GitHub Issues. The author does not allow the agent to merge its own PRs; human review and merging remain required. Initial performance may be lower than the reported merge rates during the first week. The tool runs on existing Claude or ChatGPT subscriptions to avoid duplicate token costs.

**Tags**: `#agent-workflow`, `#prompt-engineering`, `#task-scoping`, `#code-review`, `#productivity`

---

<a id="item-ai-practitioner-2"></a>
### [GPT-6 Astra quota burn rate exceeds GPT-5.6 Sol due to cache TTL and client bugs](https://www.reddit.com/r/codex/comments/1wciwc1/gpt6_astra_burns_quota_4_times_faster_than_gpt56/) ⭐️ 8.0/10

The author measured a drop in weekly API-equivalent allowance from $2,500+ with GPT-5.6 Sol to about $1,200 with GPT-6 Astra on two Pro 20x accounts. This reduction persists after accounting for Astra&\#x27;s higher API prices. The primary drivers are a cache-retention TTL decrease from 24 hours \(Sol\) to 30 minutes \(Astra\) and Codex client bugs that break cache reuse during forks, subagents, and reasoning effort changes. These failures force repeated processing of conversation history, which constitutes the majority of priced usage in long agentic workloads. Additionally, Astra performs wasteful subagent polling, consuming millions of input tokens on empty checks.

reddit · r/codex · /u/Frequent-Goal4901 · Sep 10, 13:14

**「Operational adjustments」** Avoid using GPT-6 Astra for long-context agentic loops unless cache behavior is strictly managed. Prefer clients like Claude Code that preserve cache prefixes during forks and subagent tasks. Test higher reasoning effort settings \(e.g., XHigh\) to reduce total token burn by avoiding cache-miss penalties associated with lower effort retries. Monitor DevTools or use tools like CodexBar to track API-equivalent spend rather than raw token counts.

**「Measurement methodology and scope」** The author calculated costs by pricing input, cached input, and output tokens at published API rates. Results were cross-checked using CodexBar, Tokscale, T3 Code, and manual DevTools inspection of daily-workspace-usage-counts. The report covers only Codex Desktop and CLI environments with default settings. It does not evaluate direct API usage where cache preservation may differ. The author notes that OpenAI&\#x27;s subscription page claims half the messages, but observed usage value is closer to a quarter.

**Tags**: `#cost-optimization`, `#cache-management`, `#model-comparison`, `#agent-workflows`, `#field-report`

---

<a id="item-ai-practitioner-3"></a>
### [Autoprompt skill raises DeepSeek V4 Flash Terminal-Bench score to 82.02%](https://www.reddit.com/r/ClaudeCode/comments/1wc2bz9/a_claude_code_skill_pushed_dsv4flash_from_6742_to/) ⭐️ 8.0/10

The Autoprompt skill runs a plan → build → test → review → repair loop from one prompt. This self-reviewing loop &quot;rinses out its own mistakes.&quot; In a v1.0 Terminal-Bench 2.1 run using OpenCode, DeepSeek V4 Flash 0731 scored 67.42% without the skill and 82.02% with it. The author states this represents 45% fewer failed tasks. The tradeoff is longer runs and higher token costs. The skill is maintained as free, open-source software for Claude Code.

reddit · r/ClaudeCode · /u/Sorosu · Sep 9, 23:41

**「Action」** Adopt the Autoprompt skill or adapt its plan-build-test-review-repair loop to reduce agent failure rates, accepting higher token costs and longer execution times.

**「Limits」** The report covers a single benchmark \(Terminal-Bench 2.1\) and one model version \(DeepSeek V4 Flash 0731\). Results rely on the author&\#x27;s v1.0 run; no independent verification or community comments are provided.

**Tags**: `#agent-workflows`, `#self-correction`, `#model-evaluation`, `#prompt-engineering`, `#reliability`

---

<a id="item-ai-practitioner-4"></a>
### [Realtime API GA: Context Truncation and Sideband Patterns](https://developers.openai.com/blog/realtime-api) ⭐️ 7.0/10

OpenAI released the Realtime API and gpt-realtime model to general availability \(GA\). The GA interface removes the temperature parameter, as low temperatures do not make audio responses deterministic and high temperatures cause aberrations. Sessions now last up to 60 minutes with a 32,768 token window. To reduce prompt cache busting during automatic truncation, set retention\_ratio to 0.8. This truncates 20% of the context window at once rather than incrementally. Use sideband connections to keep business logic and tool use on your application server while the client handles audio streams via WebRTC or SIP. Migrate from the beta interface to GA to access features like async function calling and image input.

rss · OpenAI Developer Blog \(Apify adapter\) · Sep 12, 12:00

**「Actionable Configuration Steps」** Set retention\_ratio to 0.8 in session updates to optimize prompt caching costs during long conversations. Route tool execution and business logic through a server-side sideband connection instead of the client. Update prompts to use specific instructions, as the new model follows them strictly.

**「Feature Availability and Constraints」** Async function calling is available only on the GA model, not the beta model. EU data residency requires explicit enablement and use of the eu.api.openai.com endpoint. The beta interface will eventually be deprecated. Prompt caching does not summarize dropped messages; it only caches identical prefix content.

**Tags**: `#Realtime API`, `#Context Management`, `#Cost Optimization`, `#Voice Agents`, `#System Architecture`

---