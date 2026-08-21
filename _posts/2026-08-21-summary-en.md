---
layout: default
title: "Horizon Summary: 2026-08-21 (EN)"
date: 2026-08-21
lang: en
---

> From 140 items, 3 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Multi-agent workflow for Three.js game development](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [DeepSeek Pro verifies code details better than Gemini 3.7 in legacy codebases](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Prototype JSON API for browser automation using Bun.WebView](#item-ai-practitioner-3) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Multi-agent workflow for Three.js game development](https://www.reddit.com/r/ClaudeCode/comments/1vtv818/i_claude_coded_a_multiplayer_threejs_tank_game/) ⭐️ 8.0/10

The developer built a multiplayer Three.js tank game using Claude Code and Codex in a multi-agent pipeline. The repository includes an AGENTS.md file and subsystem instruction files to record rules for agents across sessions. Units are meters, seconds, and radians with a fixed 60 Hz step. Authoritative logic is deterministic. Vehicle development splits the fleet into bounded families. One agent owns a vehicle profile, implements geometry, runs checks, and generates screenshots. A separate critic reviews rendered tanks for proportions, clipping, and missing surfaces. An orchestrator reruns checks and commits only verified files. Agents also implemented fixed-step movement, suspension, armor, ballistics, WebSocket multiplayer, procedural vehicles, destructible props, UI, and performance probes. Trailer production used agents to stage battles, build camera paths, and record browser runtime at 60 fps.

reddit · r/ClaudeCode · /u/BasedKetsu · Aug 20, 20:34

**「Actionable practices for agent operations」** Store important decisions and agent rules in persistent repository files like AGENTS.md so fresh agents can resume work without chat history. Enforce strict file and Git worktree ownership to prevent concurrent agents from overwriting each other. Use a render-inspect-measure cycle for visual quality tasks instead of text-only tests. Define concrete invariants and executable failure conditions for every system to improve agent reliability.

**「Limitations and verification methods」** Text-only reviews missed warped proportions and camera problems that were obvious in screenshots. Visual quality verification required a proper render loop with visual comparison because standard tests do not work for this domain. The developer directed the architecture and made final calls while agents handled implementation and testing.

**Tags**: `#agent-orchestration`, `#context-management`, `#visual-regression`, `#workflow-design`, `#multi-agent-systems`

---

<a id="item-ai-practitioner-2"></a>
### [DeepSeek Pro verifies code details better than Gemini 3.7 in legacy codebases](https://www.reddit.com/r/ChatGPTCoding/comments/1vtttzk/deepseek_pro_vs_gemini_37_for_a_real_complex/) ⭐️ 8.0/10

The author tested DeepSeek Pro and Gemini 3.7 on a large, messy production codebase with PHP, Python/FastAPI, and Nuxt components. The goal was repository archaeology: identifying current implementation, legacy code, and documentation drift. DeepSeek Pro naturally verified details by following call paths, checking exact methods, and running tests. It found cases where documentation did not match code. Gemini 3.7 formed a coherent mental model quickly but inferred implementation details rather than verifying them. The author applied a structured &\#x27;forensic analysis&\#x27; prompt to Gemini that forced contradiction hunting and evidence auditing. This improved Gemini&\#x27;s scores, but it still occasionally filled in reasonable but incorrect implementation details. DeepSeek Pro maintained higher accuracy in verification without special prompting.

reddit · r/ChatGPTCoding · /u/Maamriya · Aug 20, 19:43

**「Actionable guidance」** Use DeepSeek Pro for initial analysis of unfamiliar, complex codebases to leverage its natural verification loop. If using Gemini 3.7, apply a forensic workflow prompt that explicitly requires contradiction search, evidence audit, and disproving own conclusions before reporting.

**「Scope and limitations」** This evaluation measures repository archaeology and architecture understanding, not code implementation ability. The author notes Gemini 3.7 may still outperform in tasks with exact scope and contracts. The test involved a single specific codebase and fresh sessions for each model.

**Tags**: `#model-comparison`, `#prompt-engineering`, `#codebase-analysis`, `#agent-workflow`, `#verification-strategy`

---

<a id="item-ai-practitioner-3"></a>
### [Prototype JSON API for browser automation using Bun.WebView](https://simonwillison.net/2026/Aug/20/bun-webview-json-api/) ⭐️ 7.0/10

Simon Willison built a prototype JSON API for browser automation using Bun 1.4&\#x27;s new Bun.WebView feature. The implementation loads web pages and executes JavaScript against them, inspired by the shot-scraper CLI tool. Testing with cgroups showed the service requires 192MB-256MB of RAM to run a full Chrome instance against complex web pages.

rss · Simon Willison - Coding Agents · Aug 20, 15:37

**「Actionable insight」** Use Bun.WebView for lightweight browser automation tasks where memory usage must stay under 256MB per instance.

**Tags**: `#browser-automation`, `#bun`, `#resource-optimization`, `#agent-infrastructure`, `#webview`

---