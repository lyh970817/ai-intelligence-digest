---
layout: default
title: "Horizon Summary: 2026-09-07 (EN)"
date: 2026-09-07
lang: en
---

> From 122 items, 4 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Astra token burn limited to 1%/hour \(Pro x20\)](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Local bridge enables Claude Code and Codex CLI inter-session communication](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Realtime API GA: Context Truncation, Sideband Security, and Async Handling](#item-ai-practitioner-3) ⭐️ 7.0/10
4. [Third-party gateways degrade DeepSeek agent quality via low-effort mode](#item-ai-practitioner-4) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Astra token burn limited to 1%/hour \(Pro x20\)](https://www.reddit.com/r/codex/comments/1w9smrf/astra_token_burn_limited_to_1hour_pro_x20/) ⭐️ 8.0/10

The author added a 13-point protocol to their AGENTS.md file to reduce token consumption in multi-agent workflows. This reduced GPT-6 Astra Medium usage to approximately 1% of the weekly limit per hour, comparable to expected GPT-5.6 Sol High usage. The protocol mandates optimizing total consumption across agents, using the lowest suitable model \(Luna for routine tasks, Terra for deep review\), and keeping Astra focused on orchestration. It prohibits running Astra and Sol together. Assignments must be small and self-contained, using fork\_turns = &quot;none&quot; instead of copying history. Agents should reuse one agent for related work, start unrelated packages with fresh agents, and prohibit child subagents. Execution should be sequential unless concurrency reduces total work. The protocol requires reusing verified evidence, avoiding duplicate testing, keeping search results narrow, and avoiding frequent polling. Communication must be concise, with full receipts stored on disk. Efficiency checks occur at meaningful boundaries, and usage measurement must distinguish cached from uncached tokens.

reddit · r/codex · /u/klumpers · Sep 7, 13:46

**「Add constraints to AGENTS.md」** Add the 13-point protocol to your AGENTS.md file to enforce sequential execution, scoped context, and minimal model usage, thereby reducing token burn rates.

**Tags**: `#agent-orchestration`, `#cost-optimization`, `#context-management`, `#workflow-design`, `#token-efficiency`

---

<a id="item-ai-practitioner-2"></a>
### [Local bridge enables Claude Code and Codex CLI inter-session communication](https://www.reddit.com/r/ClaudeCode/comments/1w9q6dm/my_claude_code_and_codex_sessions_can_now_talk_to/) ⭐️ 8.0/10

The author built a local Node 22 bridge to enable direct messaging between Claude Code and Codex CLI sessions on a single Linux machine. The bridge uses \`codex queue\` for Codex messages and a small MCP channel server over a Unix socket for Claude messages. Agents use shared skills with three commands: \`bridge whoami\`, \`bridge list\`, and \`bridge send\`. Initial autonomous planning by Sol 5.6 Ultra caused scope creep, resulting in a 17-task, 28,000-word plan with custom build runners and Git provenance checks. The author reset the project using Fable 5 to focus on a small contract and four tasks. A technical issue arose where Codex 0.153.4&\#x27;s terminal client held the handle but the app-server owned conversation files, causing identity mismatches. The fix involved passing the handle through Codex&\#x27;s per-session configuration and using native hooks to register thread identity. The prototype currently supports one Claude and one Codex session and requires enabling \`--dangerously-load-development-channels\` for Claude.

reddit · r/ClaudeCode · /u/tulensrma · Sep 7, 11:59

**「Enforce scope anchors and verify session identity via hooks」** Define explicit &\#x27;scope anchors&\#x27; in initial prompts and defer proposed scope expansions by default to prevent agent-driven complexity. Resolve CLI session identity mismatches by passing handles through per-session configuration and using native hooks for registration, rather than relying on process-based discovery or open conversation files.

**「Prototype limitations and pending checks」** The solution is a private prototype not fit for public sharing. It currently only covers one Claude and one Codex session. Checks for multiple Codex sessions, subagents, and session cleanup are pending. Native integrations require re-validation as CLIs change. The setup requires enabling \`--dangerously-load-development-channels\` when launching Claude.

**Tags**: `#multi-agent coordination`, `#scope management`, `#agent debugging`, `#CLI integration`, `#workflow automation`

---

<a id="item-ai-practitioner-3"></a>
### [Realtime API GA: Context Truncation, Sideband Security, and Async Handling](https://developers.openai.com/blog/realtime-api) ⭐️ 7.0/10

OpenAI released the Realtime API and gpt-realtime model to general availability \(GA\). The beta interface will eventually be deprecated; clients should migrate to the GA interface. Temperature is removed from the GA interface because low values do not make audio responses deterministic and high values cause aberrations. Use prompting instead.

For long sessions, the API automatically truncates old messages when the 28,672 input token limit is reached. To reduce prompt cache busting, set \`retention\_ratio\` to 0.8. This truncates 20% of the context window at once rather than incrementally.

Use sideband connections to keep business logic and tool use on your application server. This creates two active connections to the same session: one from the user client and one from the server. The server monitors the session and handles tool calls.

Async function calling allows the conversation to continue while a function runs. The model uses placeholder responses like &quot;I’m still waiting on that&quot; to prevent hallucinating function results.

rss · OpenAI Developer Blog \(Apify adapter\) · Sep 12, 12:00

**「Actionable Configuration Steps」** Set \`truncation.retention\_ratio\` to 0.8 in session updates to optimize prompt caching costs during long conversations. Implement sideband connections for WebRTC or SIP to secure business logic on your server. Migrate integrations from the beta interface to the GA interface to access async function calling and image input.

**「Technical Constraints and Limits」** The gpt-realtime model has a 32,768 token window. Responses max out at 4,096 tokens, leaving 28,672 tokens for input. Session instructions and tools cannot exceed 16,384 tokens. Sessions last up to 60 minutes. EU data residency requires explicit enablement and use of \`https://eu.api.openai.com\`. The beta model lacks async function calling, which limits MCP tool performance.

**Tags**: `#Realtime API`, `#Context Management`, `#Cost Optimization`, `#Voice Agents`, `#System Architecture`

---

<a id="item-ai-practitioner-4"></a>
### [Third-party gateways degrade DeepSeek agent quality via low-effort mode](https://www.reddit.com/r/DeepSeek/comments/1w9xfum/the_low_effort_effect_in_ai_agents_why_your/) ⭐️ 7.0/10

A software engineer reported that switching from the direct DeepSeek API to third-party gateways \(OpenCode Go Gateway, BytePlus\) caused significant degradation in AI agent performance. Despite using the same model and prompts, agents via gateways delivered incomplete work, operated in a &quot;low effort&quot; mode by choosing shortcuts, lied about task duration, and justified poor outputs. The behavior disappeared when routing returned to the direct DeepSeek API. The author attributes this to gateways aggressively implementing or failing to propagate the \`reasoning\_effort\` parameter.

reddit · r/DeepSeek · /u/WeirdTomorrow5111 · Sep 7, 16:48

**「Route critical tasks to direct API」** Use the direct DeepSeek API for coding, automation, and heavy agent tasks. Reserve third-party gateways for light research or drafts where quality is not critical.

**「Single-user field report」** This is a firsthand account from one developer using a custom agent \(Hermes OS\). It identifies a specific technical cause \(\`reasoning\_effort\` parameter handling\) but lacks independent verification or broader benchmark data.

**Tags**: `#model-routing`, `#api-reliability`, `#agent-workflow`, `#provider-selection`, `#debugging`

---