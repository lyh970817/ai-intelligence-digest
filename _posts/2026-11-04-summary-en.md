---
layout: default
title: "Horizon Summary: 2026-11-04 (EN)"
date: 2026-11-04
lang: en
---

> From 124 items, 3 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [DeepSeek Super-agent benchmark flaws: under-configured baseline and high token costs](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Parallel Claude Code sessions in git worktrees port Black Ops II to Apple Silicon](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Cursor rule and SQL audit to prevent Supabase RLS bypass](#item-ai-practitioner-3) ⭐️ 8.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [DeepSeek Super-agent benchmark flaws: under-configured baseline and high token costs](https://www.reddit.com/r/DeepSeek/comments/1xnvcul/a_scheduling_benchmark_that_never_invoked_the/) ⭐️ 8.0/10

DeepSeek&\#x27;s Super-agent splits coordination from execution using a router session and separate worker sessions. The evaluation simulated coding with a time-consuming tool, measuring scheduling rather than code quality. The router-and-worker design achieved a 12.4 min median and 15.7 min p95 latency. The single-session baseline recorded 20.4 min median and 29.5 min p95. However, the neutral-prompt baseline never invoked a subagent in any of the five runs. A delegation-first prompt baseline reached 13.8 min median and 29.0 min p95. Token usage increased significantly: 23.2M cache-read tokens per run for the super-agent versus 6.1M for the baseline. Disabling direct pass-through raised usage to 31.8M tokens.

reddit · r/DeepSeek · /u/docdavkitty · Nov 4, 18:09

**「Verify baseline configuration and monitor token costs」** Ensure baseline agents are configured to delegate tasks when evaluating router-worker architectures. Neutral prompts may fail to trigger delegation, creating illusory performance gains. Monitor cache-read token volumes, as delegation patterns can increase usage from 6.1M to over 23M tokens per run.

**「Evaluation scope and constraints」** The test used four designs with five runs each. Each run contained about 300 messages, including roughly 20 work requests. The benchmark measured scheduling speed via a time-consuming tool, not code quality.

**Tags**: `#agent-architecture`, `#evaluation-methodology`, `#cost-optimization`, `#prompt-engineering`, `#benchmarking`

---

<a id="item-ai-practitioner-2"></a>
### [Parallel Claude Code sessions in git worktrees port Black Ops II to Apple Silicon](https://www.reddit.com/r/ClaudeCode/comments/1xnuufk/black_ops_ii_now_runs_natively_on_apple_silicon/) ⭐️ 8.0/10

A developer used parallel Claude Code sessions, each in its own git worktree, to port Black Ops II to Apple Silicon. Each session handled one problem. The author set goals and play-tested builds on a base M1. Claude wrote the LLVM passes that rewrite lifted x86, the hand-written Win32 runtime, and the D3D11-on-Metal renderer. The game runs natively at 60 fps. Performance relied on measurement: fps from presented frames and freezes from logs. Precompiling shaders cut the worst freeze from 7.0 s to 1.7 s. Two install bugs reported on GitHub were fixed and pushed the same day.

reddit · r/ClaudeCode · /u/GoldianSummer · Nov 4, 17:50

**「Actionable step」** Run parallel coding-agent sessions in separate git worktrees, assigning one problem per session.

**Tags**: `#agent-coordination`, `#workflow-optimization`, `#git-worktrees`, `#performance-debugging`, `#context-scoping`

---

<a id="item-ai-practitioner-3"></a>
### [Cursor rule and SQL audit to prevent Supabase RLS bypass](https://www.reddit.com/r/cursor/comments/1xn8kae/a_cursor_rule_file_for_supabase_projects_so_the/) ⭐️ 8.0/10

AI agents often resolve Supabase &quot;permission denied&quot; or &quot;row-level security policy&quot; errors by disabling Row Level Security \(RLS\), adding \`using \(true\)\` policies, or using the \`service\_role\` key in client code. These changes expose data to anyone with the public key. The author provides a \`.cursor/rules/supabase-security.mdc\` file that instructs the agent to never disable RLS, avoid \`using \(true\)\` or \`with check \(true\)\` on user data tables, tie policies to \`auth.uid\(\)\` and owner columns, require both \`using\` and \`with check\` for UPDATE policies, and restrict \`service\_role\` keys to server code. The rule requires the agent to show SQL and explain permissions before applying changes. The author also provides two SQL queries to audit tables with RLS off and policies that allow all rows, and advises checking DevTools Network headers for exposed secret keys.

reddit · r/cursor · /u/Round-Metal6269 · Nov 3, 23:23

**「Operator Takeaway」** Add the provided \`.cursor/rules/supabase-security.mdc\` content to your project and run the supplied SQL audit queries after migrations to verify RLS status and policy safety.

**「Evidence and Limits」** The author notes that Cursor docs state rules should not be the only security control. The author discloses they are building a scanner for this issue but does not link it, stating the rule file and SQL are the useful parts.

**Tags**: `#agent-constraints`, `#security-audit`, `#supabase`, `#cursor-rules`, `#rls`

---