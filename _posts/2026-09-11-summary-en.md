---
layout: default
title: "Horizon Summary: 2026-09-11 (EN)"
date: 2026-09-11
lang: en
---

> From 120 items, 6 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Markdown Is All You Need](#item-ai-practitioner-1) ⭐️ 9.0/10
2. [Enforce hunk-level justification to stop agent diff padding](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Realtime API GA: Truncation, Sidebands, and Async Calls](#item-ai-practitioner-3) ⭐️ 7.0/10
4. [Practitioners reject RTK token savings in favor of explicit output truncation](#item-ai-practitioner-4) ⭐️ 7.0/10
5. [Datasette 1.0a39 and 0.65.4 security releases](#item-ai-practitioner-5) ⭐️ 7.0/10
6. [Offload Astra scaffolding to ChatGPT Pro message quota](#item-ai-practitioner-6) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Markdown Is All You Need](https://www.reddit.com/r/ClaudeCode/comments/1wd6m0p/markdown_is_all_you_need/) ⭐️ 9.0/10

The author replaced a 382-dependency memory runtime with a folder of structured Markdown files and a lightweight index \(MEMORY.md\). In a test involving three versions of a project decision \(REST, GraphQL, tRPC\), the runtime returned the superseded GraphQL fact because its retrieval path ignored temporal fields. The Markdown system returned the current tRPC decision with struck-through history and provenance tags. The architecture relies on strict editing rules: every fact carries a provenance tag \(\[stated\], \[observed\], \[inferred\], \[suggested\]\), inferred lessons require a recurrence gate, and supersession is handled by striking through old lines rather than appending. The system has run in production for seven months across three models.

reddit · r/ClaudeCode · /u/SIGH\_I\_CALL · Sep 11, 05:00

**「Operator Takeaway」** Adopt a file-based memory architecture using structured Markdown files with provenance tagging and explicit supersession editing rules \(strikethrough\) to ensure auditability and correct temporal reasoning without heavy infrastructure.

**「Evidence and Limits」** The comparison is a single-case field report \(n=1\) over seven months. The author notes the system works only if the LLM writer consistently follows the editing policy. It is designed for single-agent, single-human use; scaling to teams would require real locking and merge discipline. The author has not tested the scale ceiling beyond 345 daily notes and a few dozen entity files.

**Tags**: `#agent-memory`, `#workflow-design`, `#context-management`, `#debugging`, `#cost-optimization`

---

<a id="item-ai-practitioner-2"></a>
### [Enforce hunk-level justification to stop agent diff padding](https://www.reddit.com/r/ChatGPTCoding/comments/1wdbmoy/coding_agents_pad_their_diffs_to_look_thorough/) ⭐️ 8.0/10

Coding agents pad diffs with unnecessary reformatting, refactors, and dependencies to appear competent. This padding introduces bugs because reviewers skip unrequested changes. The author enforces strict scope rules in persistent config files \(AGENTS.md/CLAUDE.md\). The core rule requires the agent to list every changed file and justify each hunk against a specific task requirement before returning the diff. Hunks without a justification are reverted. A separate review prompt asks a different session to identify hunks that change behavior or structure beyond the task. This workflow reduced diff sizes by about 30% and decreased review surprises.

reddit · r/ChatGPTCoding · /u/Ok\_Negotiation\_2587 · Sep 11, 09:47

**「Operator Takeaway」** Add a scope rule block to AGENTS.md or CLAUDE.md that forces the agent to justify every diff hunk against a task requirement. Use a separate session to review the diff for changes that exceed the task scope.

**「Evidence and Limits」** The 30% diff size reduction is based on the author&\#x27;s personal experience with similar tasks. Agents may still drift during long sessions if the rules are not in a persistent config file. Strict dependency bans may halt agents that genuinely need a new library, requiring manual intervention.

**Tags**: `#agent-workflow`, `#prompt-engineering`, `#code-review`, `#diff-management`, `#scope-control`

---

<a id="item-ai-practitioner-3"></a>
### [Realtime API GA: Truncation, Sidebands, and Async Calls](https://developers.openai.com/blog/realtime-api) ⭐️ 7.0/10

OpenAI released the Realtime API and gpt-realtime model to general availability \(GA\). The beta interface will eventually be deprecated; migrate to the GA interface. Temperature is removed from the GA interface; use the default 0.8. Set \`retention\_ratio\` to 0.8 during truncation to reduce prompt cache busting costs. Use sideband connections to keep business logic and tool use on your server while clients connect via WebRTC or SIP. Async function calling is now supported in GA, preventing hallucinations during pending tool calls with automatic placeholder responses.

rss · OpenAI Developer Blog \(Apify adapter\) · Sep 12, 12:00

**「Actionable Configuration」** Update session configuration to set \`truncation.retention\_ratio\` to 0.8 for cost efficiency. Route tool execution through a server-side sideband connection rather than the client. Migrate integrations from the beta interface to the GA interface to access async function calling and image input.

**「Constraints and Limits」** Sessions last up to 60 minutes. The token window is 32,768 tokens, with a maximum input of 28,672 tokens after reserving 4,096 for responses. Session instructions and tools are limited to 16,384 tokens. EU data residency requires explicit enablement and use of \`https://eu.api.openai.com\`. The beta model lacks async function calling, which limits MCP tool performance.

**Tags**: `#realtime-api`, `#session-management`, `#cost-optimization`, `#voice-agents`, `#api-integration`

---

<a id="item-ai-practitioner-4"></a>
### [Practitioners reject RTK token savings in favor of explicit output truncation](https://quesma.com/blog/does-rtk-make-ai-coding-cheaper/) ⭐️ 7.0/10

Practitioners report that RTK&\#x27;s claimed token savings are misleading because the tool counts tokens from truncated command output as saved, even when the agent only processes the tail. Users observe that RTK increases agent run time and breaks sandboxing by persisting stats. Operators replace RTK with explicit rules in agent configuration, such as capping command output to 4000 bytes using \`head -c 4000\`, to reliably control context size and costs.

hackernews · michalwarda · Sep 11, 11:15 · [Discussion](https://news.ycombinator.com/item?id=49656471)

**「Operator Takeaway」** Replace RTK with explicit output truncation rules in agent configuration, such as \`COMMAND 2&gt;&amp;1 \| head -c 4000\`, to prevent streaming full logs or large files.

**「Evidence and Limits」** Claims rely on user benchmarks and observation rather than controlled studies. One user notes their benchmarks are older. Another suggests local code embedding reduces token use but increases CPU cost.

**「Discussion Signal」** Users describe RTK and similar tools as &quot;snakeoil&quot; or &quot;vaporware.&quot; One user reports that RTK causes random auto-mode denials. Another notes that AI labs have not upstreamed such optimizations, suggesting they lack real value.

**Tags**: `#cost-control`, `#agent-workflow`, `#context-management`, `#prompt-engineering`

---

<a id="item-ai-practitioner-5"></a>
### [Datasette 1.0a39 and 0.65.4 security releases](https://simonwillison.net/2026/Sep/11/datasette-security/) ⭐️ 7.0/10

Simon Willison and Alex Garcia audited Datasette using Claude Fable 5.1, GPT-5.6, and GPT-6 Astra. They split the remediation work: one developer created automated tests highlighting the issue, and the other implemented the fix. This ensured two separate humans reviewed each issue alongside coding agents.

rss · Simon Willison - Agentic Engineering · Sep 11, 03:27

**「Split test creation and fix implementation」** Assign one developer to write the failing test for a vulnerability and another to implement the fix to ensure dual human review.

**Tags**: `#security-audit`, `#workflow-pattern`, `#agent-coordination`, `#code-review`, `#testing-strategy`

---

<a id="item-ai-practitioner-6"></a>
### [Offload Astra scaffolding to ChatGPT Pro message quota](https://www.reddit.com/r/codex/comments/1wcsnbz/how_to_get_astra_without_burning_too_many_tokens/) ⭐️ 7.0/10

The author uses the separate weekly message quota for GPT-6 Pro in ChatGPT \(200 messages on the 20x plan, 50 on the 5x plan\) to handle initial code scaffolding and PRD implementation. This reserves the more expensive Codex/Astra agent for final verification and CI checks. The process involves connecting a GitHub repo to ChatGPT with read/write access, preparing a comprehensive PRD in a .md file, and pointing the AI to it once to avoid counting iterative refinements as multiple messages. The author uses Sol 5.6 Extra High for initial scanning. Since the Chat sandbox cannot run all verification steps, the operator must switch to Codex/Astra to fix broken CI, finish the work, and push back.

reddit · r/codex · /u/joaopaulo-canada · Sep 10, 19:09

**「Actionable step」** Connect your GitHub repo to ChatGPT, write a complete PRD, and use the GPT-6 Pro chat quota for initial code generation before switching to Codex/Astra for final verification and CI integration.

**「Constraints and caveats」** The ChatGPT sandbox is not identical to the local project environment and cannot run certain verification steps. If the model asks to use &\#x27;ChatGPT Work,&\#x27; stop and rephrase or slice the task smaller to avoid burning the weekly quota. This strategy is most effective for greenfield projects, new features, and disposable prototypes.

**Tags**: `#cost-optimization`, `#agent-coordination`, `#workflow-design`, `#prompt-engineering`, `#developer-tools`

---