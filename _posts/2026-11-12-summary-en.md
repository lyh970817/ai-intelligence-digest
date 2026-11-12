---
layout: default
title: "Horizon Summary: 2026-11-12 (EN)"
date: 2026-11-12
lang: en
---

> From 204 items, 6 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Field Report: Codex, Antigravity, and Muse Code on a Full-Stack Task](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Claude Code leaks Chrome profiles and orphaned processes](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Generated Glossary](#item-ai-practitioner-3) ⭐️ 8.0/10
4. [The Home Repo Pattern](#item-ai-practitioner-4) ⭐️ 8.0/10
5. [Sol 6.1 High overengineering caused 16-hour deployment failure](#item-ai-practitioner-5) ⭐️ 8.0/10
6. [Secure AI agents with Nix overlays and property-based testing](#item-ai-practitioner-6) ⭐️ 8.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Field Report: Codex, Antigravity, and Muse Code on a Full-Stack Task](https://www.reddit.com/r/ChatGPTCoding/comments/1xugdkv/i_tested_codex_google_antigravity_and_meta_muse/) ⭐️ 8.0/10

A developer tested Codex \(GPT-6.1 Sol\), Google Antigravity \(Gemini 4 Argon\), and Meta Muse Code \(Muse Wonder Full 1.0\) on a single TypeScript/Next.js full-stack task. Codex finished in ~28 minutes with 24.76M tokens and zero manual approvals. Antigravity took 3h 19m, used 50.85M tokens, and consumed 76% of a weekly Pro allowance. Muse Code took 2 hours, used 28.11M tokens, and required 68 manual approvals due to Windows sandbox ACL timeouts. Independent code inspection revealed architectural bugs in all three agents. Codex omitted submitted assignment states and had pagination issues. Muse Code and Antigravity both implemented hidden write side effects in read-only endpoints. Antigravity also risked false-positive academic classifications and processed entire rosters before pagination.

reddit · r/ChatGPTCoding · /u/PuzzleheadedFuture73 · Nov 12, 15:54

**「Required Action」** Perform independent code inspection on AI-generated implementations to catch semantic bugs like hidden write side effects and unsafe failure states that pass self-reported tests.

**「Context and Limitations」** This was a single-task, single-run comparison on one private codebase. Subscription prices were not equivalent \($100 Codex vs CAD$26.99 Antigravity\). Token accounting methods differed across providers. The code review was source-level and not blinded. None of the implementations were merged into production.

**Tags**: `#agent-evaluation`, `#model-routing`, `#code-quality`, `#token-optimization`, `#workflow-automation`

---

<a id="item-ai-practitioner-2"></a>
### [Claude Code leaks Chrome profiles and orphaned processes](https://www.reddit.com/r/ClaudeCode/comments/1xufdct/my_mac_ran_out_of_disk_i_asked_claude_what_was/) ⭐️ 8.0/10

The agent consumed 8.7 GB by creating 157 temporary Chrome profiles during screenshot checks and never removed them. It also left a headless Chrome process running for 27 hours. A subsequent run created 439 copies of the Chrome app, consuming about 2 GB of real disk space through block sharing. These resource leaks did not appear in code diffs or tests.

reddit · r/ClaudeCode · /u/Extra\_Aide5999 · Nov 12, 15:15

**「Enforce cleanup rules」** Add instructions to store profiles in a known folder and remove them in a finally block. Mandate that the agent kills started Chrome processes and moves files to trash instead of hard deleting them.

**「Scope and limitations」** This is a single-user field report on macOS. The author notes that standard code reviews and tests failed to detect the machine-level mess.

**Tags**: `#agent-reliability`, `#resource-management`, `#prompt-engineering`, `#debugging`, `#workflow-optimization`

---

<a id="item-ai-practitioner-3"></a>
### [Generated Glossary](https://martinfowler.com/bliki/GeneratedGlossary.html) ⭐️ 8.0/10

Martin Fowler proposes generating a domain-specific glossary to help LLMs handle specialized vocabulary. An LLM scans internal sources like documents, emails, and chat logs to identify single words and multi-word phrases. It flags terms that are new or used in unfamiliar ways. The LLM drafts definitions, noting alternative meanings based on context. Human experts review and amend the draft. The final glossary is stored in version control and refreshed on a schedule. Fowler advises against a single standard glossary for large organizations. Instead, maintain separate glossaries for different bounded contexts, such as source code versus human text. For large glossaries, inject only terms and links into the initial context, allowing the model to fetch full definitions via links as needed. Use the glossary to guide code generation, ensuring variable names match enterprise vocabulary. Include deprecated terms with advice on replacements.

rss · Thoughtworks and Martin Fowler · Nov 12, 14:15

**「Operator Takeaway」** Generate a domain glossary from internal texts using an LLM, validate it with human experts, and store it in version control. Inject only term lists and definition links into agent context to save tokens, letting the model retrieve full definitions on demand.

**「Evidence and Limits」** Fowler states he has never seen a single standard glossary work for large organizations. The method relies on sufficient internal text material; audio or video transcripts may be needed if text is scarce.

**Tags**: `#context-management`, `#domain-modeling`, `#agent-workflow`, `#token-optimization`, `#enterprise-ai`

---

<a id="item-ai-practitioner-4"></a>
### [The Home Repo Pattern](https://www.aihero.dev/the-home-repo-pattern) ⭐️ 8.0/10

The Home Repo Pattern consolidates agent skills, AGENTS.md, and shared docs into a single repository. Agents run from this home repo, which contains navigation pointers to other repositories. This setup allows agents to clone or access child repos as needed, providing a unified context for multi-repo projects without requiring a monorepo. The pattern solves fragmented agent context by keeping one copy of shared skills and steering files.

rss · AI Hero · Nov 12, 11:17

**「Operator Takeaway」** Paste the provided four-step prompt into a new agent session to inventory existing repos, deduplicate skills, and generate a Home Repo with AGENTS.md pointers. Run all future agent sessions from this new Home Repo directory.

**「Evidence and Limits」** The pattern handles ~20 repos well. At ~400 repos, use progressive disclosure by grouping pointers into area-specific files. At thousands of repos, a skills marketplace is preferred. Secrets like .env files remain in their original repos and are not moved. Code history and issue trackers stay in child repos.

**Tags**: `#agent-orchestration`, `#context-management`, `#multi-repo-workflow`, `#prompt-engineering`

---

<a id="item-ai-practitioner-5"></a>
### [Sol 6.1 High overengineering caused 16-hour deployment failure](https://www.reddit.com/r/codex/comments/1xu7cg0/sol_61_high_overengineering_turned_a_production/) ⭐️ 8.0/10

An operator used Sol 6.1 High as an orchestrator for a production deployment. The process took 16 hours and consumed over 90% of the ChatGPT Business subscription allowance. A technical audit found that more than 95% of the time was spent on self-imposed blockers, redundant validations, and recovery procedures. The deployment framework grew to over 50 modules, with the main script containing approximately 9,800 lines of Python. Eleven consecutive blockers required repeated code modifications. Five of six release changes fixed the deployment infrastructure itself, not the application. The system added custom SQL parsers, Python AST analysis, and cryptographic state bindings. The actual application build takes 25 seconds for frontend and backend, with an 80-second PostgreSQL backup. The orchestrator introduced additional abstractions and permanent safeguards for each edge case instead of simplifying the process.

reddit · r/codex · /u/real\_Paparider · Nov 12, 08:20

**「Enforce simplicity constraints」** Prefer simpler, maintainable solutions over accumulating defensive abstractions. Keep verification proportional to actual operational risk. Avoid converting one-time incidents into permanent architectural requirements. Detect and eliminate redundant validations. Recognize when acceptance criteria are satisfied and finish the task.

**「Scope and limitations」** This is a single-user report of one deployment event. The author notes that higher reasoning effort may reinforce overengineering behavior but states this experience alone cannot establish that claim. The application involved is relatively small.

**Tags**: `#agent-orchestration`, `#workflow-optimization`, `#cost-control`, `#failure-analysis`, `#prompt-engineering`

---

<a id="item-ai-practitioner-6"></a>
### [Secure AI agents with Nix overlays and property-based testing](https://ghuntley.com/answer/) ⭐️ 8.0/10

Geoffrey Huntley argues that securing AI agents requires traditional engineering rigor rather than more AI. He demonstrates using Nix overlays to patch dependencies and disable dangerous capabilities, such as removing \`git force-push\` support from the environment. This approach creates a single source of truth for developer laptops, CI/CD, agent sandboxes, and production images. Huntley also advocates for property-based testing \(using tools like Bombadil or Hegel\) and deterministic back-pressure checks to prevent agent loops from closing on bad code. He suggests generating small, well-specified utilities first-party instead of relying on open-source libraries to reduce supply chain risk.

rss · Geoffrey Huntley · Nov 11, 19:38

**「Operator Takeaway」** Use Nix overlays to monkey-patch underlying tools in agent sandboxes, removing unsafe capabilities like force-push at the system level. Implement property-based testing and static analysis hooks to enforce constraints and prevent agent loops from committing invalid code.

**「Evidence and Limits」** The author explicitly warns against running agents as root on production hosts or connecting them to production databases. The described workflow relies on Nix, which the author acknowledges has a reputation for being hard to use, though he claims agents mitigate this complexity. The demo code is available in a GitHub repository named \`nix-demo\`.

**Tags**: `#agent-safety`, `#nix`, `#property-based-testing`, `#dependency-management`, `#workflow-engineering`

---