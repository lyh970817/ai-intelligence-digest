---
layout: default
title: "Horizon Summary: 2026-08-14 (EN)"
date: 2026-08-14
lang: en
---

> From 113 items, 4 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Bladebro: Rust-based agent browser for token efficiency and bot detection evasion](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Bounded step counts cause models to hide scope in final plan step](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Enforce hard round caps and diff-only context for reviewer agents](#item-ai-practitioner-3) ⭐️ 7.0/10
4. [Enforce ASD-STE100 in claude.md to simplify output](#item-ai-practitioner-4) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Bladebro: Rust-based agent browser for token efficiency and bot detection evasion](https://www.reddit.com/r/DeepSeek/comments/1vo9j2s/an_agent_browser_that_actually_allows_your_agent/) ⭐️ 8.0/10

The author released Bladebro, an open-source Rust binary that replaces high-token browser tools like Playwright MCP. It uses five core tools with ~1,900 tokens of definitions, compared to 13,700 for Playwright. Actions return only changes, reducing a click event from ~2,000 tokens to ~60. The tool supports batched commands, allowing multiple actions in one call. It implements structural fingerprinting to maintain element references across DOM re-renders. Bot detection evasion includes Bezier mouse paths, real movement deltas, micro-tremors, log-normal typing cadence, and GPU spoofing via lspci. The author tested it on Zillow and Fiverr without blocks. It does not solve Cloudflare Turnstile or captchas, returning a blocked verdict instead.

reddit · r/DeepSeek · /u/Opening\_Library9560 · Aug 14, 14:56

**「Actionable step」** Install Bladebro via npm to replace Playwright MCP for web-agent tasks requiring lower token usage and higher reliability against bot detection.

**「Evidence and limitations」** Token counts and reliability claims come from the author&\#x27;s testing. The tool fails on Cloudflare Turnstile and captchas, requiring external solvers. It does not support browser extensions. Binaries are available for macOS, Windows, and ARM64 Linux.

**Tags**: `#agent-tooling`, `#token-efficiency`, `#web-automation`, `#reliability-engineering`, `#bot-detection`

---

<a id="item-ai-practitioner-2"></a>
### [Bounded step counts cause models to hide scope in final plan step](https://www.reddit.com/r/ChatGPTCoding/comments/1vo4fam/i_ran_the_same_planning_prompt_over_10_app_ideas/) ⭐️ 8.0/10

The author ran a planning prompt with a bounded number of steps over 10 app ideas. In 8 of the 10 plans, the final step was named &quot;polish&quot; or &quot;final touches&quot; but contained real work, such as a request counter, copy to clipboard, order status tracking, team reports, or an entire dashboard. The model folded work that did not fit inside the step cap into the last step under a vague name instead of dropping it or reporting the overflow.

reddit · r/ChatGPTCoding · /u/SSShken · Aug 14, 11:17

**「Action」** Check two things on any model-generated plan: whether the last item is heavier than the ones before it, and whether anything mentioned in the original description is missing from every step title.

**Tags**: `#agent-planning`, `#prompt-engineering`, `#output-review`, `#scope-management`, `#failure-modes`

---

<a id="item-ai-practitioner-3"></a>
### [Enforce hard round caps and diff-only context for reviewer agents](https://www.reddit.com/r/codex/comments/1vo4opi/whats_your_actual_stopping_rule_when_one_agent/) ⭐️ 7.0/10

A multi-agent workflow with a coding agent and a reviewing agent failed to terminate naturally. The reviewer found new issues in each round, including previously requested changes and self-written comments, leading to five rounds on a pagination helper. The operator killed the process and shipped the version from round two. The reviewer lacks a concept of &quot;good enough&quot; and will always find something. The operator now enforces a hard cap of three rounds. The operator also restricts the reviewing agent&\#x27;s context to the code diff only, excluding conversation history, to prevent arguing with prior reasoning.

reddit · r/codex · /u/Upset-Day9099 · Aug 14, 11:30

**「Operator Takeaway」** Set a hard round cap \(e.g., three rounds\) for reviewer agents. Limit the reviewer&\#x27;s input to code diffs only, excluding conversation history.

**「Evidence and Limits」** The three-round cap is an arbitrary number picked by the operator. The operator uses coldtea-ai, which enforces a four-round cap. The finding is based on a single instance involving a pagination helper.

**Tags**: `#agent-workflows`, `#multi-agent-review`, `#stopping-criteria`, `#context-management`, `#workflow-optimization`

---

<a id="item-ai-practitioner-4"></a>
### [Enforce ASD-STE100 in claude.md to simplify output](https://www.reddit.com/r/ClaudeCode/comments/1vnqfrk/i_saw_everyone_asking_how_to_fix_claude/) ⭐️ 7.0/10

The author added a constraint to their \`claude.md\` file. The added text reads: &quot;\#\# Communication style Use ASD-STE-100 when you speak to the operator.&quot; The author states this change is working for them.

reddit · r/ClaudeCode · /u/Necessary\_Abroad6632 · Aug 13, 23:11

**「Action」** Add the instruction &quot;Use ASD-STE-100 when you speak to the operator&quot; to your project&\#x27;s \`claude.md\` file to enforce Simplified Technical English.

**Tags**: `#prompt-engineering`, `#communication-style`, `#system-instructions`, `#clarity`, `#agent-workflow`

---