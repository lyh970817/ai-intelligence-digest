---
layout: default
title: "Horizon Summary: 2026-11-01 (EN)"
date: 2026-11-01
lang: en
---

> From 98 items, 3 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [6.1 Sol vs 6.1 Terra: Complementary Strengths in Architecture Tasks](#item-ai-practitioner-1) ⭐️ 8.0/10
2. [Anthropic Subscription Billing Mechanics and Model Value Analysis](#item-ai-practitioner-2) ⭐️ 8.0/10
3. [Karpathy builds HackerTube with Claude Code and Opus 5.5](#item-ai-practitioner-3) ⭐️ 7.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [6.1 Sol vs 6.1 Terra: Complementary Strengths in Architecture Tasks](https://www.reddit.com/r/codex/comments/1xl7y4b/61_sol_xhigh_vs_61_terra_max_a_complex_system/) ⭐️ 8.0/10

Terra finished the architecture task in 17.6 minutes, 1.57× faster than Sol’s 27.6 minutes. Terra maintained ~100 tok/s throughput across many small calls, while Sol slowed to ~28–29 tok/s during three large generation calls. Terra generated 4.7× more reasoning tokens and executed more commands \(128 vs 57\). Sol used roughly half the total tokens.

Terra excelled at discovery, finding five source-level defects and providing a clear evidence taxonomy. Sol produced a tighter working specification with named mechanisms, line anchors, file-change tables, and explicit rejection of 11 alternatives. The recommended workflow is to ship Sol’s blueprint as the base spec and graft in Terra’s qualification paragraph, risk list, and extra source leads.

reddit · r/codex · /u/ashokallu · Nov 1, 16:50

**「Workflow and Cost Strategy」** Use Terra for initial investigation and defect discovery, then use Sol to write the final structured specification. On subscription billing \(Codex credits\), Terra is both faster and cheaper due to lower per-token rates and no long-context surcharge. On pure API billing, Terra costs ~20% more because context accumulation triggers long-context surcharges.

**「Cost Mechanics and Limitations」** The cost difference depends on the billing model. Under API pricing, Terra cost $1.78 vs Sol’s $1.48 because 19 of Terra’s 50 calls crossed the 272K long-context threshold. Sol stayed just under this limit. Under Codex credits, Terra used fewer credits \(32.5 vs 37.1\) despite generating 88% more tokens, as its per-token credit rate is half that of Sol and lacks long-context surcharges. Terra’s output had almost no backticked identifiers, which reduces readability.

**Tags**: `#model-comparison`, `#agent-workflow`, `#cost-optimization`, `#architecture-design`, `#prompt-engineering`

---

<a id="item-ai-practitioner-2"></a>
### [Anthropic Subscription Billing Mechanics and Model Value Analysis](https://www.reddit.com/r/ClaudeCode/comments/1xki1qr/measuring_how_anthropic_bills_models_on_their/) ⭐️ 8.0/10

The author reverse-engineered Anthropic&\#x27;s subscription billing by parsing \`anthropic-ratelimit-unified-\*\` headers on a fresh Pro account. The quota model is: \`percent = Σ \(weight × tokens\) / budget\`. Key findings include: cache reads cost 0.025× \(half the API rate of 0.05×\), making them ~40% of total burn despite being free in some contexts; cache writes cost 1.25× regardless of TTL \(API charges 2× for 1-hour writes\); and output tokens cost 5× input tokens. Smaller models carry a markup relative to their API price ratio. Opus 5.5 offers the best value per dollar on subscriptions, while Haiku and Sonnet are more expensive per API dollar. No recent nerfs were detected aside from the end of a +50% weekly promo in September 2026.

reddit · r/ClaudeCode · /u/lambdita · Oct 31, 18:45

**「Optimize for Opus 5.5 and Cache Reads」** Route tasks to Opus 5.5 to maximize subscription value, as it has the lowest effective cost per API dollar compared to Haiku or Sonnet. Prioritize cache hits, as cache reads consume ~40% of the quota despite their low individual weight.

**「Methodology Constraints」** The analysis relies on rounding noise in whole-percent header readings, which provides hard bounds but requires thousands of samples. Concurrent requests can inflate perceived usage by 12–32% if every rise is summed; only new highs should be counted. The study used a specific mix of Claude Code-shaped requests and may not generalize to all workflow patterns. Fable model data was derived from an Ultra account.

**Tags**: `#cost-optimization`, `#model-routing`, `#cache-strategy`, `#subscription-analysis`

---

<a id="item-ai-practitioner-3"></a>
### [Karpathy builds HackerTube with Claude Code and Opus 5.5](https://karpathy.bearblog.dev/hacker-tube/) ⭐️ 7.0/10

Andrej Karpathy used Claude Code with Opus 5.5 to build and deploy HackerTube, a YouTube clone aggregating videos recommended on Hacker News. The agent downloaded HN comments, ran Sonnet in a workflow to filter spam, and identified 6,454 videos across 150 topics from 2007-2026. Karpathy manually created a Google Cloud API key, booted a VPS, and bought a domain. He then instructed the agent to update, deploy, secure, harden, and optimize the code on the VPS. The process took approximately two hours.

rss · Andrej Karpathy · Oct 31, 17:00 · [Discussion](https://news.ycombinator.com/item?id=50319510)

**「Delegate infrastructure tasks」** Provide the agent with VPS IP access and natural language commands to handle deployment, security hardening, and optimization instead of performing these tasks manually.

**「Manual dependencies」** The operator must still perform initial setup steps: creating API keys \(Google Cloud\), provisioning the VPS instance, and purchasing the domain name. The agent handles the rest once these resources are available.

**「Community extensions」** User \[aus\_\] reported deploying a HackerTube Android TV app to NVIDIA Shields using a single prompt to a Hermes agent. User \[theptip\] suggested using Haiku or Sonnet to filter and rank RSS feeds for similar disaggregation. User \[curiouscats\] recommended including video description text boxes.

**Tags**: `#agent-workflow`, `#claude-code`, `#rapid-prototyping`, `#infrastructure-automation`, `#data-pipeline`

---