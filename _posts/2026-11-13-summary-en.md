---
layout: default
title: "Horizon Summary: 2026-11-13 (EN)"
date: 2026-11-13
lang: en
---

> From 130 items, 6 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Single agent with skills outperforms multi-agent team in cost and speed](#item-ai-practitioner-1) ⭐️ 9.0/10
2. [Decoupled offline Charon/Aeneas/Coq verification for AI-generated no\_std Rust](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Three-layer agent architecture: Skills, Code Mode MCP, and on-demand signatures](#item-ai-practitioner-3) ⭐️ 8.0/10
4. [Generate and Validate Domain Glossaries for LLMs](#item-ai-practitioner-4) ⭐️ 8.0/10
5. [Local logs show Claude Code at ~100 tok/s vs Codex at ~38 tok/s](#item-ai-practitioner-5) ⭐️ 7.0/10
6. [RealtimeVAD trades false positives for 110ms lower end-of-speech latency](#item-ai-practitioner-6) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Single agent with skills outperforms multi-agent team in cost and speed](https://www.reddit.com/r/ClaudeCode/comments/1xuqnnc/i_tested_anthropics_one_agent_with_skills_beats_a/) ⭐️ 9.0/10

A controlled experiment compared a single Claude Code agent using &\#x27;skills&\#x27; against a team of subagents \(orchestrator, planner, builder, reviewer, tester\) on a booking site task. Both setups used Claude Code 2.1.319 and Sonnet 5.5. The single agent reused one long context, while each subagent started fresh. Over 7 runs per setup, both achieved 40/40 on hidden Playwright tests and a median design score of 37/50. The single agent cost $0.81 per site versus $1.31 for the team and took 15.0 minutes versus 28.6 minutes. The cost difference stems from context caching: subagents pay to cache prompts repeatedly, while the single agent reuses cached context. A plain agent without skills was cheaper but produced broken booking flows.

reddit · r/ClaudeCode · /u/Sufficient-Storage87 · Nov 12, 22:23

**「Actionable insight」** Prefer single-agent-with-skills architectures for bounded coding tasks to reduce cost and latency without sacrificing quality, as context reuse eliminates redundant prompt caching costs inherent in multi-agent handoffs.

**「Limitations and caveats」** The test used only one model \(Sonnet 5.5\), one task type, and 7 runs per setup. Design scoring relied on Claude sessions, not human judges. Subagents ran in parallel in the team setup, whereas reviewer and tester ran sequentially in the single-agent setup. Costs reflect API list prices via a subscription, not Anthropic&\#x27;s official eval kit. A specific failure mode in the team setup involved handoff errors where the orchestrator applied unnecessary fixes after the tester correctly identified false alarms.

**Tags**: `#agent-architecture`, `#cost-optimization`, `#evaluation-harness`, `#context-management`, `#claude-code`

---

<a id="item-ai-practitioner-2"></a>
### [Decoupled offline Charon/Aeneas/Coq verification for AI-generated no\_std Rust](https://www.reddit.com/r/cursor/comments/1xvgqvq/keeping_aigenerated_no_std_rust_honest_decoupled/) ⭐️ 8.0/10

The author splits AI-assisted \#\!\[no\_std\] Rust development into two layers. The runtime repo keeps the crate untouched with \#\!\[forbid\(unsafe\_code\)\] and zero heap allocation to maintain fast local cargo check/test loops in Cursor. An offline OCI verification airlock runs downstream CI in a --network none container pinned by SHA-256 digest. This container uses Charon, Aeneas, and Coq 8.18.0. Canary mutant sanity checks inject broken safety predicates and inverted capability checks to ensure the proof pipeline does not pass on vacuous specs. The process runs coqchk -o to verify Print Assumptions == ∅ and emits a Sigstore-attested REFINEMENT-AUDIT.json bound to the git commit SHA and tree SHA-256.

reddit · r/cursor · /u/AdmissibilityScience · Nov 13, 19:10

**「Actionable step」** Move heavy formal verification \(Charon/Coq\) to an offline CI airlock to keep local AI-assisted editing fast while maintaining strict safety guarantees.

**Tags**: `#formal-verification`, `#ci-cd`, `#rust`, `#agent-workflow`, `#code-quality`

---

<a id="item-ai-practitioner-3"></a>
### [Three-layer agent architecture: Skills, Code Mode MCP, and on-demand signatures](https://www.reddit.com/r/ChatGPTCoding/comments/1xv585r/skills_code_mode_mcp_how_i_taught_an_ai_agent_to/) ⭐️ 8.0/10

The author implemented a three-layer architecture to manage hundreds of MCP tools without bloating LLM context. Layer 1 \(Persistent Context\) exposes only brief Skill descriptions and two Code Mode tools: search\(\) and execute\(\). Layer 2 \(Skills\) loads on demand when the agent identifies a relevant workflow; it lists necessary MCP servers and method names but omits full signatures. Layer 3 \(Code Mode MCP\) finds full method descriptions via search\(\) and executes JavaScript sequences via execute\(\), allowing multiple calls without returning to the LLM between steps. The author notes that hiding tools behind Code Mode alone caused agents to miss methods or fail to search, while Skills guide the agent on what to look for. Savings depend on catalog size and search frequency.

reddit · r/ChatGPTCoding · /u/ievkz · Nov 13, 11:16

**「Operator Takeaway」** Replace static tool lists with a layered system: define Skills that map workflows to specific MCP method names, expose only search\(\) and execute\(\) in persistent context, and load full method signatures on demand via Code Mode.

**「Evidence and Limits」** The author states that token savings are likely but require testing on concrete tasks to measure accurately. The architecture does not guarantee success; the LLM may still choose the wrong Skill, search for incorrect methods, or generate invalid JavaScript. Not all operations can combine into a single execute\(\) call if intermediate analysis is required.

**Tags**: `#agent-architecture`, `#context-management`, `#mcp`, `#tool-use`, `#workflow-design`

---

<a id="item-ai-practitioner-4"></a>
### [Generate and Validate Domain Glossaries for LLMs](https://martinfowler.com/bliki/GeneratedGlossary.html) ⭐️ 8.0/10

Use an LLM to scan internal documents, emails, and chat logs for specialized vocabulary. Identify single words, phrases, and known terms used in unfamiliar ways. Generate a draft glossary with precise, concise definitions, noting alternative meanings by context. Have human experts review and amend the draft. Store the glossary in version control and refresh it on a schedule. Resist creating a single standard glossary; instead, maintain separate glossaries for different bounded contexts \(e.g., source code vs. human text\). For large glossaries, include only terms and links in the initial context, allowing the model to fetch full definitions as needed. Use the glossary to guide code generation names and flag deprecated terms.

rss · Thoughtworks and Martin Fowler · Nov 12, 14:15

**「Action」** Implement a workflow where an LLM generates a domain glossary from internal texts, humans validate it, and agents inject it into context via lazy-loaded links to save tokens.

**「Constraints」** The author states they have &\#x27;yet to see&\#x27; a single standard glossary work across an organization. Audio or video transcripts may help but are not always necessary if enough text exists.

**Tags**: `#context-engineering`, `#domain-modeling`, `#agent-workflow`, `#token-optimization`, `#knowledge-management`

---

<a id="item-ai-practitioner-5"></a>
### [Local logs show Claude Code at ~100 tok/s vs Codex at ~38 tok/s](https://www.reddit.com/r/codex/comments/1xv0v7t/codex_vs_claude_code_speed_from_my_local_logs_38/) ⭐️ 7.0/10

The author parsed local session logs from ~/.codex/sessions and ~/.claude/projects for recent coding chats. They calculated tokens per second as output tokens \(including thinking\) divided by time from request to response completion, excluding tool time. Codex averaged ~38 tok/s and appeared hard-capped around 40. Claude Code averaged ~100 tok/s, varying more but running roughly 2.5× faster. The author used Codex Pro \($200\) and Claude \($20\).

reddit · r/codex · /u/Relative-Climate1791 · Nov 13, 06:46

**「Prefer Claude Code for rapid iteration when speed matters」** Route coding tasks that prioritize raw output speed to Claude Code, as local logs show it averaging ~100 tok/s versus Codex&\#x27;s ~38 tok/s.

**「Small sample and single-user context」** The data comes from the last few chats for one user. The author notes they are just sampling from these sessions. Results may not generalize across different workloads, accounts, or tiers.

**Tags**: `#model-comparison`, `#performance-metrics`, `#agent-routing`, `#coding-agents`, `#latency`

---

<a id="item-ai-practitioner-6"></a>
### [RealtimeVAD trades false positives for 110ms lower end-of-speech latency](https://github.com/KoljaB/RealtimeVAD) ⭐️ 7.0/10

The author replaced Silero VAD with a 10 ms adaptive energy detector to reduce end-of-speech latency. The detector adapts its threshold to environment noise. This approach creates more false positives, but the author&\#x27;s speculative generation pipeline allows fast abortion if the user continues speaking. Benchmarks over ~3200 turns from assistant logs showed an initial ~110 ms speedup. After a fix for quiet speech, the improvement settled at 100 ms.

rss · Show HN \(10+ points\) · Nov 12, 21:30

**「Action」** Use an adaptive energy detector instead of Silero VAD if your pipeline supports fast aborts for false triggers.

**「Evidence and limits」** The benchmark covers ~3200 turns from the author&\#x27;s own assistant logs. The solution requires a speculative generation pipeline that can abort quickly when a false positive occurs. A fix was needed to handle quiet speech.

**Tags**: `#voice-agents`, `#latency-optimization`, `#vad-tuning`, `#speculative-execution`, `#agent-workflow`

---