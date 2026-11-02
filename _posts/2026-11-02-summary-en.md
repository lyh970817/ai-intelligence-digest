---
layout: default
title: "Horizon Summary: 2026-11-02 (EN)"
date: 2026-11-02
lang: en
---

> From 113 items, 5 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [20 ways to waste fewer tokens in Codex](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Split AI coding agent rules into global user settings and local project files](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Astra edits Qwen weights to fix looping](#item-ai-practitioner-3) ⭐️ 8.0/10
4. [Force agent interview before planning](#item-ai-practitioner-4) ⭐️ 8.0/10
5. [Agent Interview Workflow for Project Briefing](#item-ai-practitioner-5) ⭐️ 8.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [20 ways to waste fewer tokens in Codex](https://www.reddit.com/r/codex/comments/1xm88mo/20_ways_to_waste_fewer_tokens_in_codex_from_basic/) ⭐️ 8.0/10

The author lists habits to reduce token waste and improve agent reliability. Define the task outcome, expected behavior, and verification method upfront. Include known edge cases early. Search for specific symbols before reading broadly. Run focused tests first. Attach relevant files or selections in the IDE instead of pasting whole modules. Start fresh chats for unrelated work. Keep the session start stable for reuse. Match the model to the task; cost per solved task varied 80x across GPT models for small, well-specified tasks. Use lower model\_reasoning\_effort for routine work if supported. Save CLI settings as profiles \(e.g., codex --profile routine\). Keep root AGENTS.md short and put specialist instructions in nested files. Use /compact after long detours. Disable web\_search for self-contained local work. Put repeatable environment setup in a setup script. Move occasional procedures into skills and disable implicit invocation via policy.allow\_implicit\_invocation: false. Trim MCP tools by disabling unused servers or specific tools. Use codex exec --output-schema for structured results and codex exec --json to track usage.

reddit · r/codex · /u/chrnas · Nov 2, 20:17

**「Operator Takeaway」** Define the task outcome and verification method upfront, attach only relevant files, and match the model to the task complexity to reduce token waste.

**「Evidence and Limits」** The author notes that tokens, API cost, and subscription quota are different measures. Savings are not guaranteed; compare whole tasks against the same definition of done, including retries. CLI settings described are not universal cloud or IDE controls. The 80x cost variance observation applies to the author&\#x27;s trials on small, well-specified tasks.

**Tags**: `#token-optimization`, `#agent-workflow`, `#context-management`, `#cost-control`, `#prompt-engineering`

---

<a id="item-ai-practitioner-2"></a>
### [Split AI coding agent rules into global user settings and local project files](https://www.reddit.com/r/cursor/comments/1xm83c6/how_i_stopped_reexplaining_the_same_stuff_to/) ⭐️ 8.0/10

The author split rules into two scopes to stop re-explaining preferences. Global user rules \(in settings\) remain tiny and stable. Local project rules \(in .cursor/rules\) hold repo-specific constraints like test commands or protected folders. The author moves a rule from local to global only after adding it to a second repo. This prevents the global base from bloating and being ignored.

reddit · r/cursor · /u/AgentPouchHQ · Nov 2, 20:12

**「Action」** Keep global user rules concise and move a rule there only when you catch yourself adding it to a second repository.

**「Limits」** The author reports that project rules grow over time, starting at four lines and reaching fifteen in a couple of weeks. Bloated global rules cause the agent to ignore half of them.

**Tags**: `#agent-configuration`, `#context-management`, `#prompt-engineering`, `#workflow-optimization`

---

<a id="item-ai-practitioner-3"></a>
### [Astra edits Qwen weights to fix looping](https://rikiyat.github.io/blog/weight-space-programming/) ⭐️ 8.0/10

Astra identifies and fixes looping failures in small Qwen models. The agent traces the failure to one direction written by the MLPs of layers 15 and 19. It subtracts that direction from 64 output columns in each layer, editing 131,072 weights. This intervention stops the model from repeating text and hitting token limits.

hackernews · dbreunig · Nov 2, 18:21 · [Discussion](https://news.ycombinator.com/item?id=50341174)

**「Operator Takeaway」** Use mechanistic interpretability tools to trace specific failure modes to weight directions. Edit those weights directly to repair the model without full retraining.

**「Evidence and Limits」** The source reports an 85 out of 96 failure rate for the base model before editing. The improvement claim of &\#x27;5x&\#x27; better math skills comes from a community comment, not the primary analysis summary. The workflow applies to small models.

**「Discussion Signal」** Commenters debate whether this ability is emergent or results from training on neural weights data. One user notes LLMs rapidly grasp complex systems like legacy codebases. Another expresses shock at the agent&\#x27;s ability to edit weights without tooling.

**Tags**: `#mechanistic-interpretability`, `#model-debugging`, `#weight-editing`, `#llm-reliability`, `#agent-workflow`

---

<a id="item-ai-practitioner-4"></a>
### [Force agent interview before planning](https://www.reddit.com/r/ChatGPTCoding/comments/1xm3e7e/before_your_agent_plans_anything_let_it_interview/) ⭐️ 8.0/10

Switch the agent to plan mode or read-only state. Instruct it to interview you one question at a time. Cover target users, definition of done, verification methods, existing assets, constraints, and out-of-scope items. Stop when the agent can write a one-page brief. Save this as BRIEF.md. Generate the implementation plan only after the brief is complete.

reddit · r/ChatGPTCoding · /u/chrnas · Nov 2, 17:24

**「Enforce single-question constraint」** Require the agent to ask exactly one question per turn during scoping. This prevents rushed answers and allows each response to shape the next question.

**「Scope management mechanics」** Define explicit acceptance criteria \(tests, commands, or visual checks\) in the brief. List out-of-scope items to prevent scope creep. Check new requests against the brief to classify them as in-scope, extensions, or direction changes. Place extensions on a &\#x27;later&\#x27; list.

**Tags**: `#agent-workflow`, `#prompt-engineering`, `#requirements-gathering`, `#scope-management`, `#context-building`

---

<a id="item-ai-practitioner-5"></a>
### [Agent Interview Workflow for Project Briefing](https://www.reddit.com/r/ClaudeCode/comments/1xm3ca3/before_your_agent_plans_anything_let_it_interview/) ⭐️ 8.0/10

Switch to plan mode \(Shift+Tab in Claude Code\) or instruct the agent not to edit files. Paste a prompt requiring the agent to interview the operator one question at a time. Cover target audience, definition of done, verification methods, existing assets, constraints, and out-of-scope items. Stop asking questions when enough information exists for a one-page brief. Write this brief to BRIEF.md, then generate the plan. Use the brief to evaluate new requests as inside scope, extensions, or changes of direction.

reddit · r/ClaudeCode · /u/chrnas · Nov 2, 17:22

**「Actionable Step」** Enforce a single-question-at-a-time constraint during initial scoping to prevent rushed answers and ensure each response shapes the next question.

**Tags**: `#agent-workflow`, `#prompt-engineering`, `#scope-management`, `#context-building`

---