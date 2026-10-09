---
layout: default
title: "Horizon Summary: 2026-10-09 (EN)"
date: 2026-10-09
lang: en
---

> From 139 items, 5 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Session-Bench v1: 12 coding harnesses compared on session file fidelity](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Haiku 5.5, Sonnet 5.5, and Opus 5.5 subagent comparison on six real tasks](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [DeepSeek API rejects strict json\_schema with HTTP 400](#item-ai-practitioner-3) ⭐️ 7.0/10
4. [Hybrid voice-and-text workflow for Django feature development](#item-ai-practitioner-4) ⭐️ 7.0/10
5. [Optimize CLI --help for LLM agents](#item-ai-practitioner-5) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Session-Bench v1: 12 coding harnesses compared on session file fidelity](https://www.reddit.com/r/ChatGPTCoding/comments/1x1rkzl/sessionbench_v1_what_12_coding_harnesses_preserve/) ⭐️ 8.0/10

The author ran a single bug-fix task across twelve coding harnesses, three runs each. An outside witness recorded the live output, a ledger, and file hashes. A decoder read only the session files left on disk and compared 31 facts against the witness for a 100-point score. Eleven of twelve harnesses preserved full conversation fidelity. The 19-point spread came from storage efficiency and auditability. Pi stored the session in 19 KB with 100% unique events. OpenClaw used 697 KB with 0% unique events. Four harnesses \(DeepSeek Harness, Copilot CLI, OpenCode, Codex\) recorded token usage that added up to a stated total. Cursor CLI stored no token count. Antigravity and Cursor CLI stored protobuf inside SQLite with no published schema, making the sessions unreadable by standard tools.

reddit · r/ChatGPTCoding · /u/jazzy8alex · Oct 9, 17:33

**「Verify session artifacts before selecting a harness」** Check if your harness writes events only once and stores readable token counts. Paste raw session files into a model to estimate handover costs; inefficient storage inflates token counts significantly.

**「Scope and scoring constraints」** The test used one synthetic task on one machine. It did not evaluate long sessions, compaction, sub-agents, or crashes. The harnesses did not run the same model. Some scoring rules were written after the first captures, and three rules were waived or corrected after results were known. Reviews were done by separate AI agent sessions and outside model review, not by a second person.

**Tags**: `#agent-evaluation`, `#session-management`, `#cost-optimization`, `#debugging-workflow`, `#tool-selection`

---

<a id="item-ai-practitioner-2"></a>
### [Haiku 5.5, Sonnet 5.5, and Opus 5.5 subagent comparison on six real tasks](https://www.reddit.com/r/ClaudeCode/comments/1x1e7ts/i_tested_haiku_55_sonnet_55_and_opus_55_as/) ⭐️ 8.0/10

The author reran six tasks previously completed by Opus 5.5 using Sonnet 5.5 and Haiku 5.5 with high effort, same prompts, and same files. Results were checked against the real answer.

Code search \(find every file to change for a new feature; 48 files actually changed\): Opus found 45, Sonnet 44, Haiku 44. Costs: Opus $6.17, Sonnet $1.38, Haiku $0.44. The author judged quality the same and selected Haiku for price.

Web research \(three tasks checked against official rulebooks and Google help pages\): Wrong facts: Opus 1, Sonnet 3, Haiku 10. On Google Play account rules \(12 key facts\): Opus got 12 right, Sonnet 9, Haiku 5. Haiku could not open a league’s official rulebook PDF and used last season’s rules instead.

Fact-checking two blog posts before publishing: Real errors found: Opus 8, Sonnet 7, Haiku 4. Correct sentences wrongly marked as errors: Opus 0, Sonnet 6, Haiku 30. The author stated that following Haiku would have deleted half of a correct post.

Cost for all five web tasks: Opus $3.93, Sonnet $1.59, Haiku $0.12.

Current routing: Haiku for code search; Opus for research and fact-checking; Sonnet when small mistakes are OK.

reddit · r/ClaudeCode · /u/emarkosov · Oct 9, 06:39

**「Routing decision」** Route Haiku to code search, Opus to research and fact-checking, and Sonnet to tasks where small mistakes are acceptable.

**「Scope and limits」** Provisional field report based on six tasks in one project. The author asks whether Sonnet vs Opus results on research hold up, indicating uncertainty beyond this sample.

**Tags**: `#model-routing`, `#cost-optimization`, `#agent-evaluation`, `#fact-checking`, `#code-search`

---

<a id="item-ai-practitioner-3"></a>
### [DeepSeek API rejects strict json\_schema with HTTP 400](https://www.reddit.com/r/DeepSeek/comments/1x1n8x3/tested_deepseek_api_compatibility_tool_calling/) ⭐️ 7.0/10

A compatibility test against the official DeepSeek API using the deepseek-flash model found that Tool Calling and json\_object structured output passed 3/3 runs. Strict json\_schema requests consistently returned HTTP 400 errors. Chat Completions and SSE Streaming also passed all checks.

reddit · r/DeepSeek · /u/LeoW\_Builds · Oct 9, 14:44

**「Action」** Use json\_object mode for structured output with DeepSeek and validate the schema at the application layer. Avoid sending strict json\_schema requests to prevent HTTP 400 rejections.

**「Limitations」** The test involved only three runs from a single location in Shanghai. The author states these results do not prove universal or permanent lack of support for strict json\_schema. Latency figures are point-in-time observations and not suitable for provider comparisons.

**Tags**: `#api-compatibility`, `#structured-output`, `#model-routing`, `#deepseek`, `#integration-testing`

---

<a id="item-ai-practitioner-4"></a>
### [Hybrid voice-and-text workflow for Django feature development](https://simonwillison.net/2026/Oct/9/built-using-my-voice/) ⭐️ 7.0/10

Simon Willison built a Django &quot;Newsletters&quot; page using the ChatGPT desktop app \(Codex tab\) in voice mode. He started by typing &quot;Start dev server and open in browser&quot; to establish a visual preview. He then used voice chat while cooking to define a new model, migrations, view code, templates, and four import scripts \(Substack RSS, Substack undocumented API, public GitHub repo, private GitHub repo\). The model handled pagination logic and search integration based on vocal instructions. Willison switched to text-based prompting after creating a pull request to review the code. He replaced a subprocess Git call with an API-based import for the private repository and tweaked display details. The feature shipped after this text-based review phase.

rss · Simon Willison - Coding Agents · Oct 9, 12:54

**「Actionable workflow pattern」** Initialize coding agent sessions with a command that opens a local dev server preview. Use voice mode for high-level logic, UI tweaks, and multitasking. Switch to text mode for secure operations involving API keys or private repositories, and for precise debugging where pasting error messages or highlighting code is more efficient than verbal description.

**「Constraints and context」** The workflow relied on GPT-6 Astra High. Voice mode was effective for about 30 minutes of iterative development but required a switch to text for final security-sensitive adjustments. The author notes this approach is not a daily driver due to the inefficiency of describing specific code errors vocally and the social constraint of speaking aloud in shared workspaces.

**Tags**: `#voice-agents`, `#workflow-design`, `#code-review`, `#agent-handoffs`, `#developer-productivity`

---

<a id="item-ai-practitioner-5"></a>
### [Optimize CLI --help for LLM agents](https://ghuntley.com/tier/) ⭐️ 7.0/10

Geoffrey Huntley argues that optimizing CLI \`--help\` output and documentation for LLM agents reduces friction compared to using MCP or skill packs. He defines &quot;S-tier&quot; tools as those embedded in model weights, allowing direct CLI use without extra configuration. For new tools, he recommends optimizing \`--help\` text so models achieve outcomes with the fewest tool calls. The next step is publishing documentation optimized for Agentic Search Engine Optimization \(ASEO\), ensuring agents find all necessary information in a single web search. Finally, he suggests contracting with labs to include CLI documentation in future training runs.

rss · Geoffrey Huntley · Oct 9, 07:07

**「Action」** Measure whether an agent can achieve outcomes by walking the help verbs across all subverbs, then optimize the language to minimize tool calls.

**Tags**: `#cli-design`, `#agent-context`, `#developer-tooling`, `#prompt-engineering`, `#documentation`

---