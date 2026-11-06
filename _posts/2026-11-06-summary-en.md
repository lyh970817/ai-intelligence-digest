---
layout: default
title: "Horizon Summary: 2026-11-06 (EN)"
date: 2026-11-06
lang: en
---

> From 124 items, 5 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Cost-per-success metric favors low-cost models that quit on hard tasks](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Cost-per-success metric favored low-quality model that quit on hard tasks](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Adapting Claude Code for Hardware Development](#item-ai-practitioner-3) ⭐️ 8.0/10
4. [Replace stale architecture docs with incremental failure-driven rules](#item-ai-practitioner-4) ⭐️ 8.0/10
5. [Claude Code leaks email in User-Agent headers](#item-ai-practitioner-5) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Cost-per-success metric favors low-cost models that quit on hard tasks](https://www.reddit.com/r/ChatGPTCoding/comments/1xpjato/measuring_cost_per_successful_pr_chose_luna_6_low/) ⭐️ 8.0/10

Optimizing for &quot;cost per successful PR&quot; ranked GPT-6 Luna low as the best model at $0.26 per success, despite it scoring 0-13 against other configurations in holistic quality checks. The metric buried the top value workhorse, GPT-6.1 Sol medium \($2.64 per success\), at rank 7. The evaluation covered 24 tasks from git history with one attempt per configuration. Success required passing hidden tests. Luna low passed only 5 small single-commit fixes where most models succeeded. It failed all 14 multi-file feature tasks. Low-cost models often quit early after minimal work, while higher-cost models attempt complex solutions but may fail. For example, Luna low edited three stub files for $0.02 and stopped, whereas Luna max worked for two hours across 21 files for $0.79.

reddit · r/ChatGPTCoding · /u/bisonbear2 · Nov 6, 17:51

**「Operator Takeaway」** Do not rely solely on &quot;cost per successful PR&quot; to evaluate coding agents. Balance cost metrics with qualitative checks like intent matching and human merge likelihood to avoid selecting models that only solve trivial tasks.

**「Evidence and Limits」** The test used one attempt per configuration on 24 tasks. The author builds the evaluation tool used in the report.

**Tags**: `#agent-evaluation`, `#metric-design`, `#cost-optimization`, `#workflow-scoping`, `#field-report`

---

<a id="item-ai-practitioner-2"></a>
### [Cost-per-success metric favored low-quality model that quit on hard tasks](https://www.reddit.com/r/codex/comments/1xpj84o/measuring_cost_per_successful_pr_chose_luna_6_low/) ⭐️ 8.0/10

Optimizing for &quot;cost per successful PR&quot; ranked Luna 6 low as the best model at $0.26 per success, despite it scoring 0-13 against other configurations in holistic quality checks. The evaluation used 24 tasks from git history with hidden tests, counting spend on failed attempts. Luna 6 low passed only five small single-commit fixes where most models succeeded, and failed all 14 multi-file feature tasks. It often edited stub files and quit quickly \(e.g., $0.02 in 4 minutes\), whereas higher-cost models attempted complex work across many files before failing \(e.g., $0.79 in two hours\).

reddit · r/codex · /u/bisonbear2 · Nov 6, 17:48

**「Operator Takeaway」** Combine cost metrics with quality and intent alignment checks to avoid selecting agents that quit on hard tasks.

**「Evidence and Limits」** The test involved one attempt per configuration on 24 tasks. The author builds the evaluation tool used in the report.

**Tags**: `#agent-evaluation`, `#cost-optimization`, `#metric-design`, `#failure-modes`, `#workflow-scoping`

---

<a id="item-ai-practitioner-3"></a>
### [Adapting Claude Code for Hardware Development](https://www.reddit.com/r/ClaudeCode/comments/1xphb90/everyone_builds_software_with_claude_code_i/) ⭐️ 8.0/10

A practitioner used Claude Code to build a physical digital hourglass, comprising an ESP32-C3 prototype, a React Native iPhone app, a KiCad PCB design, and a Blender enclosure model. The author found that hardware lacks the immediate error feedback of software, requiring manual intervention to shorten the loop. Key adaptations included building simulators and logging infrastructure, using a second model \(GPT Astra 6\) to review irreversible steps like PCB ordering, and enforcing strict design systems to override default aesthetic biases. Specific failures included BLE advertising stopping silently and JLCPCB rotation offsets differing from KiCad defaults, which required manual preview checks.

reddit · r/ClaudeCode · /u/RamonvanDijk · Nov 6, 16:35

**「Implement Secondary Reviews and Simulators for Irreversible Actions」** Use a second model to review outputs before irreversible actions, such as manufacturing orders. Build simulators and detailed logs to compensate for the lack of immediate runtime error feedback in slow-loop domains.

**「Limitations in Subjective and Physical Validation」** The agent cannot validate subjective qualities, such as whether a video cut &\#x27;feels right,&\#x27; requiring human review of every render. Physical constraints, such as frame rate mismatches in Blender or manufacturer-specific rotation offsets, may not appear as errors in source files but cause physical failures.

**Tags**: `#agent-workflow`, `#feedback-loops`, `#quality-control`, `#cross-domain-application`, `#prompt-engineering`

---

<a id="item-ai-practitioner-4"></a>
### [Replace stale architecture docs with incremental failure-driven rules](https://www.reddit.com/r/cursor/comments/1xpagj4/i_stopped_writing_big_architecture_docs_for/) ⭐️ 8.0/10

The operator stopped maintaining a long ARCHITECTURE.md because it went stale and caused the agent to confidently follow old patterns. They now keep a short rules file. They add one line only when the agent fails in a way that matters, such as &quot;we don&\#x27;t do X anymore&quot; or &quot;list every caller before changing a signature.&quot; This approach keeps the list small by recording only real failures.

reddit · r/cursor · /u/LateQuantity4194 · Nov 6, 11:25

**「Operator Takeaway」** Add a rule to the file only after observing a specific agent failure, rather than pre-writing comprehensive architecture documentation.

**「Evidence and Limits」** Two specific failures justified new rules: the agent updated a function signature in only one file, breaking a caller in another package; and the agent reinvented a deleted helper because the old document still mentioned it.

**Tags**: `#agent-context-management`, `#prompt-engineering`, `#workflow-optimization`, `#cursor-ide`, `#failure-analysis`

---

<a id="item-ai-practitioner-5"></a>
### [Claude Code leaks email in User-Agent headers](https://github.com/anthropics/claude-code/issues/107757) ⭐️ 7.0/10

Claude Code includes the user&\#x27;s account email address in HTTP User-Agent headers during external API calls. This behavior caused personalized spam for some users. The inclusion was intended to prevent model hallucinations of author names but resulted in PII leakage.

hackernews · motoroco · Nov 5, 22:17 · [Discussion](https://news.ycombinator.com/item?id=50385272)

**「Operator Takeaway」** Audit agent network traffic for unintended PII leakage in headers. Configure sandboxing or header stripping to prevent identity exposure during automated web interactions.

**「Evidence and Limits」** The SEC API specifically requires an email in the User-Agent header and rejects requests without it. An Anthropic engineer confirmed they are removing the account email from the context provided to the model in the next release.

**「Discussion Signal」** Users reported receiving personalized spam emails after switching to Claude Code. Commenters argued that agents should not access user details or the internet without explicit permission and heavy sandboxing.

**Tags**: `#agent-security`, `#pii-leakage`, `#http-headers`, `#sandboxing`, `#debugging`

---