---
layout: post
title: "Fractelier v3.0: Making the Scope the Subject"
date: 2026-06-23
description: "AI writes 10x the code a human can review. The fix isn't a faster model -- it's context construction. Fractelier v3.0 makes the code's own structure -- the scope tree -- the subject of the system."
tags: [fractelier, pm-delta, ai, agents]
categories: [research]
giscus_comments: false
related_posts: false
---

## The bottleneck moved, and we should follow it

AI coding tools crossed a threshold a while ago. With Claude Code, one person can
produce more code in a day than a small team used to write in a week. But teams
are not shipping ten times faster. The bottleneck is no longer model capability --
it is **context construction**: decomposing work into the right-sized units,
assembling the exact context each unit needs, and verifying the output against
real requirements. AI generates roughly 10x the code volume per day; a human can
still only review two or three pull requests. Without structure you either
throttle the AI or skip review. Neither is acceptable.

A year ago I argued this is a research discipline, not a tooling afterthought.
[Fractelier]({% comment %}<!-- PLACEHOLDER: fill in the public GitHub repo URL for Fractelier before publishing -->{% endcomment %})
-- the platform we built internally as PM-DELTA -- is our standing answer to it.
The name is *fractal + atelier*: a fractal workshop where masters and agents
collaborate. v3.0 is the version where the architecture finally matches the name.

## What changed in v3.0: the scope becomes the subject

In the 2.x line, the subject of the system was the **task** -- a Linear issue.
Everything orbited the task. That was the wrong center of gravity. Code does not
live in a task tracker; it lives in a tree of directories, each with its own
purpose, its own history, its own people. So in v3.0 the subject is the **scope**:
any directory carrying a `CLAUDE.md`. Tasks, events, and agents are now things
that *happen on* the scope tree, not the other way around.

Three ideas carry the weight.

**Fractal scope containers.** Each scope keeps its AI-context at its root and
collects everything else -- proposal, Linear slice, worktree and maintenance
config, issue and acceptance records -- in a `.scope/` container drawer. Three
invariants keep work at any depth from drowning in context: no scope inlines its
children's content, every proposal is self-contained, and Linear config never
inherits across a scope boundary. These are the human-facing analogue of the
tiered context-loading rules the agents already follow. You can work at a leaf
without paying for the whole tree.

**The Orchestration Map.** Underneath, the autonomous executor used to spread its
task graph across three stores that quietly drifted apart whenever tasks were
added at runtime -- the classic "writer A updated store X, writer B forgot store
Y" bug. v3.0 collapses them into one recursive structure that the orchestrator and
the dashboard both walk. There is no second view to drift to, so that whole class
of bug has no shape to take. Parallelism is governed by one rule -- scopes that
don't overlap run concurrently -- and "run these in order" simply emerges when
scopes do overlap. A run is a cursor over a persistent map, so crash recovery
becomes "open the map, walk the open frontier," and a sealed unit of work is never
re-attempted -- retry always appends new work.

**Knowledge that compounds.** The system keeps what it learns across runs in three
tiers: bitter lessons (root-cause records of real incidents), insights
(runtime-emergent patterns that get promoted as they prove out), and conventions
(stable architectural rules). At the start of every task, the relevant lessons and
insights are injected into that task's workspace. Each task begins from the memory
of every prior failure, not from a blank slate. That is the difference between a
system that resets each night and one that gets harder to fool over time.

## Does it actually run?

Yes -- unattended, every night, through a gated pipeline (plan, develop, review,
fix, verify) that branches and merges along the work graph and parks results for a
human morning pass. Over the most recent four-week window it averaged about **259
tasks completed per week**, with one full week reaching 445. (Full per-week
numbers will be published alongside the technical report; review-quality and
cost-per-PR figures need a GitHub-authenticated re-run, so I'm not quoting
numbers I haven't measured.) The team wakes up to reviewed, staged pull
requests, not a pile of raw diffs.

This is the concrete shape of one of the opportunities I keep coming back to: an
AI-enabled small team, developing through tight human-AI collaboration, can reach
an unusually high rate of creation in the right domain. Fractelier is the
infrastructure that lets us actually live in that regime instead of just talking
about it.

## What's next

The scope-rooted model has more to give: sparse, on-demand worktrees that expand
only the part of the tree a task touches, a VSCode Project Explorer that reads each
scope's own index, and preflight/postflight hooks that harden the existing review
backend. The codebase stays `pm-bot` until the v1 demo is stable; the public name
is Fractelier from here on.

If you want the architecture in depth, the technical report is here:
[Fractelier v3.0 Technical Report]({% comment %}<!-- PLACEHOLDER: fill in the public URL for docs/reports/fractelier-tech-report/report.pdf before publishing -->{% endcomment %}).
Questions and collaboration: **lyk@sii.edu.cn**.

*-- Yikang LI, SII | DELTA Lab*
