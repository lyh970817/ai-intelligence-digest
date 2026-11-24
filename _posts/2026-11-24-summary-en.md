---
layout: default
title: "Horizon Summary: 2026-11-24 (EN)"
date: 2026-11-24
lang: en
---

> From 45 items, 2 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Designing ChatGPT Apps: Know/Do/Show Framework](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Armin Ronacher and Mario Zechner on Coding With Agents](#item-ai-practitioner-2) ⭐️ 8.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Designing ChatGPT Apps: Know/Do/Show Framework](https://developers.openai.com/blog/what-makes-a-great-chatgpt-app) ⭐️ 8.0/10

OpenAI defines a ChatGPT app as a set of well-defined tools that perform tasks, trigger interactions, or access data, rather than a ported product UI. The framework evaluates value through three lenses: Know \(providing new context like live data or private metrics\), Do \(taking actions like creating records or triggering workflows\), and Show \(presenting structured UIs like charts or tables\). Developers should select a small set of capabilities mapped to specific jobs-to-be-done, using clear action names and structured outputs. Design must account for the model as a user by ensuring privacy-by-design, minimal required parameters, and stable schemas. Apps should function as part of an ecosystem, keeping actions small and outputs chainable for multi-app workflows.

rss · OpenAI Developer Blog \(Apify adapter\) · Nov 24, 12:00

**「Action」** Define app capabilities as discrete, clearly named operations \(e.g., search\_properties, create\_ticket\) that map to specific user outcomes, rather than exposing full product feature sets. Ensure each operation uses structured inputs and outputs to allow the model to route intent accurately and chain results with other tools.

**「Evidence and Limits」** The source provides a design framework and checklist but does not include performance benchmarks or comparative data against non-app interactions. It distinguishes between vague intent handling \(requiring clarifying questions\) and specific intent handling \(direct execution\), noting that users may disengage if forced into multi-step onboarding flows within chat.

**Tags**: `#agent-design`, `#tool-integration`, `#api-structure`, `#prompt-engineering`, `#product-strategy`

---

<a id="item-ai-practitioner-2"></a>
### [Armin Ronacher and Mario Zechner on Coding With Agents](https://www.aihero.dev/armin-ronacher-and-mario-zechner-on-coding-with-agents~fn8vd) ⭐️ 8.0/10

Armin Ronacher and Mario Zechner report that agents excel at verifiable tasks with clear oracles, such as test suites, but fail at ambiguous system design and API architecture. Mario states agents &quot;suck&quot; at tasks requiring domain knowledge or gut feeling. He uses adversarial review across different model families to mitigate individual model bias and laziness. Armin notes that verified code often becomes just another artifact for the agent to inspect rather than a fundamental constraint. Both developers emphasize that humans must retain understanding of the codebase to direct agents effectively.

rss · AI Hero · Nov 24, 08:52

**「Operator Takeaway」** Route agents to tasks with clear test-based oracles and use adversarial multi-model review for quality assurance. Retain human control for ambiguous architectural decisions and core code diffs.

**「Evidence and Limits」** Mario reports that reviewers in adversarial setups can get &quot;overzealous,&quot; requiring human judgment to filter findings. Armin observes that models lean towards defensive code, which may reduce long-term understandability. Neither developer claims to have found a definitive new engineering pattern for agent-based quality software creation.

**Tags**: `#agent-coordination`, `#quality-assurance`, `#workflow-design`, `#model-routing`

---