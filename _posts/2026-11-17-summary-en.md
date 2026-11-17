---
layout: default
title: "Horizon Summary: 2026-11-17 (EN)"
date: 2026-11-17
lang: en
---

> From 52 items, 1 important content pieces were selected

---

**AI Practitioner Intelligence**
1. [Deterministic Simulation Testing](#item-ai-practitioner-1) ⭐️ 8.0/10

---

## AI Practitioner Intelligence

<a id="item-ai-practitioner-1"></a>
### [Deterministic Simulation Testing](https://martinfowler.com/articles/deterministic-simulation-testing.html) ⭐️ 8.0/10

Deterministic simulation testing replaces real clocks, networks, and storage with simulated components driven by a single-threaded execution loop. This approach ensures reproducibility by eliminating sources of nondeterminism such as wall-clock time, thread scheduling, and unseeded randomness. The technique uses logical &quot;ticks&quot; for timeouts and strict coding rules to maintain determinism, including banning system clock calls and unordered collection iteration. This deterministic harness allows operators to use LLMs to generate executable fault-injection tests from natural language descriptions or diagrams.

rss · Thoughtworks and Martin Fowler · Nov 17, 14:33

**「Operator Takeaway」** Use the deterministic simulation harness to prompt LLMs to convert natural language fault scenarios or whiteboard diagrams into executable test code.

**「Evidence and Limits」** The core protocol logic must follow six strict coding rules: no system clock calls, no unseeded randomness, no threads or standard futures, no direct I/O, no iteration over unordered collections, and no cross-thread callbacks across the seam. Violating these rules breaks replayability. Production adapters handle real I/O on background threads but must queue completions for the main tick loop to avoid data races.

**Tags**: `#distributed-systems`, `#testing-strategy`, `#llm-workflows`, `#deterministic-simulation`, `#agent-harnesses`

---