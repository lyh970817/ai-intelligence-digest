---
layout: default
title: "Horizon Summary: 2026-11-19 (EN)"
date: 2026-11-19
lang: en
---

> From 45 items, 3 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Designing ChatGPT Apps as Scoped Toolkits](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Ship a 21,000-line feature with mattpocock/skills](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Disable Chrome On-Device AI via Enterprise Policy](#item-ai-practitioner-3) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Designing ChatGPT Apps as Scoped Toolkits](https://developers.openai.com/blog/what-makes-a-great-chatgpt-app) ⭐️ 8.0/10

OpenAI defines a ChatGPT app as a set of well-defined tools rather than a ported product UI. The model orchestrates these tools within conversations. Value derives from three capabilities: &\#x27;Know&\#x27; \(accessing live or private data\), &\#x27;Do&\#x27; \(taking actions like creating records or triggering workflows\), and &\#x27;Show&\#x27; \(presenting structured UIs like charts or tables\). Developers should select a small set of core jobs-to-be-done and expose them as concrete, narrowly scoped operations. Tool definitions require clear names, minimal required parameters, and stable, structured JSON outputs to enable model routing and multi-app chaining. Privacy by design dictates collecting only necessary fields and avoiding blob parameters.

rss · OpenAI Developer Blog \(Apify adapter\) · Nov 24, 12:00

**「Actionable Design Steps」** Replace broad feature ports with 3-5 specific, named operations \(e.g., search\_properties, create\_ticket\) that map to distinct user outcomes. Ensure each tool returns structured data with stable IDs and clear field names to support downstream model usage.

**「Scope and Constraints」** The guidance targets developers building for the ChatGPT platform using the Apps SDK and MCP servers. It emphasizes that apps function as part of an ecosystem where the model may call multiple tools in sequence, requiring outputs that other apps can consume. The source does not provide performance benchmarks or code samples, referring readers to separate developer docs for technical implementation details.

**Tags**: `#agent-tool-design`, `#function-calling`, `#prompt-engineering`, `#mcp`, `#workflow-scoping`

---

<a id="item-ai-practitioner-2"></a>
### [Ship a 21,000-line feature with mattpocock/skills](https://www.aihero.dev/watch-me-ship-a-21-000-line-feature-with-mattpocock-skills~ez95n) ⭐️ 8.0/10

The author shipped a 21,000-line feature using the &\#x27;Grill With Docs&\#x27; and &\#x27;Retro&\#x27; skills. The process began with &\#x27;grilling&\#x27;: a conversational phase to define the &\#x27;why&\#x27; and align domain language via a GLOSSARY.md file. This glossary served as the data model. The author used ADRs to preserve decision context. Prototyping occurred in a subagent to reduce decision space before implementation. The workflow separated &\#x27;Smart Zone&\#x27; \(high-context design\) from &\#x27;Dumb Zone&\#x27; \(low-context implementation\) to manage token costs and output quality. The author generated a spec and 47 user stories, then ran the &\#x27;Implement Spec&\#x27; skill AFK \(away from keyboard\). The resulting PR was split into stacked diffs, distinguishing reversible &\#x27;two-way doors&\#x27; from critical &\#x27;one-way doors&\#x27;. Human review focused on system improvements rather than line-by-line checks. The author identified patterns in agent errors and updated lint rules and documentation. Finally, the &\#x27;Retro&\#x27; skill analyzed session transcripts and review comments to root-cause failures, leading to ratcheted lint checks and doc fixes.

rss · AI Hero · Nov 18, 17:16

**「Actionable steps」** Maintain a GLOSSARY.md file to align domain language and data models before coding. Separate high-context design \(&\#x27;Smart Zone&\#x27;\) from low-context implementation \(&\#x27;Dumb Zone&\#x27;\) to control token costs. Split large PRs into stacked diffs, merging reversible changes first. Use retrospective analysis of agent sessions to update lint rules and documentation instead of just fixing code.

**「Context and constraints」** The prototype agent consumed ~260k tokens, entering the &\#x27;dumb zone&\#x27; where output quality degraded and costs increased. The author notes that auto-compaction is &\#x27;still a little dodgy&\#x27; but safe after converting conversation to a document. The workflow relies on saving session transcripts to disk for retroactive analysis. The author treats this as a provisional field report for one specific feature in the Course Video Manager repo.

**Tags**: `#agent-workflow`, `#context-management`, `#code-review`, `#prompt-engineering`, `#software-architecture`

---

<a id="item-ai-practitioner-3"></a>
### [Disable Chrome On-Device AI via Enterprise Policy](https://perishablepress.com/chrome-ai-wasting-much-bandwidth/) ⭐️ 7.0/10

Community members report that Chrome&\#x27;s on-device AI features cause high CPU usage and input latency. One user observed the &quot;On device&quot; process consuming 300% CPU, causing a one-second delay per keypress. Disabling the feature via standard settings did not persist. A contributor provided a JSON policy file method to permanently disable these features on Linux. Place the file at \`/etc/opt/chrome/policies/managed/disable\_ai.json\` for Chrome or \`/etc/chromium/policies/managed/disable\_ai.json\` for Chromium. The JSON content sets \`GenAiDefaultSettings\` to 2 and \`AIModeSettings\`, \`GeminiSettings\`, and \`GenAILocalFoundationalModelSettings\` to 1.

hackernews · speckx · Nov 19, 16:54 · [Discussion](https://news.ycombinator.com/item?id=50562636)

**「Apply JSON Policy File」** Create the specified JSON policy file in the managed policies directory to permanently disable Chrome on-device AI features when UI toggles fail to stop background processes.

**「Disputed Bandwidth Claims」** Commenters dispute the original article&\#x27;s claim that Chrome AI uses hundreds of GBs of bandwidth per month, calling it blog spam without logs. The confirmed issue is CPU contention and latency, not necessarily bandwidth exhaustion. The provided policy path applies to Linux systems.

**「Corroboration and Dissent」** User josephernest corroborates severe performance degradation \(300% CPU, input lag\) and notes that UI-based disabling does not prevent the process from returning. Users xnx and skullone reject the bandwidth waste claim due to lack of evidence. User edoceo reports similar slowdowns across other AI-integrated apps like VSCode and Android keyboards.

**Tags**: `#browser-configuration`, `#performance-tuning`, `#resource-management`, `#chrome-policies`, `#developer-workflow`

---