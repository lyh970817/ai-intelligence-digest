---
layout: default
title: "Horizon Summary: 2026-08-18 (EN)"
date: 2026-08-18
lang: en
---

> From 113 items, 3 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Align harness config to close provider performance gaps](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Disable codex-auto-review to stop token waste](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Claude Code injects dynamic &lt;total\_tokens&gt; tag with 15M per-turn reset](#item-ai-practitioner-3) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Align harness config to close provider performance gaps](https://www.reddit.com/r/DeepSeek/comments/1vrja31/same_deepseek_model_very_different_experience/) ⭐️ 8.0/10

The author compared DeepSeek V4 Flash 0731 across DeepSeek’s first-party API, InferX, and DeepInfra using the same machine and DeepSeek Harness setup. Initially, the first-party API provided a superior agent experience, while third-party providers appeared weaker. Debugging revealed two main configuration mismatches in the InferX setup. First, reasoning content streamed as ordinary text instead of into the separate Think box. Setting \`thinkingFormat: deepseek\` in the provider configuration resolved this, indicating a protocol compatibility issue rather than a model difference. Second, subagent tools like Claude Code were missing because the relevant backend \(\`@deepseek-ai/dsh-subagent-claude-code\`\) was not installed and mounted. After installing the backend and aligning the provider composition, the InferX setup behaved much more like the first-party endpoint. The apparent &quot;one-shot intelligence&quot; gap narrowed significantly once the harness exposed the same tools and system instructions.

reddit · r/DeepSeek · /u/Fwuzeem · Aug 18, 08:30

**「Set thinkingFormat and mount missing subagent backends」** Set \`thinkingFormat: deepseek\` in your provider configuration to ensure reasoning streams into the correct UI component. Install and mount missing subagent backends, such as \`@deepseek-ai/dsh-subagent-claude-code\`, to expose the full tool environment to the model.

**「Provisional field report with uncontrolled variables」** This is a provisional field report based on one user’s debugging session. The author notes that differences in quantisation, inference settings, chat templates, or sampling defaults may still exist between providers but were not tested. The comparison initially lacked identical system prompts, tool schemas, and backend integrations, making it an uncontrolled evaluation of model weights. The author plans to freeze the corrected harness configuration for a future controlled comparison.

**Tags**: `#agent-orchestration`, `#model-evaluation`, `#api-compatibility`, `#debugging-workflow`, `#provider-integration`

---

<a id="item-ai-practitioner-2"></a>
### [Disable codex-auto-review to stop token waste](https://www.reddit.com/r/codex/comments/1vr8pvh/i_found_the_culprit_eating_your_usage_limit/) ⭐️ 8.0/10

OpenAI silently enabled a &quot;codex-auto-review&quot; feature in Codex agent version 0.147.0 on August 7. This feature re-reads the entire conversation history to approve every agent action, such as running commands or editing files. The author measured 10.4 million tokens consumed in one week from 141 checks. A single check can cost up to ~195,000 tokens. The feature activates automatically without user configuration.

reddit · r/codex · /u/Stunning-Angle-9239 · Aug 17, 23:40

**「Check analytics and disable auto-approve」** Open https://chatgpt.com/codex/cloud/settings/analytics\#usage to check for &quot;codex-auto-review&quot; entries in local logs. Turn off auto-approve/review settings immediately to stop the token drain.

**「Source measurements and scope」** The data comes from a single user&\#x27;s logs over one week. The worst day saw 46 checks in 19 minutes, consuming 6.4 million tokens. The author links the behavior to GitHub release rust-v0.147.0 and PR \#36373.

**Tags**: `#cost-optimization`, `#agent-debugging`, `#openai-codex`, `#token-usage`, `#workflow-audit`

---

<a id="item-ai-practitioner-3"></a>
### [Claude Code injects dynamic &lt;total\_tokens&gt; tag with 15M per-turn reset](https://www.reddit.com/r/ClaudeCode/comments/1vrd6z8/a_total_tokens_tag_counting_up_to_15m_was_added/) ⭐️ 7.0/10

A dynamic &lt;total\_tokens&gt; tag appears in every model&\#x27;s system prompt in Claude Code. The tag starts at 15,000,000 for each new turn and decrements as tokens are consumed within that turn. It resets to 15,000,000 upon receiving a fresh user message or inbound notification. This value remains stable across sessions and models. The counter tracks a per-turn token allowance rather than context window remaining or session-lifetime usage.

reddit · r/ClaudeCode · /u/arthurlindao · Aug 18, 03:01

**「Action」** Treat the 15M limit as a per-turn spend budget ceiling enforced by the harness, not a context window constraint. Do not add this tag to agent frontmatter, as the harness loads it automatically.

**「Evidence and limits」** The author observed the counter drop from 15,000,000 to ~14,762,000 during a single long turn consuming ~240k tokens. Tokens consumed by background workflows after a turn ended did not reduce the next turn&\#x27;s starting value. The interpretation that this represents a harness turn-spend budget is flagged as inference by the source.

**Tags**: `#claude-code`, `#system-prompt`, `#token-budget`, `#agent-harness`, `#debugging`

---