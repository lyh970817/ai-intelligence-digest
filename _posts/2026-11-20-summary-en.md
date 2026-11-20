---
layout: default
title: "Horizon Summary: 2026-11-20 (EN)"
date: 2026-11-20
lang: en
---

> From 53 items, 2 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Design ChatGPT Apps as Scoped Toolkits](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Healthy code cuts AI agent review costs by 22-35%](#item-ai-practitioner-2) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Design ChatGPT Apps as Scoped Toolkits](https://developers.openai.com/blog/what-makes-a-great-chatgpt-app) ⭐️ 8.0/10

ChatGPT Apps function as sets of well-defined tools rather than mini-versions of existing products. Developers should scope capabilities to specific jobs-to-be-done using the &\#x27;Know/Do/Show&\#x27; framework: providing new context \(Know\), taking actions \(Do\), or presenting structured UIs \(Show\). Effective apps use clear, descriptive action names and stable, machine-readable schemas to aid model routing and multi-tool orchestration. Outputs must be chainable, avoiding long tunnel-like flows to allow the model to manage the conversation.

rss · OpenAI Developer Blog \(Apify adapter\) · Nov 24, 12:00

**「Actionable Steps for Tool Definition」** Define tools with small, focused actions \(e.g., \`search\_properties\` instead of \`run\_full\_pipeline\`\) and strict, minimal parameter schemas. Ensure every tool output includes stable IDs and structured data fields to support chaining with other apps. Validate that each tool clearly satisfies at least one &\#x27;Know,&\#x27; &\#x27;Do,&\#x27; or &\#x27;Show&\#x27; value criterion before deployment.

**「Scope and Constraints」** The guidance applies specifically to the ChatGPT Apps environment and MCP servers. It emphasizes that apps should not require full navigation hierarchies or port every product feature. The source notes that ambiguity in tool definitions acts as a &\#x27;tax on routing,&\#x27; reducing the frequency of model invocation.

**Tags**: `#agent-tool-design`, `#prompt-engineering`, `#model-orchestration`, `#api-design`, `#workflow-scoping`

---

<a id="item-ai-practitioner-2"></a>
### [Healthy code cuts AI agent review costs by 22-35%](https://martinfowler.com/fragments/2026-11-20.html) ⭐️ 7.0/10

Marcus Borg ran an experiment on 465 pull requests across 246 open source repositories. A five-agent review and fix pipeline processed each request. CodeScene measured code health. Healthy code \(score 9.7\) cost 22% to 35% less to review than unhealthy code \(score 2.8\). Complex Method and Complex Conditional smells drove the higher costs.

rss · Thoughtworks and Martin Fowler · Nov 20, 18:38

**「Refactor complex methods and conditionals before agent review」** Prioritize refactoring Complex Method and Complex Conditional smells before handing code to agents. This reduces token usage and review friction.

**「Study scope and metrics」** The data covers three LLMs and uses CodeScene for health metrics. The cost reduction range applies to the difference between typical unhealthy and healthy pull requests in this sample.

**Tags**: `#agent-cost-optimization`, `#code-quality-metrics`, `#agentic-workflow`, `#refactoring-priorities`

---