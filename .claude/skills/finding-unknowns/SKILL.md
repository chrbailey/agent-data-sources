---
name: finding-unknowns
description: >-
  Close the gap between what the user asked for and what actually needs to
  happen by surfacing the four categories of unknowns (known knowns, known
  unknowns, unknown knowns, unknown unknowns) before, during, and after a
  task. Use when starting any nontrivial feature, spec, or prompt; when the
  user asks for an interview, brainstorm, prototype comparison, or blindspot
  pass; when beginning a long implementation (keep implementation notes); or
  when wrapping one up (write a pitch/explainer and quiz the user before
  merge).
---

# Finding Your Unknowns

The map is not the territory. A prompt — however detailed — is a map of what
the user wants, and output quality is bottlenecked not by model capability
but by the gaps between that map and reality. This skill turns the four
categories of knowledge (popularized by Anthropic's *A Field Guide to Claude
Fable*) into concrete working techniques. Your job is to find the gaps
**before they get expensive**.

## The four categories

| # | Category | Definition | Failure mode if ignored |
|---|----------|------------|------------------------|
| 1 | **Known knowns** | Everything explicitly captured in the prompt, spec, or referenced files | Ambiguous or contradictory spec; Claude fills gaps with guesses |
| 2 | **Known unknowns** | Gaps the user knows exist but hasn't resolved ("not sure which auth flow we need") | Claude picks silently; the user discovers the wrong choice after hours of work |
| 3 | **Unknown knowns** | Things so obvious to the user they never wrote them down; "I'll know it when I see it" taste and house conventions | Technically-correct output that gets rejected on sight |
| 4 | **Unknown unknowns** | Constraints, edge cases, and interactions nobody has considered yet | Late-breaking surprises: hidden coupling, missed requirements, production incidents |

Every technique below exists to move items *up* this table — into the known-knowns
row — as cheaply as possible.

## Choosing where to spend effort

Scale the process to the task. A one-line fix needs none of this. A
multi-hour, multi-file feature deserves the full loop. Quick triage before
starting:

- Spec is long but you can see ambiguities → **interview** (category 2)
- Task involves taste, UX, style, or "make it good" → **brainstorm/prototype** (category 3)
- You or the user are new to this codebase or domain → **blindspot pass** (category 4)
- Work will run long or touch many files → **implementation notes** (category 4, during)
- Work is done and about to merge or ship → **pitch/explainer + quiz** (category 4, after)

## 1. Known knowns — make the map explicit

Before executing, restate the task in your own words: goal, scope, non-goals,
and the concrete deliverable. If the restatement and the prompt disagree
anywhere, say so — a contradiction in the spec is cheaper to fix now than in
review. Gather the real references (files, APIs, prior art) rather than
assuming them: read the code paths the task touches before proposing how to
change them.

## 2. Known unknowns — interview, don't guess

When the user has open questions (or you detect decisions the prompt doesn't
settle), run a short interview **before** writing code:

- Ask **one question at a time** — batched question lists get skimmed and
  half-answered.
- Ask only the **5–10 highest-leverage questions**: prioritize anything whose
  answer would change architecture, data model, scope, audience, or the
  definition of done. Skip questions you can answer yourself by reading the
  code.
- For each question, offer a recommended default so a busy user can just say
  "yes."
- Stop when the remaining unknowns no longer change what you'd build.

Prompt pattern the user may invoke directly:

> "Interview me about this spec, one question at a time. Prioritize questions
> whose answers would change the architecture or scope."

## 3. Unknown knowns — show options, extract taste

For anything the user will judge by sight (UI, copy, API ergonomics, report
formats), do not converge on one answer and polish it. Instead:

- **Brainstorm** 3–5 meaningfully different directions and present them
  side by side, each with a one-line tradeoff summary.
- **Prototype cheaply** — a sketch, a stub, a single rendered screen — and
  ask "which of these is closest?" Seeing a wrong option makes hidden
  criteria speakable; finding them during implementation is expensive.
- **Mine for references**: ask for an example the user already likes ("show
  me a page/PR/doc in this project that feels right") and diff your plan
  against it. Existing code is a record of unknown knowns — match its
  conventions, naming, and idiom instead of importing your own.

## 4. Unknown unknowns — hunt them at every phase

### Before: blindspot pass

When entering unfamiliar territory, sweep for what nobody thought to ask:

> "I'm working on [task] but I know little about [area]. Do a blindspot pass:
> what are the unknown unknowns here — constraints, existing behavior, edge
> cases, and interactions — that would change how I should prompt or plan?"

Executing a blindspot pass: explore the relevant modules, config, tests, and
docs; then report (a) surprising constraints found, (b) adjacent systems the
change could break, (c) questions the spec should have answered, and (d) the
riskiest assumption currently being made. Teach, don't just list — the goal
is to make the user a better prompter for this domain.

### During: implementation notes

For any long-running implementation, keep a temporary `implementation-notes.md`
(in the scratchpad or work branch, not committed to main) and log as you go:

- every **deviation from the plan** and why
- every **edge case** hit that the spec didn't cover, and the decision made —
  when the spec is silent, choose the **conservative option** and flag it
- anything **surprising** in the existing code that future phases must respect

These notes are how unknown unknowns discovered mid-flight get surfaced
instead of silently absorbed. Review them with the user at natural
checkpoints, and feed them into the pitch below.

### After: pitch, explainer, quiz

Before work merges or ships, close the loop:

- **Pitch / explainer** — a short summary document for stakeholders bundling
  what was built, the key decisions (pulled from the implementation notes),
  what deviates from the original spec, and what was deliberately left out.
  The reader should be able to catch a wrong assumption without reading the
  diff.
- **Quiz** — generate a report of the changes (an HTML page or markdown doc)
  ending with a handful of concrete questions the user must be able to
  answer before merging: "What happens now when X?", "Which module handles
  Y?", "What did we decide about Z and why?" If the user can't answer, that's
  an unknown unknown caught at the last cheap moment — walk through it
  together before merge.

## Guardrails

- Don't interrogate. For small tasks, skip straight to execution; a needless
  interview is worse than a wrong guess on a five-minute change.
- One question at a time, always with a recommended default.
- Never let a technique replace judgment: if you already know the answer from
  the code, don't ask the user.
- Implementation notes are temporary working files — don't commit them as
  permanent documentation; distill them into the pitch instead.

## Source

Distilled from "A Field Guide to Claude Fable: Finding Your Unknowns" by
Thariq Shihipar (Anthropic, 2026) and the companion AIE talk "Field Guide to
Fable" (https://www.youtube.com/watch?v=9fubhllmsBU).
