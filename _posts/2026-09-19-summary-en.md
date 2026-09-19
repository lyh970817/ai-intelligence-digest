---
layout: default
title: "Horizon Summary: 2026-09-19 (EN)"
date: 2026-09-19
lang: en
---

> From 104 items, 5 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Enable reasoning\_effort\_override to preserve prompt cache in Codex](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Audit reveals 58% drop in Claude Code Max 20x subscription value](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Migrate agentic workflows to Responses API for stateful reasoning](#item-ai-practitioner-3) ⭐️ 7.0/10
4. [Cross-validate DeepSeek 4.1 Flash with Kimi to cut costs](#item-ai-practitioner-4) ⭐️ 7.0/10
5. [Cursor Plan Usage: Dollar-Capped &\#x27;Other Models&\#x27; Pool](#item-ai-practitioner-5) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Enable reasoning\_effort\_override to preserve prompt cache in Codex](https://www.reddit.com/r/codex/comments/1wk8jzq/one_flag_to_keep_989_of_my_prompt_cached_when/) ⭐️ 8.0/10

Enabling the \`reasoning\_effort\_override\` flag in OpenAI&\#x27;s Codex CLI preserves ~99% of prompt cache when switching Astra reasoning effort levels. The author tested this with a ChatGPT Pro login on bundled Codex build 0.155.0-alpha.2.6. With the flag off, switching from low to medium effort cached 55.8% of input tokens. With the flag on, it cached 98.9%. Switching back to low maintained 99.3% cache. Codex keeps the request-level effort fixed and adds a trusted \`configuration\_update\` to the conversation. Operators can enable it for one session via \`codex --enable reasoning\_effort\_override -m gpt-6-astra\` or persist it via \`codex features enable reasoning\_effort\_override\`. Mac app users must fully quit and reopen the app after enabling.

reddit · r/codex · /u/systemous · Sep 19, 01:26

**「Action」** Run \`codex features enable reasoning\_effort\_override\` and restart the Codex Mac app to maintain high prompt cache hit rates when changing reasoning effort levels.

**「Limits」** The feature is marked under development. Results come from version 0.155.0-alpha.2.6; newer main versions check a model-capability flag, so success is not guaranteed for every version. The reported numbers are cache-hit percentages, not direct subscription cost reductions. Some cache noise was present in the control data.

**Tags**: `#prompt-caching`, `#cost-optimization`, `#cli-configuration`, `#openai-codex`, `#workflow-optimization`

---

<a id="item-ai-practitioner-2"></a>
### [Audit reveals 58% drop in Claude Code Max 20x subscription value](https://www.reddit.com/r/ClaudeCode/comments/1wk3zq5/i_audited_my_session_logs_against_the_usage_meter/) ⭐️ 8.0/10

The author parsed local session logs from ~/.claude/projects on two machines. They deduped messages by ID and extracted usage blocks \(input, output, cache write, cache read\) from assistant messages. The author priced these tokens at published API list rates for Opus: $5 input, $25 output, $6.25 cache write, and $0.50 cache read per million. They divided the total dollar value by the percentage reported by the usage endpoint to calculate dollars per percent. Last week, a Max 20x account yielded about $5,540 of usage. This week, the same account yields about $2,350. The weekly dollar cap dropped by 58 percent, while the announced change was 17 percent. The author notes their traffic is 95 percent cache reads by token count.

reddit · r/ClaudeCode · /u/Siigari · Sep 18, 22:07

**「Actionable step」** Parse your local JSONL transcripts for assistant lines with usage objects. Sum the tokens by reset window and price them at list rates. Compare this calculated dollar value against the percentage shown by the /usage endpoint to determine your actual dollars-per-percent.

**「Limitations and context」** The author reduced their own burn rate by 43 percent between the two weeks through fewer calls and shorter contexts. Anthropic has not published how the usage meter is weighted. The author cannot prove from their side that cache reads were re-weighted, though they suspect this caused the collapse in dollars-per-percent.

**Tags**: `#cost-optimization`, `#agent-operations`, `#usage-auditing`, `#prompt-caching`, `#subscription-management`

---

<a id="item-ai-practitioner-3"></a>
### [Migrate agentic workflows to Responses API for stateful reasoning](https://developers.openai.com/blog/responses-api) ⭐️ 7.0/10

OpenAI designed the /v1/responses endpoint as a stateful agentic loop. It preserves the model&\#x27;s reasoning state across turns, unlike /v1/chat/completions which drops context between calls. The API supports hosted tools \(File Search, Code Interpreter, Web Search, Image Gen, MCP\) that execute server-side. It emits multiple output items, including tool calls and intermediate steps, while keeping raw chain-of-thought hidden and encrypted.

rss · OpenAI Developer Blog \(Apify adapter\) · Sep 22, 12:00

**「Switch to /v1/responses for multi-step agents」** Migrate agentic and reasoning workflows from /v1/chat/completions to /v1/responses. Use the previous\_response\_id parameter to maintain state across turns. Rely on hosted tools for RAG and code execution to reduce backend latency and cost.

**「Performance gains and safety constraints」** Internal benchmarks show GPT-5 scores 5% higher on TAUBench when using Responses due to preserved reasoning. Cache utilization improves by 40–80% compared to Chat Completions. Raw chain-of-thought remains inaccessible to clients to prevent exposure of unaligned thoughts and competitive risks. Chat Completions remains supported but is not the default for future agentic development.

**Tags**: `#agent-architecture`, `#api-design`, `#reasoning-models`, `#cost-optimization`, `#openai`

---

<a id="item-ai-practitioner-4"></a>
### [Cross-validate DeepSeek 4.1 Flash with Kimi to cut costs](https://www.reddit.com/r/DeepSeek/comments/1wklqt2/i_tried_gpt_astra_turned_to_deepseek_41_flash/) ⭐️ 7.0/10

The author spent $130 on GPT Astra for about a dozen turns but it failed to meet requirements. They switched to DeepSeek 4.1 Flash, which identified multiple issues in the project for no extra cost. The author then used Kimi to review DeepSeek&\#x27;s output. Kimi found flaws and provided feedback, which the author passed back to DeepSeek for correction.

reddit · r/DeepSeek · /u/OwlZealousideal4779 · Sep 19, 13:04

**「Use Kimi to review DeepSeek drafts」** Route initial issue identification and drafting to DeepSeek 4.1 Flash, then use Kimi to cross-validate the output and catch flaws before finalizing fixes.

**「Cost and model availability constraints」** DeepSeek 4.1 Flash and Hy4 preview calls were free on WorkBuddy at the time of writing. The author notes that every model&\#x27;s first draft has flaws, necessitating cross-validation and a predefined standard for correctness.

**Tags**: `#agent-workflow`, `#cost-optimization`, `#model-routing`, `#quality-control`, `#cross-validation`

---

<a id="item-ai-practitioner-5"></a>
### [Cursor Plan Usage: Dollar-Capped &\#x27;Other Models&\#x27; Pool](https://www.reddit.com/r/cursor/comments/1wjzc8n/pro_20_vs_pro_60_vs_ultra_200_real_included_usage/) ⭐️ 7.0/10

The author shared dashboard screenshots from three Cursor plans \(Pro $20, Pro+ $60, Ultra $200\) with filled usage bars. The &\#x27;Other Models&\#x27; allowance is a dollar pool at API prices, not a fixed token count. Token totals vary significantly based on model mix, thinking effort, context, and cache. Pro plan used 130.4M Cursor tokens and 159.8M Other tokens. Pro+ used 1.1B Cursor tokens and 465.1M Other tokens. Ultra used 4.2B Cursor tokens \(81.1% utilized\) and 2.4B Other tokens \(99.8% utilized\). Heavy agent workflows using Claude Sonnet thinking models deplete the Other pool quickly.

reddit · r/cursor · /u/tagoslabs · Sep 18, 19:08

**「Calculate Plan Based on Model Mix」** Estimate your expected model mix and calculate dollar-equivalent token burn instead of relying on nominal token limits to prevent unexpected overages.

**「Data Limitations」** The data comes from different billing months for each plan, representing real usage rather than official specifications. The author notes that the same plan can show very different token totals depending on the specific models selected.

**Tags**: `#cost-management`, `#agent-workflows`, `#tool-evaluation`, `#cursor-ide`, `#model-routing`

---