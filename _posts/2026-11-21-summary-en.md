---
layout: default
title: "Horizon Summary: 2026-11-21 (EN)"
date: 2026-11-21
lang: en
---

> From 38 items, 2 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [OpenAI framework for ChatGPT Apps](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Healthy Code Reduces AI Agent Review Costs](#item-ai-practitioner-2) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [OpenAI framework for ChatGPT Apps](https://developers.openai.com/blog/what-makes-a-great-chatgpt-app) ⭐️ 8.0/10

OpenAI defines a ChatGPT App as a set of well-defined tools rather than a ported product UI. The model orchestrates these tools within conversations. Value comes from three capabilities: Know \(provide new context or data\), Do \(take actions on behalf of the user\), and Show \(present information in structured or visual UIs\). Developers should scope apps to small, composable actions with clear parameter names and stable structured outputs. Designs must avoid long, tunnel-like flows to allow multi-tool ecosystem interoperability.

rss · OpenAI Developer Blog \(Apify adapter\) · Nov 24, 12:00

**「Operator Takeaway」** Scope agent tools to specific, named operations that map to single jobs-to-be-done. Use clear, unambiguous parameter names and return stable, structured outputs to aid model routing and chaining.

**「Evidence and Limits」** The source provides a design framework and checklist. It does not include performance benchmarks or code implementations for the SDK.

**Tags**: `#agent-design`, `#tool-use`, `#context-scoping`, `#mcp`, `#workflow-orchestration`

---

<a id="item-ai-practitioner-2"></a>
### [Healthy Code Reduces AI Agent Review Costs](https://martinfowler.com/fragments/2026-11-20.html) ⭐️ 7.0/10

Marcus Borg reports an experiment showing that healthy code reduces AI agent review costs by 22% to 35%. The study compared a typical unhealthy pull request \(CodeHealth 2.8\) with a typical healthy one \(CodeHealth 9.7\). It analyzed 465 pull requests across 246 open source repositories using three LLMs and a five-agent review and fix pipeline. CodeScene identified &\#x27;Complex Method&\#x27; and &\#x27;Complex Conditional&\#x27; as the primary code smells driving increased costs.

rss · Thoughtworks and Martin Fowler · Nov 20, 18:38

**「Refactor Before Agent Handoff」** Refactor &\#x27;Complex Method&\#x27; and &\#x27;Complex Conditional&\#x27; smells before handing code to AI agents to lower token and compute costs.

**「Study Scope」** The data comes from a specific experiment using CodeScene metrics and a five-agent pipeline on open source repositories. Results apply to this setup and may vary with different tools or workflows.

**Tags**: `#agent-cost-optimization`, `#code-quality`, `#llm-evaluation`, `#refactoring`, `#workflow-design`

---