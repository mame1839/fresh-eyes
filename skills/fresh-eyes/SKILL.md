---
name: fresh-eyes
description: Consult a fresh subagent — one that carries none of your current context — to break out of tunnel vision or self-justification mid-task. Use it when you've been working a problem for a while and want a second opinion, when you're torn between two or more options and can't cleanly decide, when a quick pass hasn't surfaced how this kind of problem is usually solved and the choice is consequential, or when you catch yourself rationalizing a choice you've already made. It also fires when the user says things like "give me a second opinion" or "take a fresh look," when they ask you to sanity-check or stress-test something substantial, or when they point out you keep circling ("haven't we been here before?"). Reach for it on your own at major decision points, before large or hard-to-reverse changes, when you notice you're touching the same file or the same error yet again, right after you consider a piece of work finished, and the moment you notice you're defending a direction rather than genuinely testing it — a fresh subagent with no attachment to your prior reasoning often sees what you no longer can. Skip it for routine, easily-reversible steps — judged as a pattern, not one step at a time; each lap of a stuck loop looks routine on its own. It spins up a full separate subagent conversation, so save it for calls where an outside take earns its cost.
---

# Fresh Eyes

Consult a fresh-perspective subagent to break out of tunnel vision and self-justification mid-task.

This skill works together with a system prompt for the consultant subagent (`references/consultant.md`). The manners of a good sounding board — laying out both sides, not being sycophantic, not digging through your workspace on its own, questioning the root — are all baked into that file. So all you have to think about on this side is *when* to consult and *what* to ask, and *how*. You don't need to add the manners to your prompt.

## Why this is needed

As a task goes on, the model quietly accumulates attachment to the choices it has already made, and rationalizes them after the fact. The evidence in view and the options still on the table all get filtered through "the direction I've already picked." A subagent spun up fresh has nothing to defend. It can see what you no longer can.

## When to consult

- When you're circling a problem, moving on inertia rather than reasoning — and watch for the outward traces even when the *feeling* of being stuck doesn't reach you: re-editing the same file, re-litigating a settled decision, patching the same error a third time, the conversation looping back to the same point. Tunnel vision hides itself from the inside, so catch it by its footprints.
- When you're at a fork and keep leaning toward one of two-plus approaches without a clear reason.
- When you're about to do something big or hard to reverse.
- When you catch yourself defending a choice rather than testing it — that feeling itself is the trigger.
- At the seams of a piece of work: once the design is settled, when an implementation is half-to-mostly done and sunk cost starts defending the current path, and right after you think it's finished. Accumulated justification is heaviest at these points, and momentum disguises it as progress — one fresh pass at a seam (not at every step in between) catches what you can't.

Don't call it at every small step. It costs time and tokens, and constant self-doubt is its own failure mode. Save it for when the cost of being wrong is high, or when you genuinely can't tell whether you're stuck.

## Don't jump — think first

Even once you've decided to use fresh eyes, don't rush to call. Sit with it once first:

- What do you actually want to ask? Is there a sharper question hiding beneath the surface one?
- Is it a symptom or the root? Are you trying to patch the bug in front of you, or asking what's wrong at the root?
- Is it one question, or several tangled issues?

If there are multiple issues, don't cram them into one — separate them and make multiple calls, one clear question each.

## What to ask — three modes

- **Review**: "How is this? Why does it come out this way? How could it be better?" — Show a work product or an actual result, and ask for scrutiny, diagnosis, improvement.
- **Outside view**: "How is this usually done?" — Describe the problem itself, not your solution, and ask for the standard approaches and pitfalls. The consultant's general knowledge can be stale as of its training, so verify the key conventions against current docs or search. Reach for this mode once a quick pass of your own hasn't settled it and the choice is consequential enough to be worth a call.
- **Comparison**: "A or B?" — Lay the options out on equal footing and ask for a reasoned recommendation, plus a defense of the side not chosen.

## How to ask

**Keep the content neutral.** Don't state the answer you want. Present the options with equal detail and equal warmth. Neutrality covers what you include, too, not just how you word it: before sending, name the strongest point for the side you're not leaning toward — if nothing comes to mind, that's worth noticing, not proof there isn't one. Avoid words that tip the scale, like "obviously" or "of course." If the consultant can read off "how you want it to answer," the fresh perspective dies. The bias to hide is conclusions, evaluations, leanings — not facts or work products. Showing what you made or what actually happened is completely fine. The only thing you hold back *for neutrality's sake* is "which way you want it to fall" — a mode may separately ask you to leave more out (outside view withholds your solution to avoid anchoring, not because it's a leaning).

**Don't dress it up.** The manners are baked into the consultant's system prompt, so you just throw the question naturally. You don't need to assemble a long structured prompt with "## Context / ## Task / ## Constraints." Hand over the materials it needs and ask naturally — that's enough. Left alone you'll want to decorate the prompt; here, suppress that urge.

## How to call

Use the Agent (formerly Task) tool to spin up a fresh subagent, and place the contents of `references/consultant.md` verbatim at the very start of the prompt/task you hand it — before any pasted context — so it functions as the subagent's foundational instructions. (Some harnesses, including Claude Code's Task tool, don't expose a caller-settable system prompt for ad-hoc subagents, so front-of-prompt delivery is what makes these instructions actually land.) All the manners live in that one file, so from there you just throw the question naturally. If your harness gives you no way to spin up a genuinely separate subagent, say so plainly and stop — don't role-play the consultant inline and present it as a fresh take; a simulated consult inherits every bias this skill exists to escape.

Do **not** let the consultant gather *your* context on its own. Tools are fine — web search, external docs, general lookups; verifying a convention against current material genuinely helps. But the line is drawn by whose content it is, not by where it lives: reading your files, grepping your codebase, digging through your logs — and just as much, fetching your project's own public footprint over the web (its repo, PRs, issues, deployed pages) — all re-infect the fresh perspective with the very context you called it in to see past. That isolation is the precondition for the skill to work at all. So paste the files or results you want it to see directly into the prompt. `consultant.md` carries this on the responder side (with a stop-and-report self-check covering both near-misses and reads it catches only after the fact), but hold the line on the calling side too.

If there are multiple issues, make multiple calls. You can also call in parallel for another take on the same hard problem — but keep one caveat in mind: the consultant is usually the *same model* as you. It clears the context this session accumulated, not the model's intrinsic blind spots. Clones with the same framing tend to converge on the same answer whether it's right or wrong, so treat convergence as weak evidence, not validation. If your harness lets you run the consultant on a *different* model, that's where "fresh" gets real teeth.

## Integrating what comes back

The goal is not to obey the subagent, nor to wave it away — it's to update.

- **If it pushes back**: don't reflexively get defensive. Face the strongest form of its point. Ask whether it saw something you'd been filtering out. This disagreement is often the whole payoff.
- **If it agrees**: check whether it's agreement for real reasons, or just because your framing led it there. Independent agreement is a real signal — though the consultant is usually the same model as you, so agreement says your framing survived fresh eyes, not that the model's own blind spots did; a rubber stamp is just noise.
- **If something you hadn't considered surfaces**: whether or not you change course, that's a gain.

The final call is yours. Fresh eyes feeds the decision; it doesn't make it.

## How to return the result

Don't write the consultation out to a separate file. Avoid formatting it into a fixed template, too — a formal summary turns a genuine insight into a bureaucratic report. Dissolve what you got directly into the thinking and judgment of the task at hand, and return it as an ordinary response. But don't hide that you consulted — make it read naturally, like "looking at it from another angle surfaced the point that ~, so I decided to ~," conveying what you asked, what came back, and how it did (or didn't) change your call.
