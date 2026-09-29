---
layout: default
title: "Horizon Summary: 2026-09-29 (EN)"
date: 2026-09-29
lang: en
---

> From 122 items, 2 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Prevent coding agents from duplicating helper functions](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Sonnet 5.5 built a 30 s motion-graphics reel](#item-ai-practitioner-2) ⭐️ 8.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Prevent coding agents from duplicating helper functions](https://www.reddit.com/r/ChatGPTCoding/comments/1wtcxcq/coding_agents_write_a_new_helper_instead_of/) ⭐️ 8.0/10

Coding agents often write new helper functions instead of finding existing ones because writing is cheaper than searching. The author adds two instructions to prevent this. First, require the agent to search the codebase for an existing function before writing a new one. It must list findings and only write new code if nothing fits, explaining why. Second, run a review prompt after any session that added code. This prompt lists every new function or helper added, searches the codebase for similar behavior, and shows matches. Listing utility folders in the instructions \(e.g., &quot;date and money helpers are in src/utils&quot;\) also reduces duplication.

reddit · r/ChatGPTCoding · /u/Ok\_Negotiation\_2587 · Sep 29, 15:18

**「Enforce search-before-write and post-session review」** Add a rule to your agent instructions: search for existing functions before writing new ones. Save a review prompt that lists new functions and checks for duplicates after each coding session.

**「Effectiveness and scope」** The author states the review prompt finds duplicates more often than not, including cases missed in manual review. The workflow applies to both coding agents and chat interfaces like ChatGPT or Claude.

**Tags**: `#agent-workflow`, `#prompt-engineering`, `#code-quality`, `#duplication-prevention`, `#review-process`

---

<a id="item-ai-practitioner-2"></a>
### [Sonnet 5.5 built a 30 s motion-graphics reel](https://www.reddit.com/r/ClaudeCode/comments/1wtapu5/sonnet_55_built_a_30_s_motiongraphics_reel_same/) ⭐️ 8.0/10

A practitioner used Sonnet 5.5 with ultracode to generate a 30-second motion-graphics video entirely via code. The pipeline employed 14 agents: 5 builders each owned one scene file and avoided shared files; 5 independent reviewers rendered contact sheets, read PNGs, and returned structured defect lists; 4 fixer agents ran only where reviewers flagged issues. The process took 45 minutes and 618 tool calls. Verification relied on agents reading rendered images to catch bugs like negative radii and text overflow. File ownership was enforced by prompt instructions within a shared folder, not worktrees. The total cost was approximately $35.40 at Sonnet 5.5 list prices, compared to a calculated $50.50 for Opus 5.5.

reddit · r/ClaudeCode · /u/oxmannnn · Sep 29, 13:53

**「Operator Takeaway」** Enforce file ownership via prompt instructions in a shared workspace rather than using isolated worktrees, and require reviewer agents to render and read image outputs to detect visual bugs before final assembly.

**「Evidence and Limits」** The cost comparison is a calculation based on token profiles from the Sonnet session, not a direct run of Opus 5.5. The author notes that 99% of tokens were cache reads, making the actual price gap about 43% rather than 2x. The quality comparison is subjective and not a controlled test.

**Tags**: `#agent-orchestration`, `#visual-verification`, `#multi-agent-workflow`, `#code-generation`, `#debugging-strategy`

---