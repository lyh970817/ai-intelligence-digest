---
layout: default
title: "Horizon Summary: 2026-10-20 (EN)"
date: 2026-10-20
lang: en
---

> From 129 items, 6 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Tune Decision Model Thresholds for Evals](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Grok Bot Token Costs Driven by Context Re-reading in Multi-Agent Handoffs](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [High baseline variance invalidates single-run token optimizer benchmarks](#item-ai-practitioner-3) ⭐️ 8.0/10
4. [Tune Codex subagents by model strength and reasoning effort](#item-ai-practitioner-4) ⭐️ 8.0/10
5. [Claude Code deletes local session history after 30 days by default](#item-ai-practitioner-5) ⭐️ 7.0/10
6. [LLM Prompt Regression Testing with Static Eval Sets](#item-ai-practitioner-6) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Tune Decision Model Thresholds for Evals](https://hamel.dev/blog/posts/decision-model-evals/) ⭐️ 8.0/10

Decision models return failure probabilities but use a default 0.50 threshold to classify traces as pass or fail. Using this default without checking it against labeled data yields subpar results. Tuning the threshold on saved scores improves F1 scores by balancing precision and recall based on business needs. The author tested Jev, Perplexity Decider, Liquid d1, Cloudflare Clef, and OpenAI Decisions on 100 apartment leasing agent traces. OpenAI separated classes best with an F1 of 0.87 after tuning, while Perplexity was cheapest at 0.82 cents per 100 runs with an F1 of 0.79. Calibration checks determine if model scores reflect true failure probabilities.

rss · Hamel Husain · Oct 20, 07:00

**「Prompt Agent to Tune Thresholds」** Ask a coding agent to tune decision thresholds using saved model scores and binary labels. Require stratified five-fold cross-validation to maximize F1 while enforcing minimum precision and recall constraints \(e.g., 80%\). Reuse saved scores to avoid new model calls.

**「Test Constraints and Limitations」** The test used 100 traces from a single domain \(apartment leasing\). Latency was excluded from the comparison because it depends on batching, concurrency, and infrastructure distance. Minimum precision and recall requirements were not met in 36 of 100 training splits for Perplexity and 29 for Liquid d1-ultra. Calibration adjustments used Platt scaling on a small sample and do not guarantee improvement on new data.

**Tags**: `#automated-evals`, `#decision-thresholds`, `#model-comparison`, `#cost-optimization`, `#agent-workflow`

---

<a id="item-ai-practitioner-2"></a>
### [Grok Bot Token Costs Driven by Context Re-reading in Multi-Agent Handoffs](https://www.reddit.com/r/cursor/comments/1xaki84/i_traced_where_my_grok_bot_tokens_were_going_the/) ⭐️ 8.0/10

A trace of Grok Bot usage over one day \(75.35 million tokens\) shows that 93.8% of tokens were cache reads, while only 1.06% were output. In a single hour-long session where bots coordinated and handed off jobs, 13.19 million tokens were consumed. Each handoff cost a median of 977k tokens because the receiving bot re-read its entire conversation history, and the coordinator re-read everything again upon reply. One worker with 303k tokens of context accounted for 4.24 million tokens in that hour. The author attributes this to stateless models requiring full context re-ingestion for every call.

reddit · r/cursor · /u/AdithyaBandara · Oct 20, 06:16

**「Operator Takeaway」** Assign each task to a fresh worker and keep one task per chat to minimize context re-ingestion during handoffs.

**「Evidence and Limits」** The export does not name specific bots or models, so classifications like &\#x27;background workers&\#x27; are heuristic. Per-handoff token counts are estimates pieced together from timing, cache chains, and file timestamps. The author cannot convert token types into exact costs because Grok Bot does not publish how each type weights against plan limits. The tracing tools mentioned \(Langfuse, Braintrust\) cannot see inside Grok Bot&\#x27;s own model calls.

**Tags**: `#agent-cost-optimization`, `#context-management`, `#llm-observability`, `#multi-agent-patterns`

---

<a id="item-ai-practitioner-3"></a>
### [High baseline variance invalidates single-run token optimizer benchmarks](https://www.reddit.com/r/codex/comments/1xagvzo/i_tested_15_ai_coding_token_optimizers_the/) ⭐️ 8.0/10

The author tested 15 token optimizers across 3 coding agents \(Claude Code, Codex, OpenCode\) and 2 open-source projects using real bug-fixing tasks. Baseline token usage varied by 54.5% across repeated runs without any optimizer. Four out of five apparent savings disappeared on retest. Only 9 of 79 configurations showed savings that held up under repeat-run screening. Results did not transfer across projects; every passing saving came from the same codebase. The same optimizer saved tokens with one agent but increased costs with another.

reddit · r/codex · /u/Middle\_Key8737 · Oct 20, 02:55

**「Action」** Use repeated-run screening and cross-project validation before adopting token-saving tools. Do not trust single-shot savings claims.

**「Evidence and limits」** The study used actual bug-fixing tasks rather than synthetic prompts. No optimizer makers sponsored the study. The author notes that some optimizers showed substantial savings, but evaluating them is difficult due to baseline instability.

**Tags**: `#cost-optimization`, `#evaluation-methodology`, `#agent-testing`, `#token-usage`, `#benchmarking`

---

<a id="item-ai-practitioner-4"></a>
### [Tune Codex subagents by model strength and reasoning effort](https://www.reddit.com/r/ChatGPTCoding/comments/1x9za9w/how_im_tuning_codex_subagents_to_manage_token/) ⭐️ 8.0/10

The author assigns specific model strengths and reasoning efforts to five agent roles to manage token usage. The Main thread uses a stronger model with high reasoning effort for architecture, planning, and final decisions. The Explorer uses a lightweight model with low reasoning effort for file discovery and dependency mapping. The Implementer uses a stronger model with medium effort for bounded changes with explicit acceptance criteria. The Reviewer and Diagnostician both use stronger models with high effort for independent correctness review and investigating difficult failures. The author uses AGENTS.md to establish delegation rules and avoids spawning agents for tasks resolvable by a single search. They also delegate suitable coding tasks to Cursor Agent CLI via shell invocation to distribute usage across existing subscriptions.

reddit · r/ChatGPTCoding · /u/Unixwzrd · Oct 19, 15:03

**「Operator Takeaway」** Assign lighter models and lower reasoning effort to exploration tasks, and reserve stronger models with high effort for planning, implementation, review, and diagnostics.

**「Evidence and Limits」** The author has not run a controlled benchmark and does not claim a specific percentage of token savings. The approach relies on defining objectives, constraints, and acceptance criteria before implementation to prevent architectural drift.

**Tags**: `#agent-orchestration`, `#cost-optimization`, `#prompt-engineering`, `#workflow-design`

---

<a id="item-ai-practitioner-5"></a>
### [Claude Code deletes local session history after 30 days by default](https://www.reddit.com/r/ClaudeCode/comments/1xaejai/psa_claude_code_deletes_your_local_session/) ⭐️ 7.0/10

Claude Code deletes local sessions after 30 days by default. Add &quot;cleanupPeriodDays&quot;: 36500 to ~/.claude/settings.json to extend retention. Avoid setting the value to 0.

reddit · r/ClaudeCode · /u/M5\_Maxxx · Oct 20, 01:01

**「Update settings.json to preserve history」** Add &quot;cleanupPeriodDays&quot;: 36500 to ~/.claude/settings.json to prevent automatic deletion of local session history.

**「Recovery limits and data completeness」** Deleted replies may not be recoverable. The file ~/.claude/history.jsonl may retain prompts but not Claude&\#x27;s replies. Time Machine backups can restore data if active.

**Tags**: `#agent-configuration`, `#context-management`, `#claude-code`, `#workflow-optimization`

---

<a id="item-ai-practitioner-6"></a>
### [LLM Prompt Regression Testing with Static Eval Sets](https://3anddoneapp.com/try) ⭐️ 7.0/10

The developer built a task management app using Anthropic models for ranking, suggestion generation, and task extraction. To maintain output quality, they created static eval sets containing constructed task lists and expected top-three outputs. They store these eval outputs and re-run tests whenever they modify a prompt rule or test a new model version. This process catches regressions and helps distinguish between prompt tuning needs and errors in the developer&\#x27;s own ranking logic.

rss · Show HN \(10+ points\) · Oct 19, 13:07

**「Actionable Step」** Create static eval sets with expected inputs and outputs for your LLM features. Re-run these tests automatically after every prompt change or model update to detect regressions.

**Tags**: `#LLM evaluation`, `#prompt engineering`, `#workflow automation`, `#regression testing`, `#agent development`

---