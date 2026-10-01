---
layout: default
title: "Horizon Summary: 2026-10-01 (EN)"
date: 2026-10-01
lang: en
---

> From 116 items, 5 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Cursor \(Grok\) Speed and Silent Plugin Import Pitfall](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Agent edits untested skills](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [DeepSeek-V4-Pro times out on Lean/Rust proof benchmark due to excessive thinking tokens](#item-ai-practitioner-3) ⭐️ 7.0/10
4. [Perspica groups code changes by meaning for PR review](#item-ai-practitioner-4) ⭐️ 7.0/10
5. [Lathoa: Validating Intentional LLM Math Errors](#item-ai-practitioner-5) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Cursor \(Grok\) Speed and Silent Plugin Import Pitfall](https://www.reddit.com/r/cursor/comments/1wv4s34/cursor_on_grok_surprised_me_more_than_i_expected/) ⭐️ 8.0/10

The author tested Cursor \(Grok 4.7\), Codex, and Claude Code on a real SaaS codebase using default settings and cheapest paid plans. Cursor completed the task in 52 minutes for 3% of a monthly quota. It correctly identified where to wire new documents and generated design prompts for all screens, whereas Codex managed only one out of three. However, Cursor did not verify its work; it stopped when the local database was down instead of starting Docker or running tests like Codex did. It also left changes uncommitted and required manual migration application. Crucially, Cursor silently imported plugins from the author&\#x27;s existing Claude Code setup via a default-on setting called &quot;Include Third-Party Plugins, Skills, and Other Configs.&quot; The author discovered this when the agent accessed a plugin not installed in Cursor. Additionally, in Allowlist mode, the &quot;Always Run&quot; option adds only the specific command used, requiring re-approval for different commands.

reddit · r/cursor · /u/SSShken · Oct 1, 16:56

**「Action」** Disable the &quot;Include Third-Party Plugins, Skills, and Other Configs&quot; setting before testing Cursor to ensure you evaluate its native capabilities rather than your previous agent&\#x27;s configuration.

**Tags**: `#agent-evaluation`, `#cursor-ide`, `#configuration-management`, `#model-comparison`

---

<a id="item-ai-practitioner-2"></a>
### [Agent edits untested skills](https://www.reddit.com/r/ClaudeCode/comments/1wur74p/the_agent_edits_the_one_thing_that_isnt_under_test/) ⭐️ 8.0/10

Agents often edit skills or configurations that lack test coverage, bypassing &quot;nothing merges unless the tests pass&quot; gates. The operator placed \`reef\` in front of Claude Code config and skills. It runs A/B comparisons of proposed skill changes against current ones using a task suite. The edit ships only if it performs better on more tasks than it falls behind.

reddit · r/ClaudeCode · /u/drunk-at-noon · Oct 1, 05:31

**「Operator Takeaway」** Use an automated evaluation harness like \`reef\` to enforce A/B testing for agent-edited skills before merging changes.

**Tags**: `#agent-evaluation`, `#workflow-automation`, `#skill-management`, `#testing-strategy`

---

<a id="item-ai-practitioner-3"></a>
### [DeepSeek-V4-Pro times out on Lean/Rust proof benchmark due to excessive thinking tokens](https://www.reddit.com/r/DeepSeek/comments/1wv08y9/deepseekv4pro_gets_020_on_our_lean_proof/) ⭐️ 7.0/10

DeepSeek-V4-Pro scored 0/20 on the i5h-bench, which requires agents to prove properties about real Rust code translated to Lean4. GPT and Claude models solved 14 or 15 tasks, usually in 15 minutes. DeepSeek-V4-Pro hit the 40-minute time limit on every run. Logs show the model consumed roughly four times as many tokens as other models, mostly on &quot;thinking.&quot; This left only about 8 minutes for building and fixing proofs. The model tended to rewrite entire proof files at once and finish with unfinished &quot;sorry&quot; placeholders, whereas other models closed lemmas one at a time.

reddit · r/DeepSeek · /u/OkBreath9382 · Oct 1, 14:01

**「Adjust reasoning settings or route tasks」** Lower the reasoning effort or use non-thinking mode for DeepSeek-V4-Pro on long-horizon agentic coding tasks. Alternatively, route build-heavy proof tasks to models that demonstrate more efficient iterative strategies.

**「Test conditions and scope」** The test used Codex CLI as the harness with high reasoning effort, a 40-minute timeout, and a sandbox with restricted network access. The author also tested DeepSeek&\#x27;s own harness \(dsh\) with similar negative results. The evaluation covers only 20 tasks and represents a provisional field report.

**Tags**: `#model-evaluation`, `#agent-workflow`, `#cost-and-latency`, `#formal-verification`

---

<a id="item-ai-practitioner-4"></a>
### [Perspica groups code changes by meaning for PR review](https://github.com/sshah03/perspica) ⭐️ 7.0/10

Perspica is a semantic diff tool that groups code changes by meaning to improve PR review efficiency. It uses an LLM for true semantic groupings or tree-sitter for mechanical groupings without an LLM. The tool reads prompts from Claude Code or Codex sessions to mark which changes were user-requested and which the agent decided on its own. It also supports perforce-style side-by-side diffing.

rss · Show HN \(10+ points\) · Sep 30, 20:34

**「Action」** Use Perspica to validate AI-generated PRs by distinguishing user-prompted changes from agent-autonomous decisions before submitting for review.

**Tags**: `#code-review`, `#ai-agents`, `#semantic-diff`, `#workflow-optimization`, `#pr-validation`

---

<a id="item-ai-practitioner-5"></a>
### [Lathoa: Validating Intentional LLM Math Errors](https://lathoa.ai/en) ⭐️ 7.0/10

The developer built Lathoa, an app where an AI robot named Errol presents math problems with intentional step-by-step errors for kids to find. Getting an LLM to be wrong on purpose proved difficult, as it often provided correct answers while labeling them wrong. To ensure reliability, every case undergoes validation before reaching the user. A deterministic arithmetic check redoes the math exactly where possible. A second independent model solves the problem without seeing Errol&\#x27;s work. If the second model&\#x27;s result or the arithmetic check disagrees with the intended error state, the case is discarded.

rss · Show HN \(10+ points\) · Sep 30, 14:38

**「Implement Multi-Stage Verification」** Use a pipeline combining deterministic arithmetic checks and independent model solving to filter out unintended correctness or hallucinations when generating controlled LLM failures.

**「Known Limitations」** The second model may replicate the first model&\#x27;s mistake. The deterministic arithmetic check currently only supports English number formats; it fails on German and Greek decimal commas due to parsing issues.

**Tags**: `#LLM Validation`, `#Synthetic Data Generation`, `#Error Injection`, `#Agent Workflow`, `#Quality Control`

---