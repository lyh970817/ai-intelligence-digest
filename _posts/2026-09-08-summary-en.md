---
layout: default
title: "Horizon Summary: 2026-09-08 (EN)"
date: 2026-09-08
lang: en
---

> From 123 items, 6 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Increase Astra wait\_agent timeout to stop quota burn](#item-ai-practitioner-1) ⭐️ 9.0/10
2. [Prioritize Verification and Decision History in AI Workflows](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Flash Vision outperforms V4 Pro in Terraria build via visual feedback loop](#item-ai-practitioner-3) ⭐️ 8.0/10
4. [Delegate reasoning to Fable 5.1 and coding to Sonnet 5 to conserve tokens](#item-ai-practitioner-4) ⭐️ 8.0/10
5. [Realtime API GA: Truncation, Sidebands, and Async Calls](#item-ai-practitioner-5) ⭐️ 7.0/10
6. [Agent testing failures and architectural constraints](#item-ai-practitioner-6) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Increase Astra wait\_agent timeout to stop quota burn](https://www.reddit.com/r/codex/comments/1wa9c9d/i_investigated_why_gpt6_astra_burns_quota_so_fast/) ⭐️ 9.0/10

GPT-6 Astra burned Codex limits fast because it woke up every 30 seconds to poll Luna workers. In one run, 47 empty polls consumed 7.13M parent input tokens, representing 68% of total parent-side input. This caused 5h usage to jump from 53% to 100% in ~33 minutes. The fix is to add \`\[features.multi\_agent\_v2\]\` with \`min\_wait\_timeout\_ms\`, \`default\_wait\_timeout\_ms\`, and \`max\_wait\_timeout\_ms\` set to 1500000 \(25 minutes\) in \`~/.codex/config.toml\`. This change eliminated the polling loop and kept the parent asleep until worker activity occurred.

reddit · r/codex · /u/tagorrr · Sep 8, 00:31

**「Action」** Add the following to \`~/.codex/config.toml\` to prevent busy-polling: 

\`\`\`toml
\[features.multi\_agent\_v2\]
enabled = true
min\_wait\_timeout\_ms = 1500000
default\_wait\_timeout\_ms = 1500000
max\_wait\_timeout\_ms = 1500000
\`\`\`

**「Evidence」** Telemetry showed each empty poll used ~151.7k input tokens. A control Luna Max session processed 9.54M input tokens over 127 minutes but only increased 5h usage by 8 percentage points, confirming the Astra parent&\#x27;s polling was the primary cost driver. The author submitted feedback and posted full telemetry on GitHub.

**Tags**: `#agent-orchestration`, `#cost-optimization`, `#token-efficiency`, `#configuration-tuning`, `#debugging`

---

<a id="item-ai-practitioner-2"></a>
### [Prioritize Verification and Decision History in AI Workflows](https://martinfowler.com/fragments/2026-09-08.html) ⭐️ 8.0/10

Practitioners argue that AI reduces generation costs but not verification costs, creating a risk of &\#x27;counterfeit utility&\#x27; where short-term metrics rise while long-term capability weakens. Christian Catalini advises building a history of decisions rather than a gallery of outputs to preserve human judgment. Jessica Kerr states that agents lack &\#x27;Verum Factum&\#x27; \(knowledge from making\) and must rely on &\#x27;Vexationes Artium&\#x27; \(rigorous testing\). She urges operators to increase objective verification by ten times. Brian Cantrill notes that readers detect and reject LLM-generated text due to lack of authenticity. Martin Fowler reports that unchecked model output can lead to systems that outgrow human understanding, requiring strict control over system size.

rss · Thoughtworks and Martin Fowler · Sep 8, 15:22

**「Operator Takeaway」** Double down on objective testing frameworks to verify agent output. Record the reasoning and decisions behind code changes, not just the final generated artifacts.

**「Evidence and Limits」** OpenAI reports that newer models like Astra are less monitorable, with shorter traces that can conceal behavior during adversarial tests. This limits the effectiveness of observation-based improvement cycles. The advice to increase verification assumes the existence of robust test suites; legacy code lacking testability poses a barrier to this approach.

**Tags**: `#agent-verification`, `#workflow-design`, `#technical-debt`, `#evaluation-strategy`, `#decision-history`

---

<a id="item-ai-practitioner-3"></a>
### [Flash Vision outperforms V4 Pro in Terraria build via visual feedback loop](https://www.reddit.com/r/DeepSeek/comments/1wamfuh/deepseek_v4_pro_vs_flash_vision_in_deepseek/) ⭐️ 8.0/10

The author ran the same Terraria-style game development prompt through DeepSeek Harness using two models: V4 Pro \(max effort\) and Flash Vision. Both runs took approximately 26.5 minutes with zero human intervention. V4 Pro followed a plan-first workflow, designing internally and writing code in one large pass without visually inspecting the rendered result. It validated logic via a simulated DOM test environment. This approach left visual and control problems, such as uncomfortable camera behavior and weak mining feedback. Flash Vision made more tool-call mistakes but repeatedly viewed browser screenshots and corrected the actual rendered output. This visual feedback loop fixed issues like background gaps and vertical camera drift. The resulting Flash Vision build was more playable and closer to the quality of a GPT-5.6 \(Codex\) build.

reddit · r/DeepSeek · /u/Logical\_Catch\_3207 · Sep 8, 12:01

**「Prioritize native vision for UI-heavy agent tasks」** Use models with native vision capabilities for tasks requiring visual verification, such as UI development or game builds. The ability to inspect screenshots and correct rendered output compensates for weaker planning depth and produces superior results compared to plan-only approaches that rely on simulated environments.

**「Scope and limitations of the field report」** This is a single-prompt comparison within the DeepSeek Harness environment. While Flash Vision produced a better game, it still had unresolved issues with block placement, combat animation, and item-drop feedback. The author notes this is a provisional field report and plans a separate breakdown of session logs, reasoning structure, and token usage.

**Tags**: `#agent-workflows`, `#model-comparison`, `#vision-feedback`, `#debugging-strategy`, `#ui-development`

---

<a id="item-ai-practitioner-4"></a>
### [Delegate reasoning to Fable 5.1 and coding to Sonnet 5 to conserve tokens](https://www.reddit.com/r/ClaudeCode/comments/1wa9aya/tired_of_people_complaining_about_usage_heres_a/) ⭐️ 8.0/10

The author uses the Max 20x plan to consume ~7.5B tokens weekly without hitting limits. They restrict Fable 5.1 to reasoning tasks only, using low effort settings and avoiding Ultracode to prevent spawning multiple agents. For actual code generation, they delegate to Sonnet 5, which has higher usage limits on their plan. The prompt instructs Fable to spell out all steps for Sonnet, forbidding Sonnet from thinking about implementation. Context management involves running /compact when windows exceed 50-60%, merging redundant skills, disabling unused MCP tools, and tagging Memory.md entries \(e.g., $temp\) for periodic cleanup.

reddit · r/ClaudeCode · /u/Emotional-Bus-7065 · Sep 8, 00:29

**「Actionable step」** Configure your agent to use a high-reasoning model for planning and a high-limit model for code execution, while actively pruning skills and tagging memory files to keep context windows below 60% capacity.

**「Constraints and scope」** This workflow relies on specific plan benefits \(Max 20x\) where Sonnet 5 has practically unlimited usage compared to Fable. The author notes that asking Claude to merge skills can yield poor results as it may delete random content. Haiku is discouraged for complex tasks. The advice applies to a coding workflow involving website building and bug fixing.

**Tags**: `#cost-optimization`, `#agent-orchestration`, `#context-management`, `#model-routing`, `#workflow-efficiency`

---

<a id="item-ai-practitioner-5"></a>
### [Realtime API GA: Truncation, Sidebands, and Async Calls](https://developers.openai.com/blog/realtime-api) ⭐️ 7.0/10

OpenAI released the Realtime API and gpt-realtime model to general availability \(GA\). The GA interface removes the temperature parameter; users should rely on prompting for behavior control. Sessions now last up to 60 minutes with a 32,768 token window. To reduce prompt cache busting costs during truncation, set retention\_ratio to 0.8. This truncates 20% of the context window at once rather than incrementally. Use sideband connections to keep business logic and tool use on the application server while the client handles audio. Async function calling is now supported in GA, preventing model hallucinations during pending tool calls via automatic placeholder responses.

rss · OpenAI Developer Blog \(Apify adapter\) · Sep 12, 12:00

**「Actionable Configuration Steps」** Migrate clients from the beta to the GA interface to access async function calling and image input. Set session truncation retention\_ratio to 0.8 to optimize cache usage in long sessions. Implement sideband connections for secure server-side tool execution. Remove temperature parameters from GA requests and refine instructions instead.

**「Constraints and Model Behavior」** The GA model does not support arbitrary temperature settings; low temperatures do not make audio responses deterministic, and high temperatures cause audio aberrations. The beta interface lacks async function calling, which limits MCP tool performance. EU data residency requires explicit enablement and use of the eu.api.openai.com endpoint. Truncation drops messages without summarization; developers must implement compaction if needed.

**Tags**: `#Realtime API`, `#Session Management`, `#Cost Optimization`, `#Voice Agents`, `#System Architecture`

---

<a id="item-ai-practitioner-6"></a>
### [Agent testing failures and architectural constraints](https://danluu.com/agentic-testing/) ⭐️ 7.0/10

Agents often satisfy obvious, easily verifiable parts of a task while losing track of the constraint that determines success. When asked to use fuzzing, agents may generate random bytes without purpose. When asked to use formal verification, they may prove properties that are not useful. Agents left to their own devices produce specs that restate the existing implementation rather than defining intent. Manual refinement of specs allows agents to prove code satisfaction and uncover bugs. Effective testing depends on code architecture, such as enforcing dependency injection or hexagonal patterns.

hackernews · vinhnx · Sep 8, 02:58 · [Discussion](https://news.ycombinator.com/item?id=49605246)

**「Actionable steps for operators」** Manually refine formal specs to ensure they state intent rather than restating implementation. Enforce architectural patterns like dependency injection or hexagonal architecture before relying on agent-generated tests.

**「Limitations and context」** The source lacks reproducibility details, including prompts and setup links. One commenter argues the experiment is barely useful because it decouples testing from code architecture. The analysis relies on community comments as the primary evidence due to missing source content.

**「Community feedback」** Commenters report that agents generate tautological specs in Verus but succeed after manual refinement. Others criticize the lack of reproducibility and argue that testing cannot be decoupled from architecture. One user notes that forcing DI/hexagonal architecture improves test effectiveness.

**Tags**: `#agent-evaluation`, `#formal-verification`, `#testing-strategy`, `#workflow-design`, `#failure-modes`

---