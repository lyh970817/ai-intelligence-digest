---
layout: default
title: "Horizon Summary: 2026-09-23 (EN)"
date: 2026-09-23
lang: en
---

> From 124 items, 3 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [DeepSeek 4.1 Flash context reliability drops after 125k tokens](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Prompt Strategies for LLM Classification](#item-ai-practitioner-2) ⭐️ 7.0/10
3. [Migrate Agentic Workflows to Responses API](#item-ai-practitioner-3) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [DeepSeek 4.1 Flash context reliability drops after 125k tokens](https://www.reddit.com/r/DeepSeek/comments/1wo67kq/deepseek_41_flash_has_context_problems/) ⭐️ 8.0/10

DeepSeek 4.1 Flash exhibits significant tool-call argument errors and system prompt forgetting beyond 125k tokens of input context. The model reverts to training data instincts, such as using the argument &quot;command&quot; instead of the specified &quot;cmd&quot; for shell tools. Error rates in tool arguments rise from 0.2% at 0–25k tokens to 50.7% above 300k tokens. The model also becomes susceptible to prompt injection from file reads or web searches at larger context sizes. Treating the effective context window as 125k tokens improves reliability but increases costs by disrupting cache efficiency.

reddit · r/DeepSeek · /u/hegbork · Sep 23, 13:35

**「Action」** Limit effective context to ~125k tokens for DeepSeek 4.1 Flash to maintain tool-use reliability, despite the resulting increase in cache read costs.

**「Evidence and limits」** Data comes from a single developer&\#x27;s coding agent tests. Sample sizes decrease at higher token ranges \(e.g., 580 calls &gt;300k\). Sessions with ~70% error rates after 500k tokens were excluded due to small sample size.

**Tags**: `#context-management`, `#model-evaluation`, `#agent-reliability`, `#deepseek`, `#tool-use`

---

<a id="item-ai-practitioner-2"></a>
### [Prompt Strategies for LLM Classification](https://www.nobodywho.ai/posts/jev-in-25-lines/) ⭐️ 7.0/10

Commenters suggest placing classification options before the input text to leverage masked attention. This allows the transformer to create state for the specific task before processing the body. Users also recommend adding few-shot examples in the system prompt to improve calibration. Repeating the task definition and labels clarifies instructions. Clear system instructions and a carefully worded beginning to the assistant output prevent the model from wandering off when extracting logprobs.

hackernews · bashbjorn · Sep 23, 07:26 · [Discussion](https://news.ycombinator.com/item?id=49812769)

**「Reorder Prompt Structure」** Place classification labels before the input text in your prompts to improve attention mechanics.

**「Alternative Implementations and Critiques」** One user demonstrated a seven-line implementation using DSPy instead of raw Python. Another commenter noted the original post lacks latency, compute, and error rate comparisons. They also questioned if the output format is reliably parseable and suggested the title might be parody.

**Tags**: `#prompt-engineering`, `#classification`, `#llm-reliability`, `#attention-mechanics`

---

<a id="item-ai-practitioner-3"></a>
### [Migrate Agentic Workflows to Responses API](https://developers.openai.com/blog/responses-api) ⭐️ 7.0/10

OpenAI advocates migrating agentic and multi-turn workflows from /v1/chat/completions to /v1/responses. The Responses API preserves reasoning state across turns, unlike Chat Completions which drops reasoning between calls. This state preservation yields a +5% gain on TAUBench for GPT-5. The API executes hosted tools \(File Search, Code Interpreter, Web Search, Image Gen, MCP\) server-side, reducing backend round-trips. Internal benchmarks show 40–80% better cache utilization compared to Chat Completions, lowering latency and costs. The API emits receipts for tool calls and intermediate steps but hides raw chain-of-thought to mitigate hallucination and safety risks.

rss · OpenAI Developer Blog \(Apify adapter\) · Sep 22, 12:00

**「Actionable Migration Step」** Switch agentic and multi-turn workflows to /v1/responses to leverage preserved reasoning state and hosted tools.

**「Performance Claims and Constraints」** The +5% TAUBench improvement and 40–80% cache utilization gains are cited as internal benchmarks. Raw chain-of-thought is not exposed to the client; developers receive only structured receipts. Chat Completions remains supported for non-agentic use cases.

**Tags**: `#agent-architecture`, `#api-design`, `#cost-optimization`, `#reasoning-models`, `#workflow-management`

---