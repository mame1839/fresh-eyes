# Fresh Eyes

A skill for pulling a second opinion from a fresh subagent — one that holds none of your current context — to break out of tunnel vision and self-justification mid-task.

An in-progress session quietly justifies the choices it has already made, seeing every piece of evidence and every remaining option through the filter of "the direction I've already picked." A subagent spun up fresh has nothing to defend, and can spot what you can no longer see.

Two layers: the **skill** decides *when and how to consult*; the **consultant subagent** carries *the manners of consulting* — lay out both sides, don't be sycophantic, don't read around on its own, question the root.

## Install

With [`npx skills`](https://skills.sh):

```sh
npx skills add mame1839/fresh-eyes
```

Global (all projects):

```sh
npx skills add -g mame1839/fresh-eyes
```

## Requirements

Needs a real subagent capability (the Agent / Task tool) — Claude Code, for example. It doesn't function where a consultant subagent can't be spun up.

## Layout

```
skills/
└── fresh-eyes/
    ├── SKILL.md                the skill: when and how to consult
    └── references/
        └── consultant.md       system prompt handed to the consultant subagent
```

`npx skills add` ships the whole skill directory, so `references/consultant.md` comes along with it. At call time the skill pastes that file into a fresh subagent to make it act as the consultant.

## Manage

```sh
npx skills list               # list installed skills
npx skills remove fresh-eyes  # remove
```
