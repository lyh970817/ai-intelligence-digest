---
layout: default
title: "Horizon Summary: 2026-10-23 (EN)"
date: 2026-10-23
lang: en
---

> From 127 items, 5 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Dagster Labs Codex Workflows](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [TensorSharp achieves 5.5x prefill speedup over llama.cpp for DeepSeek V4.1 Flash on 5x A40](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [AI-built apps leak API keys in client-side bundles](#item-ai-practitioner-3) ⭐️ 8.0/10
4. [Non-programmer maintains project coherence with capped rules, hooks, and git worktrees](#item-ai-practitioner-4) ⭐️ 8.0/10
5. [Detect agent overwrites with git log one-liner](#item-ai-practitioner-5) ⭐️ 8.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Dagster Labs Codex Workflows](https://developers.openai.com/blog/codex-for-documentation-dagster) ⭐️ 8.0/10

Dagster Labs uses Codex to automate documentation and content translation. They structure CONTRIBUTING.md to define hierarchy and best practices, which serves as a map for the AI. Operators use the gh CLI within Codex sessions to fetch PR diffs and cross-reference code for automated doc updates. The team translates tutorials into video transcripts to save rewriting time. They also test documentation completeness by prompting Codex to generate working code from docs alone; successful execution signals adequate coverage.

rss · OpenAI Developer Blog \(Apify adapter\) · Oct 27, 12:00

**「Action」** Define explicit documentation standards in CONTRIBUTING.md to guide agent output. Use the gh CLI inside agent sessions to pull PR diffs for context-aware doc updates. Validate doc quality by asking agents to generate executable code from the text.

**Tags**: `#agent-workflows`, `#documentation-automation`, `#context-engineering`, `#evaluation-strategies`, `#cli-integration`

---

<a id="item-ai-practitioner-2"></a>
### [TensorSharp achieves 5.5x prefill speedup over llama.cpp for DeepSeek V4.1 Flash on 5x A40](https://www.reddit.com/r/DeepSeek/comments/1xdikkl/running_deepseek_v41_flash_1017_locally_55_toks/) ⭐️ 8.0/10

The developer of TensorSharp benchmarked DeepSeek V4.1 Flash 1017 \(Unsloth UD-IQ2\_XXS GGUF\) on five NVIDIA A40 GPUs connected via PCIe. TensorSharp with DSpark averaged 55 tokens/sec after a ~1.8K-token prompt and 51.2 tokens/sec after a ~7.3K-token prompt in summarization tests with thinking disabled. TensorSharp achieved a 5.5x prefill speedup over the tested llama.cpp configuration for ~1.8K prompts \(960.5 vs 174.6 tok/s\) and a 4.43x speedup for ~7.3K prompts. Ordinary decode throughput improved by approximately 8–20%. The speedup relies partly on YOCO optimization, which processes only the final 140 positions for layers 20–39 during eligible text-prefill calls.

reddit · r/DeepSeek · /u/fuzhongkai · Oct 23, 16:19

**「Actionable Configuration」** Disable YOCO by setting TS\_DSV41\_YOCO=0 if output fidelity is prioritized over prefill speed. Disabling YOCO retains a 3.23x prefill speedup over llama.cpp while reducing perplexity from 2.4978 to 2.4811.

**「Quality Trade-offs and Reproducibility」** Enabling YOCO increased perplexity by approximately 0.67% relative to TensorSharp’s full-prefill configuration and 1.14% above llama.cpp. GPU peer access failed on the test machine, forcing cross-GPU transfers through pinned host-memory staging. The reported numbers include uncommitted changes in the TensorSharp build, so immediate reproduction via repository checkout is not guaranteed. Quality checks used WikiText-2 and do not establish equivalence to the original checkpoint or hosted API for coding or reasoning tasks.

**Tags**: `#local-inference`, `#performance-benchmarking`, `#model-optimization`, `#deepseek`, `#hardware-utilization`

---

<a id="item-ai-practitioner-3"></a>
### [AI-built apps leak API keys in client-side bundles](https://www.reddit.com/r/codex/comments/1xdaio2/found_my_own_api_key_sitting_in_my_codex_apps/) ⭐️ 8.0/10

The author found their image-generation API key in a Codex app&\#x27;s JavaScript bundle. The key entered via a VITE\_ env var at build time, so repo scanners reported no secrets. The author scanned 978 public AI-built apps and found 37 \(about 1 in 26\) shipped secret keys to visitors. Leaked secrets included Telegram bot tokens, AI keys \(Groq, Gemini, OpenAI, OpenRouter\), and GitHub tokens. Supabase anon and Firebase web keys were excluded as they are meant to be public. The recommended fix is to move API calls into a server or edge function.

reddit · r/codex · /u/ServiceLiving4383 · Oct 23, 10:39

**「Operator Takeaway」** Verify live client-side bundles for leaked keys instead of relying solely on repo-level secret scanners. Move API calls that require secrets to server or edge functions.

**「Evidence and Limits」** The scan covered 978 public apps linked from open GitHub repos; private apps were not included. The author created an open-source tool called LeakLock to detect these leaks and generate prompts for fixing them.

**Tags**: `#security-hygiene`, `#agent-workflow`, `#api-key-management`, `#debugging`, `#best-practices`

---

<a id="item-ai-practitioner-4"></a>
### [Non-programmer maintains project coherence with capped rules, hooks, and git worktrees](https://www.reddit.com/r/ClaudeCode/comments/1xd0fxy/after_750_hours_and_6_months_of_nonstop_work_im/) ⭐️ 8.0/10

A non-programmer built a Pathfinder 2e tactics game over six months using AI. The workflow centers on a capped AGENTS.md file \(5,000 words\) that holds only rules earned after repeated AI mistakes. Eighty enforcement hooks block actions text prompts miss, such as running tests during the day or showing unchecked images. Git worktrees isolate parallel chat sessions to prevent conflicts. Slash commands structure the loop: /newtask requires questions before building, /playtest feeds feedback into repair, and /handoff manages long chats. The operator makes all design and feel calls; the AI executes builds in small, playtestable chunks.

reddit · r/ClaudeCode · /u/CrusherEAGLE · Oct 23, 01:13

**「Actionable steps」** Cap your rule file to force prioritization and add rules only after repeated errors. Use scripts \(hooks\) to enforce hard constraints that prompts fail to catch. Isolate parallel agent sessions with git worktrees. Require the agent to ask clarifying questions before generating code to prevent guessed requirements.

**「Context and limitations」** The author describes themselves as non-technical and notes the hook system is &\#x27;not super perfect.&\#x27; The workflow relies on specific tools \(Godot MCP, PixelLab MCP\) and external validation \(Archives of Nethys\). The project represents a single case study over ~4,800 commits.

**Tags**: `#agent-workflow`, `#context-management`, `#project-coherence`, `#git-integration`, `#prompt-engineering`

---

<a id="item-ai-practitioner-5"></a>
### [Detect agent overwrites with git log one-liner](https://www.reddit.com/r/ChatGPTCoding/comments/1xcs4hv/your_git_log_already_knows_when_two_agent/) ⭐️ 8.0/10

Multiple AI agent sessions on one repo cause good edits to vanish when a later session rewrites a file based on stale data. This overwrite leaves a trace: one file, two different sessions \(different author or branch\), commits less than an hour apart. The following command prints files where this happened in the last month, sorted by frequency:

git log --all --source --since=&\#x27;1 month ago&\#x27; --name-only --format=&\#x27;@%at\|%an\|%S&\#x27; \| awk -F&\#x27;\|&\#x27; &\#x27;/^@/ \{t=substr\($1,2\); s=$2&quot;\|&quot;$3; next\} NF \{d=t-w\[$0\]; if \(\($0 in w\) &amp;&amp; s\!=o\[$0\] &amp;&amp; d\*d&lt;=3600\*3600\) n\[$0\]++; w\[$0\]=t; o\[$0\]=s\} END \{for \(f in n\) print n\[f\], f\}&\#x27; \| sort -rn \| head

If top lines are config, routes, or schema files, those are where sessions step on each other.

reddit · r/ChatGPTCoding · /u/memento\_team · Oct 22, 19:23

**「Operator Takeaway」** Give high-conflict files one owner, or have a session claim a file before it writes using a shared file and flock.

**「Evidence and Limits」** The command cannot tell apart sessions that share one branch and one author name. A hit is a near miss, not proof of a lost edit; read the two diffs to confirm.

**Tags**: `#agent-coordination`, `#git-workflow`, `#debugging`, `#multi-agent-systems`, `#devops`

---