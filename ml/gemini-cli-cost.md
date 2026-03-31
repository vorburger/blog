---
title: "Calculating Gemini CLI Token Costs for Agentic Vibe Coding"
date: 2026-03-31
tags: ["ml"]
image: "/images/placeholder.png"
---

# Calculating Gemini CLI Token Costs for Agentic Vibe Coding

While [parallelizing AI workflows with background agents](../linux/terminal-bells.md) is a massive productivity booster, this "fire and forget" vibe coding introduces a new challenge: keeping track of your LLM API costs. If you want to quickly convert your terminal token usage into actual dollars, I highly recommend using this [Gemini CLI Cost Calculator](https://aish.li/cost/gemini-cli).

Using the Gemini CLI, you get a transparent summary of your token usage at the end of every session:

```text
│  Model                       Reqs   Input Tokens   Cache Reads  Output Tokens │
│  ──────────────────────────────────────────────────────────────────────────── │
│  gemini-2.5-flash-lite         12         73,086         1,950            674 │
│  gemini-3.1-pro-preview        93        363,946     4,728,671          9,516 │
│  gemini-2.5-flash              15         93,993        14,061          4,644 │
```

The trouble is, just like me, you probably want to know the actual **COST**, not just the raw token count. 

That's where [Aish.li's Gemini CLI cost tool](https://aish.li/cost/gemini-cli) comes in. You simply copy and paste the terminal output table above directly into the site, and it instantly calculates precisely what your session cost in real currency.

It's a very useful, purpose-built tool that takes the anxiety out of agentic coding. Now you can vibe without worrying about an unknown price tag at the end of the day.
