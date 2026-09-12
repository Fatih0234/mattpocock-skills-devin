# mattpocock-skills for Devin

[Matt Pocock's agent skills](https://github.com/mattpocock/skills) — "Skills for Real Engineers" — packaged as a **native Devin plugin**. Works across the Devin CLI, Devin Desktop, and (for skills; subagent profiles are local-only today) cloud sessions.

Skills install as namespaced slash commands: `/mattpocock-skills:<name>`.

## Install

```bash
devin plugins install Fatih0234/mattpocock-skills-devin

# or from a local checkout (linked — edits apply next session)
devin plugins install --local ./mattpocock-skills-devin
```

Then, once per repo where you want the engineering flows, run:

```
/mattpocock-skills:setup-matt-pocock-skills
```

It configures the issue tracker (GitHub / GitLab / local files), triage label vocabulary, and domain doc layout that `to-spec`, `to-tickets`, `triage`, `wayfinder` and `code-review` read.

## The flows

The main flow: **idea → ship**. `/mattpocock-skills:ask-matt` is the built-in router if you forget where you are.

```
grill-with-docs → to-spec → to-tickets → implement (tdd + code-review) → commit
```

- **`/mattpocock-skills:grill-with-docs`** — relentless interview that sharpens the idea and leaves a paper trail (`CONTEXT.md` glossary + ADRs)
- **`/mattpocock-skills:to-spec`** / **`/mattpocock-skills:to-tickets`** — turn the thread into a spec, then tracer-bullet tickets with blocking edges
- **`/mattpocock-skills:implement`** — builds each ticket test-first, ends with `/mattpocock-skills:code-review`
- **`/mattpocock-skills:triage`** / **`/mattpocock-skills:wayfinder`** — on-ramps: inbox of raw issues, or huge foggy efforts mapped as decision tickets
- **`/mattpocock-skills:improve-codebase-architecture`** — codebase health: scans for deepening opportunities, renders an HTML report, grills the one you pick

Plus standalone tools: `grill-me`, `research`, `prototype`, `diagnosing-bugs`, `resolving-merge-conflicts`, `wizard`, `handoff`, `teach`, `to-questionnaire`, `wait-what`, `writing-for-agents`.

## Devin-native adaptations

Same behaviors, Devin mechanics:

- **Real subagent profiles** in `agents/` — upstream says "spawn a sub-agent" in prose; here those are actual `run_subagent` calls against named profiles:
  - `researcher` — read-only-ish investigator (web + codebase + findings-file writes) behind `research`, `grilling` fact-finding, `wayfinder` research tickets, `design-it-twice`, and `improve-codebase-architecture`'s codebase walk
  - `standards-reviewer` + `spec-reviewer` — `code-review`'s two axes, spawned in parallel so neither pollutes the other's context
- **Fully-qualified invocations** — every `Call the Skill tool` uses `mattpocock-skills:<name>` so cross-skill edges resolve under plugin namespacing
- **`triggers: [user]`** on the 14 user-invoked skills, alongside upstream's `disable-model-invocation: true` (both honored by Devin)
- **No plugin `AGENTS.md`** — upstream's contains repo-authoring conventions (changelog rules, em-dash bans) that would otherwise inject into *your* sessions as an always-on rule
- `agents/openai.yaml` kept per skill — harmless here, keeps the tree loadable by other harnesses via [skills.sh](https://skills.sh/mattpocock/skills)

## Layout

```
.devin-plugin/plugin.json    # manifest; skills array mirrors the promoted set
skills/engineering/          # 18 skills
skills/productivity/         # 7 skills
agents/                      # 3 custom subagent profiles
```

## Syncing with upstream

Bodies diverge only where harness mechanics differ. To re-sync: diff `skills/` against the same paths in `mattpocock/skills`, port prose changes, keep the namespacing/`run_subagent` edits.

## Credit & license

All skill content © Matt Pocock, [MIT](./LICENSE). This repo is an unofficial adaptation — if upstream ships a native Devin plugin ([mattpocock/skills#772](https://github.com/mattpocock/skills/issues/772)), prefer it.
