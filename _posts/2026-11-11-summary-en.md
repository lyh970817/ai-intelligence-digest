---
layout: default
title: "Horizon Summary: 2026-11-11 (EN)"
date: 2026-11-11
lang: en
---

> From 131 items, 5 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Tests as data: ensuring AI-generated code does what we want](#item-ai-practitioner-1) ⭐️ 9.0/10
2. [Cheap-builder / frontier-reviewer loop cuts cost to 1/16th with comparable pass rates](#item-ai-practitioner-2) ⭐️ 9.0/10
3. [Opus 5.5 API output tokens increased ~60% since mid-October](#item-ai-practitioner-3) ⭐️ 8.0/10
4. [Build a 24/7 Super-agent with Router-Worker Architecture](#item-ai-practitioner-4) ⭐️ 8.0/10
5. [Modern Web Guidance skill raises agent pass rates from 55% to 92%](#item-ai-practitioner-5) ⭐️ 8.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Tests as data: ensuring AI-generated code does what we want](https://martinfowler.com/articles/tests-as-data.html) ⭐️ 9.0/10

Martin Fowler argues that developers lose trust in AI-generated tests because agents refactor both production and test code, making it hard to verify behavior. He proposes treating tests as data—using tables, domain-specific languages \(DSLs\), or approved files—rather than code. This separates the functional contract \(data\) from the execution logic \(runner\). AI can cheaply build and maintain the runners, while humans review the readable data files. This approach draws on Specification by Example, Go-style tabular tests, and Approval Testing to create black-box tests that resist refactoring and remain trustworthy.

rss · Thoughtworks and Martin Fowler · Nov 11, 15:17

**「Operator Takeaway」** Direct coding agents to generate test data files \(tables, DSLs, or approved outputs\) instead of test code. Use the agent to write the small test runner that interprets these files. Review the data files as the primary contract for system behavior.

**「Evidence and Limits」** The proposal is based on interviews with 26 developers who reported distrusting AI-refactored tests. The author notes this approach is not suitable for early prototypes where speed matters more than stability. It also requires extra work to ensure the DSL and runner are correct. Human exploratory testing and other techniques like property-based testing remain necessary for full assurance.

**Tags**: `#ai-testing-strategy`, `#agent-workflow`, `#test-architecture`, `#specification-by-example`, `#software-quality`

---

<a id="item-ai-practitioner-2"></a>
### [Cheap-builder / frontier-reviewer loop cuts cost to 1/16th with comparable pass rates](https://www.reddit.com/r/ChatGPTCoding/comments/1xthm3v/i_tested_a_cheapbuilder_frontierreviewer_loop_on/) ⭐️ 9.0/10

The author tested a &quot;Krystal Loop Protocol&quot; on 66 hidden-test tasks from CooperBench. A cheap model \(deepseek-flash\) writes code in a sandbox. Tests run against the change. A frontier model from a different family \(gpt-6.1-sol\) reviews only the diff, task, and test output. The reviewer must write a failing test to prove a bug; if the test passes, the complaint is discarded. Fixes iterate until clean or a limit is hit. The loop solved 54–59 tasks at $0.046–$0.061 per task. Gpt-6-astra alone solved 56 tasks at $0.721. Gpt-6.1-sol alone solved 56 tasks at $0.123. Deepseek-flash alone solved 54–57 tasks at $0.014–$0.027. The review step added 0–2 solved tasks but caught 70–77 real bugs. In merge conflict tests, the loop resolved 28 of 30 pairs at ~$0.10 per pair, while a single frontier model resolved 22 at $0.196.

reddit · r/ChatGPTCoding · /u/KrystalUnity · Nov 11, 13:22

**「Actionable step」** Route cheap models for code generation and reserve frontier models for test-gated review of diffs to reduce cost per task while maintaining pass rates.

**「Scope and constraints」** Results are based on 66 tasks. The author notes the sample size may be insufficient for definitive claims. The builder was not tested with local models. The reviewer must be from a different model family to ensure independent judgment. The method relies on the existence of automated tests to gate fixes.

**Tags**: `#agent-orchestration`, `#cost-optimization`, `#model-routing`, `#testing-strategy`, `#code-review`

---

<a id="item-ai-practitioner-3"></a>
### [Opus 5.5 API output tokens increased ~60% since mid-October](https://www.reddit.com/r/ClaudeCode/comments/1xtlc9v/opus_55_on_the_api_same_prompts_same_settings_60/) ⭐️ 8.0/10

A practitioner reports that Claude Opus 5.5 output tokens per input token rose from ~0.69 \(Sep 21–Oct 11\) to ~1.09 \(since Oct 12\), a ~60% increase. Prompts, model ID, and effort settings remained unchanged. Weekly spend increased from $86 to $119 due entirely to higher output volume. Local transcripts show output per turn grew from ~170 tokens on Opus 5 to ~1,300–1,700 on Opus 5.5. The author attributes this to hidden thinking tokens billed as output, noting Anthropic&\#x27;s recent announcement of fixes for issues that &quot;used more limits than intended.&quot;

reddit · r/ClaudeCode · /u/FlynancialAnalyst · Nov 11, 15:55

**「Audit output costs and constrain length」** Audit current API cost structures for Claude Opus 5.5 and implement stricter output length constraints or token budgets to prevent unexpected spend increases driven by higher verbosity.

**「Data source and limitations」** The finding relies on a single user&\#x27;s Console cost export and local transcripts. The author calculated output tokens using the formula: output $ ÷ input $ ÷ 5. The report notes that thinking tokens are billed as output but hidden by default, making it impossible to verify exactly what is being paid for. No community comments or additional tool results are available to corroborate the trend.

**Tags**: `#cost-control`, `#model-behavior`, `#api-optimization`, `#claude-opus`

---

<a id="item-ai-practitioner-4"></a>
### [Build a 24/7 Super-agent with Router-Worker Architecture](https://www.reddit.com/r/DeepSeek/comments/1xti382/from_architecture_to_product_building_a_247/) ⭐️ 8.0/10

The author built a 24/7 super-agent system in ten days based on the &quot;Exploring Super-agent Design&quot; article. The architecture decouples a cloud-based Router from local Worker agents. The Router handles task orchestration and connects to channels like IM and GitHub. Local Workers execute tasks in isolated environments. The author introduced a &quot;Task&quot; concept to manage workflows, keeping session details for tracing. The system uses an asynchronous ReAct loop, allowing the Router to dispatch messages without waiting for Worker completion. To connect local CLI agents \(such as Claude Code or Codex\) to the cloud Router, the author released Crewbot, an open-source daemon installed on each device.

reddit · r/DeepSeek · /u/Predream1 · Nov 11, 13:44

**「Actionable Step」** Install the Crewbot daemon on local devices to expose CLI agents as remote workers. Use this setup to dispatch tasks from a central Router while keeping execution and data local.

**「Constraints and Context」** The build relied on Fable 5.2 after earlier models \(Opus 5.5, Fable 5.1\) struggled with Router design logic. The system is described as a SaaS product with a free tier. The author notes that the Router does not need horizontal scaling for event routing based on the source article&\#x27;s claims.

**Tags**: `#agent-architecture`, `#workflow-orchestration`, `#asynchronous-agents`, `#multi-agent-systems`, `#context-management`

---

<a id="item-ai-practitioner-5"></a>
### [Modern Web Guidance skill raises agent pass rates from 55% to 92%](https://github.com/GoogleChrome/modern-web-guidance) ⭐️ 8.0/10

The Chrome team released Modern Web Guidance, a lightweight RAG-based skill that injects curated knowledge of modern web primitives into coding agents. The package contains 200+ guides \(~1.7MB\) and uses a pure-JS search index reduced from 500MB to ~7MB. A deterministic legacy-scan identifies outdated patterns with 92% precision. In evaluations against 1,700 assertions across 200 tasks, agents improved from a 55% pass rate unguided to 92% guided.

rss · Show HN \(10+ points\) · Nov 10, 18:01

**「Action」** Install the skill via \`npx modern-web-guidance@latest install\` and run \`npx modern-web-guidance@latest legacy-scan ./src\` to identify outdated patterns in your codebase.

**「Evidence and limits」** The evaluation covered codex, claude, and agy models. The 92% precision figure for the legacy-scan applies to held-out repositories. The pass rate improvement is based on Playwright/AST-based assertions.

**Tags**: `#agent-evaluation`, `#rag-optimization`, `#frontend-development`, `#context-management`, `#model-guidance`

---