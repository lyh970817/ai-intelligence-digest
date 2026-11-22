---
layout: default
title: "Horizon Summary: 2026-11-22 (EN)"
date: 2026-11-22
lang: en
---

> From 24 items, 2 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Design ChatGPT Apps as Scoped Toolkits](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Use LLMs to generate deterministic diagnostic scripts](#item-ai-practitioner-2) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Design ChatGPT Apps as Scoped Toolkits](https://developers.openai.com/blog/what-makes-a-great-chatgpt-app) ⭐️ 8.0/10

ChatGPT Apps function as toolkits the model orchestrates, not mini-versions of existing products. Developers should select a small set of capabilities that address specific jobs-to-be-done rather than porting full navigation hierarchies. Value derives from three patterns: Know \(providing new context or live data\), Do \(taking actions in external systems\), and Show \(presenting structured or visual UIs\). Effective apps use clear, unambiguous action names and parameters to reduce model routing errors. Outputs must be stable and structured to allow chaining with other tools in the ecosystem.

rss · OpenAI Developer Blog \(Apify adapter\) · Nov 24, 12:00

**「Actionable Implementation Steps」** Define a handful of concrete operations tied to specific user outcomes instead of exposing entire feature sets. Use straightforward parameter names and require only minimal, structured inputs. Ensure outputs include stable IDs and clear field names to support multi-app workflows.

**「Constraints and Evaluation」** Apps must handle vague intents by asking limited clarifying questions and specific intents by parsing queries directly without redundant setup. Developers should evaluate performance using a test set of positive, negative, and edge cases to measure the win rate against base ChatGPT responses.

**Tags**: `#agent-tool-design`, `#context-scoping`, `#model-routing`, `#structured-output`, `#workflow-orchestration`

---

<a id="item-ai-practitioner-2"></a>
### [Use LLMs to generate deterministic diagnostic scripts](https://github.com/sebaandrada-cell/PcapAnalyzer) ⭐️ 7.0/10

Practitioner tonyarkles reports using LLMs to write &quot;doctor&quot; scripts instead of repeatedly feeding raw data files to the model. This approach encodes lessons learned into automated test scripts. The operator runs these scripts against telemetry files instinctively, regardless of whether an issue is suspected.

hackernews · sebaandrada · Nov 21, 22:09 · [Discussion](https://news.ycombinator.com/item?id=50594132)

**「Actionable workflow change」** Replace repeated interactive analysis of raw telemetry with a step where the LLM generates deterministic diagnostic scripts. Run these scripts automatically on new data files to detect known issues without additional token costs.

**「Community corroboration and concerns」** User amanverasia shares a similar tool \(estudely-packet-explorer\). User tuckerpo notes a similar internal project at CableLabs that focused on reactive self-fixing but failed to gain traction. User rkagerer raises a privacy concern regarding whether AI features perform bidirectional redaction of sensitive capture data like IPs and MACs.

**Tags**: `#agent-workflow`, `#cost-optimization`, `#automation-pattern`, `#diagnostic-scripting`

---