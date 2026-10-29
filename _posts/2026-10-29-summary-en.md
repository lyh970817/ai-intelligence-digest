---
layout: default
title: "Horizon Summary: 2026-10-29 (EN)"
date: 2026-10-29
lang: en
---

> From 121 items, 4 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Agentic development shifts effort to modeling and breaks CI stability](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Global config and handoff protocol cut token burn in long sessions](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Interrogate Agent Code Changes Instead of Reviewing Quality](#item-ai-practitioner-3) ⭐️ 8.0/10
4. [Shift AI coding from chat UI to CLI for automation](#item-ai-practitioner-4) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Agentic development shifts effort to modeling and breaks CI stability](https://martinfowler.com/rachels-ramblings/good-devs-wary.html) ⭐️ 8.0/10

Thoughtworks senior engineers spent a week letting agents write all code for an airline application. The team reached 80% completion but faced constant red builds. Humans spent roughly two-thirds of their time at the whiteboard defining domain models and boundaries, and one-third building verification harnesses like tests and pipelines. Agents generated code faster than checks could finish, often working in parallel and stepping on each other’s changes. The product owner committed more feature code than any engineer. DORA’s 2025 research links AI adoption to higher throughput but lower delivery stability.

rss · Thoughtworks and Martin Fowler · Oct 29, 13:50

**「Actionable shift」** Shift operator effort from writing code to domain modeling and building verification harnesses. Redesign CI/CD pipelines to handle larger batch sizes and parallel agent changes without losing build trust.

**「Context and limits」** The experiment pushed agentic development to its limits and did not solve all CI stability issues. The team ran the experiment twice with different groups but did not settle on final practices. The source distinguishes this from using coding assistants; it addresses letting agents do all execution.

**Tags**: `#agentic-workflow`, `#ci-cd-stability`, `#verification-harness`, `#domain-modeling`, `#batch-size-management`

---

<a id="item-ai-practitioner-2"></a>
### [Global config and handoff protocol cut token burn in long sessions](https://www.reddit.com/r/ClaudeCode/comments/1xih978/i_worked_in_one_giant_session_all_day_hit_90_of/) ⭐️ 8.0/10

The author hit 90% of their weekly token limit with three days left after working in one giant session all day. Every message re-reads the entire context, so long sessions pay for the same history repeatedly. The author built a global setup in ~/.claude to manage this. It includes hooks that warn at 120k, 180k, and 250k tokens, and when the cache is likely cold. Another hook truncates test, build, and lint output to failures and summaries. A status line shows model, context size, and cache state. A /handoff skill runs tests, commits, and writes HANDOFF.md. The user then clears the session and continues in a fresh one using that file. Saying &quot;I&\#x27;m done for today&quot; triggers this flow. A /project-status skill provides quick updates without starting new work. Global CLAUDE.md rules enforce grep before reading files, short command output, specific model choices for tasks, and auto-compaction at 200k tokens. The author reports lower burn rates but has not measured them properly.

reddit · r/ClaudeCode · /u/IronbornV · Oct 29, 11:22

**「Action」** Adopt a handoff protocol: commit work, write a HANDOFF.md summary, clear the session, and continue in a fresh session to reset context costs.

**「Limitations」** The hooks are tested on fake transcripts, not much in real use yet, so expect rough edges. The 55-minute cold-cache threshold is a guess. The reported reduction in burn rate is observational and not properly measured.

**Tags**: `#context-management`, `#cost-control`, `#agent-workflow`, `#session-hygiene`, `#prompt-engineering`

---

<a id="item-ai-practitioner-3"></a>
### [Interrogate Agent Code Changes Instead of Reviewing Quality](https://www.reddit.com/r/codex/comments/1xic8ut/dont_review_agent_code_interrogate_it/) ⭐️ 8.0/10

The author stopped reviewing agent-generated code for quality after observing that cross-reviewing agents created an &quot;efficient LGTM machine&quot; that approved over-engineered solutions. The new workflow treats the reviewer agent as a witness to extract facts, not opinions. Step 1: Prompt a fresh agent to list exact changes \(schema, jobs, features, dependencies\) without judging code quality. Step 2: Identify vague justifications in the report, such as unrequested tables or generic abstractions. Step 3: Interrogate the agent with specific constraints it lacks, such as product scope or future plans, to force justification for every addition. Unjustified elements are cut.

reddit · r/codex · /u/EstablishmentGood414 · Oct 29, 06:18

**「Actionable Step」** Replace standard code review prompts with a fact-extraction prompt that lists schema changes, new dependencies, and modified features explicitly forbidding quality judgments. Use the resulting list to question the necessity of any item not directly requested in the original task.

**「Context and Limits」** The author applied this method for about one year. The approach relies on the operator knowing the product context and constraints, which the agent lacks. It does not replace manual testing or security reviews but targets scope creep and over-engineering specifically.

**Tags**: `#agent-workflow`, `#code-review`, `#prompt-engineering`, `#scope-management`, `#over-engineering`

---

<a id="item-ai-practitioner-4"></a>
### [Shift AI coding from chat UI to CLI for automation](https://www.reddit.com/r/ChatGPTCoding/comments/1xia3b2/if_youre_only_using_ai_coding_tools_in_the_chat/) ⭐️ 7.0/10

Many AI coding tools offer a command-line mode that returns output to stdout. This allows operators to script calls, capture responses, and chain steps. The author moved from interactive chat to CLI to automate tasks, run tools on a schedule, and wrap calls in validation logic. Scripts reject bad output instead of shipping it blindly. Config files enforce limits and rules before each run. The shift changes the mental model from treating AI as a coworker to treating it as a composable Unix tool.

reddit · r/ChatGPTCoding · /u/Firm-Builder-2001 · Oct 29, 04:12

**「Start with a simple CLI script」** Write a short script that sends a prompt to the AI tool&\#x27;s CLI, captures the response, and writes it to a file. Check documentation for headless, print, or non-interactive flags.

**Tags**: `#automation`, `#cli-workflows`, `#agent-orchestration`, `#validation-patterns`

---