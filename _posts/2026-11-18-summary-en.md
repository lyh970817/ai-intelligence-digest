---
layout: default
title: "Horizon Summary: 2026-11-18 (EN)"
date: 2026-11-18
lang: en
---

> From 53 items, 4 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Designing ChatGPT Apps as Focused Toolkits](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Workflow for shipping a 21,000-line feature with AI agents](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Data Contracts for AI Agent Reliability](#item-ai-practitioner-3) ⭐️ 8.0/10
4. [External sandboxes for coding agents](#item-ai-practitioner-4) ⭐️ 8.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Designing ChatGPT Apps as Focused Toolkits](https://developers.openai.com/blog/what-makes-a-great-chatgpt-app) ⭐️ 8.0/10

ChatGPT apps function as sets of well-defined tools rather than mini-versions of existing products. Developers should select capabilities using the &\#x27;Know/Do/Show&\#x27; filter: providing new context or data, taking real actions on behalf of the user, or presenting information in clearer, actionable UIs. Effective apps expose a small number of concrete operations with clear names and minimal, structured parameters. Outputs must be stable and machine-readable to support multi-agent chaining. Apps should handle both vague and specific intents by delivering immediate value and avoiding long onboarding flows.

rss · OpenAI Developer Blog \(Apify adapter\) · Nov 24, 12:00

**「Actionable Design Steps」** Replace broad feature ports with a handful of clearly named operations tied to specific jobs-to-be-done. Ensure tool schemas use minimal, structured inputs and return stable IDs with consistent field names to enable ecosystem interoperability.

**「Scope and Constraints」** The guidance applies specifically to the ChatGPT Apps platform and its Model Context Protocol \(MCP\) server implementation. The source emphasizes that apps are one of several tools the model may orchestrate, requiring developers to design for handoffs rather than controlling the entire user journey.

**Tags**: `#agent-design`, `#tool-calling`, `#api-design`, `#workflow-scoping`, `#interoperability`

---

<a id="item-ai-practitioner-2"></a>
### [Workflow for shipping a 21,000-line feature with AI agents](https://www.aihero.dev/watch-me-ship-a-21-000-line-feature-with-mattpocock-skills~ez95n) ⭐️ 8.0/10

The author shipped a 21,000-line feature using a structured agent workflow. The process began with &quot;Grill With Docs,&quot; where the author discussed the problem&\#x27;s &quot;why&quot; with an agent to refine the data model and naming conventions. A GLOSSARY.md file \(560 lines\) provided context for domain concepts, while ADRs explained historical decisions. The author used a prototype skill to generate three UI variants in a subagent, selecting the best option to reduce decision space for implementation. Work was scoped into a spec document and 47 user stories across nine parallel sub-issues. The implementation ran AFK \(away from keyboard\), producing a large PR. The author reviewed the code using stacked diffs, separating reversible &quot;two-way doors&quot; from critical &quot;one-way doors&quot; protected by feature flags. Finally, a &quot;Retro&quot; skill analyzed session transcripts and review comments to identify gaps in coding standards, resulting in new lint rules and documentation updates.

rss · AI Hero · Nov 18, 17:16

**「Convert review comments into lint rules」** Run a retroactive analysis on agent session transcripts and human review comments to identify recurring style or pattern violations. Convert these findings into deterministic lint rules or documentation updates to prevent recurrence in future agent sessions.

**「Context costs and scope」** The author notes that keeping agents in the &quot;smart zone&quot; \(lower token count\) yields better results and lower costs than the &quot;dumb zone&quot; \(high token count, e.g., 260k+ tokens\). The workflow relies on a mature codebase with existing glossaries and ADRs; the author describes this as &quot;turning an oil tanker around&quot; due to thousands of existing instances contradicting new standards. The 21,000-line PR contained 18% comments, higher than the repo&\#x27;s 12% average, which the retro identified as a target for cleanup.

**Tags**: `#agent-workflow`, `#context-management`, `#code-review`, `#prompt-engineering`, `#software-engineering`

---

<a id="item-ai-practitioner-3"></a>
### [Data Contracts for AI Agent Reliability](https://martinfowler.com/articles/data-contracts.html) ⭐️ 8.0/10

Data contracts provide explicit, machine-readable metadata on schema, quality, and usage rights to help AI agents safely discover and process enterprise data. The Open Data Contract Standard \(ODCS\) defines these contracts in YAML, including SQL-based quality rules and service level agreements. Unlike humans who hesitate when distrusting data, agents treat every value as truth, leading to &quot;confidently wrong&quot; results without structured guardrails. Contracts act as the interface description for data products, enabling automated verification of promises like data freshness and completeness.

rss · Thoughtworks and Martin Fowler · Nov 18, 14:02

**「Operator Takeaway」** Implement ODCS YAML files for critical data interfaces to provide agents with verifiable schema, quality rules, and terms of use. Start with high-pain areas like broken pipelines or new use cases rather than rolling out contracts for all data at once.

**「Evidence and Limits」** The source notes that writing and maintaining contracts takes time and effort, and owners must keep the promises made. It advises against introducing contracts for all company data immediately, suggesting a focused approach on team-to-team interfaces where pain points exist.

**Tags**: `#ai-agents`, `#data-engineering`, `#metadata-management`, `#reliability`, `#workflow-design`

---

<a id="item-ai-practitioner-4"></a>
### [External sandboxes for coding agents](https://simonwillison.net/2026/Nov/17/external-sandboxes-for-coding-agents/) ⭐️ 8.0/10

Simon Willison and Prime Radiant released an external sandbox pattern that isolates agent code execution from the agent process. They provided three server implementations with a unified localhost API: external-sandbox-v86 \(Node.js/v86/WebAssembly\), external-sandbox-container \(Python/Apple Containers\), and external-sandbox-quicksand \(Python/Microsoft Quicksand\). Operators configure tools like Pi, Claude Code, or Codex to send execution calls to these sandboxes. The system includes an HTTP/HTTPS allow-list proxy to restrict network access and a credential replacement mechanism to prevent secret exposure.

rss · Simon Willison - Coding Agents · Nov 17, 22:52

**「Operator Takeaway」** Configure coding agents to route code execution through one of the three provided sandbox servers to isolate risks from prompt injections or mistakes.

**Tags**: `#agent-safety`, `#sandboxing`, `#workflow-architecture`, `#code-execution`, `#security-patterns`

---