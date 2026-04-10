---
layout: post
title: "Introducing PM-DELTA: Context Construction as a Research Discipline"
date: 2026-04-10
description: "AI writes 10x code per day, but humans can only review 2-3 PRs. The bottleneck isn't model capability -- it's context construction. PM-DELTA is our answer."
tags: [pm-delta, ai, agents]
categories: [research]
giscus_comments: false
related_posts: false
---

## The Context Problem

AI coding tools have crossed a threshold. A single developer with Claude Code or Codex can produce more code in a day than a small team could write in a week. But production teams are not shipping ten times faster. Why?

The bottleneck is not model capability. It is *context construction* -- the work of decomposing a task into the right-sized units, assembling the relevant information each unit needs, and verifying the output meets real requirements. Software engineering has always been context construction: specs, docs, tests, and reviews exist to build shared understanding among collaborators. AI needs a different kind of context -- targeted, decomposed, and machine-verifiable.

Here is the core tension: AI produces 10x code volume per day, but humans can review 2-3 pull requests. Without structure, teams either throttle AI output (wasting capacity) or skip review (importing risk). Neither is acceptable.

## What PM-DELTA Is

[PM-DELTA](https://github.com/SII-DELTA/PM-DELTA) is an AI-native multi-project management framework built on three open tools: [Linear](https://linear.app) (task tracking), GitHub (code hosting), and [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (AI development).

The workflow is straightforward:

1. **Inbox** -- Drop meeting notes, research findings, or bug reports into the inbox. AI classifies intent, deduplicates against existing issues, and creates structured Linear issues with dependencies.
2. **Planning** -- Each task gets a targeted context package: relevant code, design constraints, acceptance criteria. A demand review validates *why* before design begins. Plan review validates *how* before implementation starts.
3. **Nightrun** -- Queued tasks are executed autonomously overnight through a 5-phase quality pipeline (plan, develop, review, fix, verify). Each phase has explicit gates. The team wakes up to reviewed pull requests, not raw code dumps.
4. **Review** -- Morning review surfaces what was built, what failed, and what needs human judgment. The system separates "ready to merge" from "needs discussion."

One workspace manages multiple projects. Role-based access (PI, PM, Student) ensures the right people see the right things.

### How PM-DELTA Differs

| Dimension | Cursor / Copilot | Devin / Codegen agents | PM-DELTA |
|-----------|-----------------|----------------------|----------|
| Scope | Single file | Single task | Multi-project, multi-task |
| Memory | None | Per-task | Persistent 3-tier learning |
| Quality | Human reviews all | AI self-reviews | Structured gates |
| Overnight | N/A | Single agent | Nightrun fleet, 5-phase pipeline |

## Three Mechanisms for Emergent Quality

PM-DELTA does not try to make AI "smarter." Instead, quality emerges from three mechanisms operating at different time scales:

**Structured Redundancy** (minutes). More compute per task yields more reliable output. Multi-agent planning generates and critiques approaches. Iterative review catches issues that single-pass generation misses. Gate-fix retry loops address failures before any human sees the code.

**Evolutionary Selection** (hours). Plan review and code review act as selection filters. Bad approaches are identified and discarded *before* they reach human reviewers. Failed approaches inform future decisions through explicit feedback capture. Over the course of a nightrun batch, the system converges on better solutions through this selective pressure.

**Compound Learning** (weeks). Team knowledge is captured in a persistent 3-tier system:

- **Rules** -- deterministic conventions enforced by code (formatting, naming, file organization)
- **Insights** -- accumulated patterns from development experience, refined automatically
- **Principles** -- design rationale and architectural decisions, referenced at planning time

This knowledge is retrieved at decision points, not just stored. Every session benefits from what previous sessions learned.

## The Autonomy Ladder

PM-DELTA provides a progressive autonomy model. Each level is independently useful -- teams adopt bottom-up at their own pace:

| Level | Mode | What It Means |
|-------|------|---------------|
| L0 | AI-Assisted | Industry baseline (autocomplete, chat) |
| L1 | AI-Driven, Human-Reviewed | Interactive development with structured review |
| L2 | AI-Autonomous with Gates | **Nightrun: autonomous execution with quality gates** |
| L3 | AI Fleet Execution | Parallel multi-task execution with coordination |
| L4 | AI Self-Planning | PM agent decomposes and schedules work |
| L5 | Hypothesis-Driven | Continuous knowledge compounding |

Today, L2 is fully operational in our lab. L3 is in active development. The key insight is that each level builds on the previous one -- you do not need L5 to get value from L2.

## The Self-Improving Flywheel

Here is what makes PM-DELTA different from a static tool: development friction feeds back as improvements to the framework itself.

When a nightrun task fails because the plan was underspecified, that failure becomes a new plan-review principle. When a code review catches a recurring pattern, it becomes a rule. When a team discovers a better way to structure context for a specific type of task, it becomes an insight.

The more projects use PM-DELTA, the better it gets. Each project's development experience -- its failures, fixes, and discoveries -- enriches the shared knowledge base. This is not aspirational; it is how we have been developing PM-DELTA itself for the past year.

## Try It

PM-DELTA is currently in private beta. We are looking for research labs and development teams who want to try structured AI-native project management.

- **GitHub**: [SII-DELTA/PM-DELTA](https://github.com/SII-DELTA/PM-DELTA) -- *currently in private beta; email lyk@sii.edu.cn for access*
- **Slides**: [PM-DELTA Overview (reveal.js)](/assets/slides/pm-delta-v2.html)
- **Video walkthrough**: *coming soon*

If you are interested in adopting PM-DELTA for your team, or if you want to contribute, reach out at lyk@sii.edu.cn.
