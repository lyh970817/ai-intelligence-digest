---
layout: default
title: "Horizon Summary: 2026-11-24 (EN)"
date: 2026-11-24
lang: en
---

> From 35 items, 1 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Design ChatGPT Apps as Atomic Capabilities](#item-ai-practitioner-1) ⭐️ 8.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Design ChatGPT Apps as Atomic Capabilities](https://developers.openai.com/blog/what-makes-a-great-chatgpt-app) ⭐️ 8.0/10

OpenAI defines a ChatGPT app as a set of well-defined tools rather than a ported product UI. Developers should scope apps to atomic operations that satisfy one of three value models: Know \(provide new context or data\), Do \(take actions on behalf of the user\), or Show \(present information in actionable UIs\). Effective design requires clear, unambiguous tool names and parameters to aid model routing, stable structured outputs for chaining, and minimal data collection. Apps must handle vague and specific intents gracefully and function as part of a multi-tool ecosystem by keeping actions small and outputs interoperable.

rss · OpenAI Developer Blog \(Apify adapter\) · Nov 24, 12:00

**「Actionable Design Steps」** Replace broad feature ports with a handful of atomic, clearly named operations \(e.g., search\_properties, create\_ticket\) that map directly to specific user jobs-to-be-done. Ensure each operation uses precise parameters and returns stable, structured schemas to enable reliable model routing and downstream chaining.

**「Scope and Constraints」** The guidance focuses on the ChatGPT Apps platform and MCP servers. It emphasizes that apps should not attempt to recreate full navigation hierarchies or own the entire user journey, but instead act as capabilities the model orchestrates within a conversation.

**Tags**: `#agent-design`, `#tool-use`, `#api-design`, `#llm-integration`, `#workflow-scoping`

---