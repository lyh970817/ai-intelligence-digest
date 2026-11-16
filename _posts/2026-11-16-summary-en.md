---
layout: default
title: "Horizon Summary: 2026-11-16 (EN)"
date: 2026-11-16
lang: en
---

> From 116 items, 5 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Cost and quality trade-offs for Opus-Haiku routing in code review and coding tasks](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Codex silently truncates AGENTS.md at 32 KiB](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Agent-written decision log replaces weekly status sync](#item-ai-practitioner-3) ⭐️ 8.0/10
4. [Investigator agents detect alignment eval tells](#item-ai-practitioner-4) ⭐️ 8.0/10
5. [Coral: Open-source gateway for agent-written TypeScript tools](#item-ai-practitioner-5) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Cost and quality trade-offs for Opus-Haiku routing in code review and coding tasks](https://www.reddit.com/r/ClaudeCode/comments/1xxyc5a/does_delegating_to_cheaper_models_actually_save/) ⭐️ 8.0/10

The author ran about 300 benchmarks on real open-source codebases to test how Claude Code splits work between models. On small jobs \(~10k lines\), delegating did not pay off; Forced Opus found more doc errors than delegated setups, likely because Opus reused cached context while subagents built their own. On larger codebases, Opus + Haiku cut costs by ~50% on large documentation reviews while improving error detection. On an 85-page docs check, Opus + Haiku read almost 3 times as much and wrote 8 times as many tokens as Opus alone, yet cost 53% less \($1.93 vs $4.11\) and found more real errors \(72 vs 49\). For coding tasks, Opus + Haiku saved 20-30% at the same quality. Haiku alone cost about 5% of Opus alone&\#x27;s price on well-defined tasks with tests, with almost the same results but less thoroughness. Left alone, Opus never delegated even on big jobs.

reddit · r/ClaudeCode · /u/BeginningSir7334 · Nov 16, 19:16

**「Routing strategy based on task type」** Use Opus + Haiku for large-scale reading and review tasks to leverage parallel coverage at lower cost. Use Haiku alone for small, well-defined coding tasks with tests to minimize overhead. Do not rely on spontaneous delegation; explicitly configure routing or force delegation for large reviews.

**「Limitations and context」** The study used mostly two runs per setup with costs estimated at API prices. Claude Opus wrote the tests and judged the results, so there was no independent judge. One apparent performance difference depended on the day the runs happened, not the model. The author notes that forcing Opus not to delegate may have pushed it to work harder, but has not tested which factor caused the result.

**Tags**: `#model-routing`, `#cost-optimization`, `#multi-agent-workflows`, `#benchmarking`, `#coding-agents`

---

<a id="item-ai-practitioner-2"></a>
### [Codex silently truncates AGENTS.md at 32 KiB](https://www.reddit.com/r/codex/comments/1xxx2lx/codex_silently_stops_loading_agentsmd_at_32_kib_i/) ⭐️ 8.0/10

Codex caps combined project instructions at 32 KiB by default. Content past this limit gets cut off without warning. The cap is shared across every AGENTS.md between the repo root and the working directory. A survey of 30 context files from top-starred repos found a median size of 1,034 tokens and a maximum of 6,249 tokens \(about 25 KB\). While the largest single file fits within the limit, monorepos with root and nested files could exceed the cap silently.

reddit · r/codex · /u/Tatachimcooky · Nov 16, 18:29

**「Action」** Monitor AGENTS.md file size to prevent silent rule loss. Use tooling like ctxcap to validate instruction integrity and track token growth in CI.

**「Limits」** The survey only counted repo roots, so it does not reflect how many real setups with nested files are near the cap. Token counts used gpt-tokenizer, which is probably closer to Codex than Claude-oriented counts but not exact.

**Tags**: `#context-management`, `#agent-debugging`, `#codex`, `#workflow-optimization`, `#failure-modes`

---

<a id="item-ai-practitioner-3"></a>
### [Agent-written decision log replaces weekly status sync](https://www.reddit.com/r/ChatGPTCoding/comments/1xxq9yb/i_killed_my_30minute_weekly_status_sync_with_a/) ⭐️ 8.0/10

The author replaced a 30-minute weekly status sync with a single-file decision log. The agent harness reads this file before every run. Each entry follows the format: Date - decision - tradeoff we accepted. The agent writes to the log at the end of each task while the decision is fresh. If a decision is in the log, the agent cannot re-decide it. If it is missing, the agent asks. This shifted meetings from reconstructing past decisions to checking new items.

reddit · r/ChatGPTCoding · /u/Humaux · Nov 16, 14:09

**「Actionable step」** Configure agents to append dated decisions and accepted tradeoffs to a shared log file immediately after completing each task. Instruct the agent harness to read this log before every run and forbid overriding logged decisions.

**「Constraints and failure modes」** The author found that manual updates failed because &\#x27;later never came,&\#x27; causing the log to go stale in a week. The system relies on the agent writing entries immediately post-task to maintain fidelity.

**Tags**: `#agent-context`, `#workflow-automation`, `#decision-logging`, `#prompt-engineering`

---

<a id="item-ai-practitioner-4"></a>
### [Investigator agents detect alignment eval tells](https://metr.org/notes/2026-11-16-measuring-alignment-eval-tells/) ⭐️ 8.0/10

METR researchers used investigator agents to identify environmental cues \(&\#x27;tells&\#x27;\) that distinguish alignment evaluations from capability tasks. The agents explored 55 environments \(36 capability, 19 alignment\) without attempting the core task, then estimated the probability the environment was an alignment eval. Opus 5.5 and Astra successfully discriminated between the two classes. Alignment evals scored higher than all capability evals in both direct questioning and open-ended analysis. Agents cited specific tells, including contrived scenarios, planted shortcuts, impossible honest success, and simulated infrastructure.

rss · METR · Nov 16, 08:00

**「Operator Takeaway」** Run investigator agents on your benchmark environments to detect &\#x27;tells&\#x27; like mocked services or contrived scenarios. Use their feedback to iterate on environment design and reduce obvious signs that the task is an alignment test rather than a real deployment scenario.

**「Evidence and Limits」** The study measured what agents can work out when explicitly asked to probe the environment, not what they notice while performing the task. The goal was to identify exists of tells, not to measure if these tells causally affect behavior during actual task execution. Some tells are intrinsic to alignment tasks \(e.g., conflicting goals\) and may be difficult to remove entirely.

**Tags**: `#evaluation-methodology`, `#benchmark-auditing`, `#agent-behavior`, `#prompt-engineering`

---

<a id="item-ai-practitioner-5"></a>
### [Coral: Open-source gateway for agent-written TypeScript tools](https://github.com/withcoral/coral) ⭐️ 7.0/10

Coral is an open-source, self-hosted gateway that sits between agents and target systems. Agents write short TypeScript programs to perform tasks and save successful steps as reusable custom tools. These tools appear in search alongside standard provider tools \(e.g., Datadog, Slack\) for reuse. Each program runs in a V8 isolate with no network access or credentials. Coral checks every tool call against workspace policy before attaching credentials and forwarding the request. The core is written in Rust and licensed under Apache 2.0.

rss · Show HN \(10+ points\) · Nov 16, 14:14

**「Operator Takeaway」** Evaluate Coral to enable agents to generate and cache TypeScript tools for repetitive workflows, aiming to reduce token costs and execution time while maintaining strict permission controls via V8 isolates and policy checks.

**「Evidence and Limits」** The author reports that custom tools helped agents work 29% faster at 31% lower cost on tasks across GitHub, Linear, and Slack using Opus 5.5. SAML, SCIM, and org-wide governance features are not yet available in the open-source edition; they will be released under an enterprise license.

**Tags**: `#agent-orchestration`, `#tool-use`, `#cost-optimization`, `#workflow-automation`, `#developer-tools`

---