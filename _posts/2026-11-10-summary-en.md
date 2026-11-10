---
layout: default
title: "Horizon Summary: 2026-11-10 (EN)"
date: 2026-11-10
lang: en
---

> From 140 items, 6 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Modern Web Guidance skill raises agent pass rates from 55% to 92%](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Prevent agent-driven repo deletion with Bash $\{var:?\} guard](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Durable execution pattern for long-horizon agents](#item-ai-practitioner-3) ⭐️ 8.0/10
4. [Stronger models increase production fragility via over-engineering](#item-ai-practitioner-4) ⭐️ 8.0/10
5. [Codex loads AGENTS.md only at startup with root-down traversal and 32 KiB cap](#item-ai-practitioner-5) ⭐️ 8.0/10
6. [Locating the source of a mysterious beep with Claude](#item-ai-practitioner-6) ⭐️ 8.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Modern Web Guidance skill raises agent pass rates from 55% to 92%](https://github.com/GoogleChrome/modern-web-guidance) ⭐️ 8.0/10

Chrome released Modern Web Guidance, a curated RAG skill containing 200+ guides on modern web primitives like CSS.highlights and &lt;dialog&gt;. The package uses a ~7MB pure-JS index for ~10ms CPU search. A deterministic legacy-scan identifies outdated patterns with 92% precision. Evaluation across Codex, Claude, and Agy models on 1,700 assertions showed task pass rates increased from 55% unguided to 92% guided.

rss · Show HN \(10+ points\) · Nov 10, 18:01

**「Operator Takeaway」** Install the modern-web-guidance CLI to inject curated modern web primitive knowledge into coding agent contexts.

**「Evidence and Limits」** The 92% pass rate applies to the specific eval suite of ~1,700 Playwright/AST-based assertions. The legacy-scan precision metric comes from held-out repositories.

**Tags**: `#agent-context`, `#web-development`, `#rag-optimization`, `#evaluation-metrics`, `#prompt-engineering`

---

<a id="item-ai-practitioner-2"></a>
### [Prevent agent-driven repo deletion with Bash $\{var:?\} guard](https://www.reddit.com/r/ClaudeCode/comments/1xsp90d/at_546_am_i_get_anurgent_message_on_my_phone_from/) ⭐️ 8.0/10

An unset variable caused an agent-executed script to delete a repository root. The command \`find $tmp -delete\` ran with an empty \`$tmp\`, so \`find\` defaulted to the current directory. The operator recommends using \`$\{tmp:?temp path missing\}\` in shell expressions. This syntax rejects unset or empty variables before the command runs.

reddit · r/ClaudeCode · /u/ricopan · Nov 10, 15:07

**「Action」** Replace bare variable references in destructive agent-generated scripts with \`$\{var:?error\}\` syntax to enforce non-empty checks.

**「Limitations」** This guard only prevents empty-path errors. A nonempty variable can still point to the wrong directory. Operators should test cleanup wrappers by printing targets instead of deleting them, and keep backups outside the checkout.

**Tags**: `#agent-safety`, `#shell-scripting`, `#error-prevention`, `#workflow-hardening`, `#bash`

---

<a id="item-ai-practitioner-3"></a>
### [Durable execution pattern for long-horizon agents](https://martinfowler.com/articles/durable-execution-agents.html) ⭐️ 8.0/10

Long-horizon agents automate tasks spanning days or weeks, such as stock replenishment involving manager approvals and supplier deliveries. These agents use an &\#x27;agentic loop&\#x27; where a model selects tools based on current state and goals. Durable execution runtimes like Temporal or Cloudflare Durable Objects manage this loop by logging each step&\#x27;s result. If a failure occurs, the runtime replays the log to rebuild state, skipping completed steps. The architecture separates entity workflows \(long-lived, e.g., one per SKU\) from process workflows \(short-lived, e.g., one replenishment\). Entity workflows handle external messages and trigger process workflows. Waiting primitives suspend workflows without consuming CPU, with wake-up costs measured in milliseconds to seconds depending on log replay. Code changes require versioning business rules to handle parallel execution of old and new logic during deployment.

rss · Thoughtworks and Martin Fowler · Nov 10, 14:10

**「Operator Takeaway」** Decouple the agentic decision loop from state management by using durable execution runtimes. Implement entity workflows to manage long-lived context and route external signals to short-lived process workflows. Use wait primitives that suspend execution without holding compute resources to scale thousands of idle agents efficiently.

**「Evidence and Limits」** Wake-up performance varies by runtime: Temporal rebuilt workflows in under 0.1 seconds, while Cloudflare took about two seconds for log replay. Durable execution does not mitigate prompt injection risks; security relies on harness-level controls like restricted tool selection and validation of external inputs. Code deployments must account for how runtimes handle log replay with changed logic, requiring strategies like Parallel Change to version business rules.

**Tags**: `#agent-architecture`, `#durable-execution`, `#workflow-management`, `#long-horizon-agents`, `#system-design`

---

<a id="item-ai-practitioner-4"></a>
### [Stronger models increase production fragility via over-engineering](https://www.reddit.com/r/ChatGPTCoding/comments/1xsnddb/the_models_are_much_stronger_now_but_im_hitting/) ⭐️ 8.0/10

The author reports more production bugs with stronger AI models despite extensive code review. Strong models add layers of defense during review cycles, increasing system complexity and failure points. A specific case involved stacked database triggers that passed local tests but failed to compile in production due to nesting limits. The author attributes this to review processes checking code correctness without seeing production environment constraints or real user behavior.

reddit · r/ChatGPTCoding · /u/moutsea · Nov 10, 13:49

**「Operator Takeaway」** Replace implicit logic with explicit transactions. Run production-environment compile checks \(such as EXPLAIN on SQL templates\) before release. Execute one complete end-to-end flow test from the first request to the final result.

**「Evidence and Limits」** The evidence comes from a single practitioner&\#x27;s postmortem of a payment auto-provisioning feature. The production environment used Cloudflare D1, which has specific trigger depth limits not present in the local test environment. The author notes that older, weaker models produced simpler code with fewer failure points.

**Tags**: `#agent-workflow`, `#testing-strategy`, `#production-debugging`, `#code-review`, `#system-reliability`

---

<a id="item-ai-practitioner-5"></a>
### [Codex loads AGENTS.md only at startup with root-down traversal and 32 KiB cap](https://www.reddit.com/r/codex/comments/1xsdy0g/agentsmd_in_codex_has_no_ondemand_part_the_whole/) ⭐️ 8.0/10

Codex builds the context chain once at startup. It loads the user file first, then one AGENTS.md file per folder from the repo root down to the launch directory. Folders below the launch directory do not load. The total size of project files shares a \`project\_doc\_max\_bytes\` cap of 32 KiB by default. Codex stops adding files once the total reaches this limit. Because files load root-first, files closest to the work are dropped if the cap is hit. Edits to AGENTS.md do not apply until restart.

reddit · r/codex · /u/MinniLabs · Nov 10, 04:46

**「Workflow adjustment」** Keep the root AGENTS.md minimal. Place folder-specific rules in that folder’s own AGENTS.md file. Launch Codex from the relevant subdirectory to ensure those rules load.

**「Constraints and scope」** The 32 KiB cap applies to the sum of all loaded project files. A long root AGENTS.md consumes this cap and transmits with every turn. This report is based on integrating Codex support into MinniMemoryMCP.

**Tags**: `#context-management`, `#agent-configuration`, `#codex`, `#workflow-optimization`, `#prompt-engineering`

---

<a id="item-ai-practitioner-6"></a>
### [Locating the source of a mysterious beep with Claude](https://simonwillison.net/2026/Nov/9/mysterious-beeps/) ⭐️ 8.0/10

Simon Willison used Claude Code to build &quot;Beep Locator,&quot; a system that triangulates sound sources using multiple web-connected devices. He prompted Claude to create a Python web server and client-side JavaScript listeners using WebAudio and WebSockets. The system records audio buffers, detects beeps via FFT, and aligns clips using chirps to estimate location. Willison iteratively added features like &quot;Rough mode&quot; for manual device placement, clap testing, and hot-swappable JavaScript modules to avoid microphone permission prompts on reload. The system located an ancient carbon monoxide detector within 40cm.

rss · Simon Willison - Coding Agents · Nov 9, 23:57

**「Operator Takeaway」** Implement hot-swappable JavaScript modules over WebSockets to update agent-controlled browser listeners without triggering repeated microphone permission prompts.

**「Evidence and Limits」** The automatic acoustic ranging between devices did not work well, requiring a manual &quot;Rough mode&quot; for initial positioning. The final accuracy was approximately 40cm. The project relied on Opus 5.5 and Fable 5.2 models.

**Tags**: `#agent-workflow`, `#physical-computing`, `#webaudio`, `#iterative-prompting`, `#debugging`

---