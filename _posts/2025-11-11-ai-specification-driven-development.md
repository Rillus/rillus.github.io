---
layout: post
title: "AI Specification Driven Development"
description: "A practical tutorial on building software with AI as a co-pilot by leading with specifications."
permalink: /ai-specification-driven-development/
tags: [ai, software-delivery, tdd, john-lewis, tutorial]
---
Back in October I stood in front of a room of engineers at John Lewis' head office and delivered my presentation on Specification Driven Development. After the talk, lots of people still had questions, so I promised I would share the full playbook. This is that write-up: the hands-on guide to *AI Specification Driven Development* (SDD) that I lean on every day.
## Why move beyond vibe coding?
I adore the thrill of tossing a single line at Claude and watching a prototype appear. You probably do too. But once the project grows beyond a weekend hack, vibe coding fights back:

- **Natural language is powerful** yet quickly tilts into ambiguity when there are multiple contributors (or Future You revisiting the repo six months later).
- **Context drifts fast** because AI assistants forget or get confused, or you start working on the next problem in the current chat, or start a new chat without the providing the story so far.
- **Bugs compound** when there is no shared definition of done.
- **Future iterations stall** without a durable artefact to brief the next change.

SDD fixes that by keeping the spec front and centre, with AI acting as a focused co-pilot rather than an excitable gremlin.

## Step 1: Anchor the work in a PRD
Everything starts with a lightweight Product Requirements Document (PRD). Mine capture the **why** and the **what** in plain Markdown:
- Overview and metadata (owner, status, links)
- Goals, success metrics, and guardrails
- Target audience and user stories
- Functional scope, non-goals, and dependencies
- Design notes and constraints

Kick it off yourself or let the assistant draft a first pass:

> "Create a PRD for a Scrabble scorekeeper web app. Players enter their words, tag double/triple letter or word scores, and the app tracks scores for up to four players."

Revisit the PRD whenever you feel the work wobble. It is the north star and it lives beside the code.
## Step 2: Embrace the five core principles
1. **Own it** - AI augments; it does not absolve. You are accountable for the quality.
2. **Review it** - Treat outputs as a junior engineer's draft. Challenge assumptions.
3. **Validate it** - Write tests, run tests, do the quick manual poke.
4. **Slice it** - Smaller tasks mean clearer prompts and fewer hallucinations.
5. **Collaborate on it** - Pairing, async reviews, and show-and-tell keep the team in sync.

Slip on any of these and you drift straight back to vibe town.
## Step 3: Warm up your model with rules
LLMs behave best when steeped in your team's culture. I store house rules right in the assistant configuration so every session starts on the same footing:
- Coding standards and architectural preferences (TypeScript strict mode, commit pattern, lint rules)
- Tooling expectations ("Use TDD by default", "Prefer absolute paths", naming conventions)
- Domain vocabulary or and clarifications (acronyms, disambiguation of terms, accessibility commitments)

Even better, update these rule files after every significant project. Claude Code, Cursor, whatever you use - they all improve when you train them with your context.
## Step 4: Choose the right workflow

### New project workflow
1. Draft the PRD.
2. Identify features or components at a high level.
3. Break them into phased, shippable tasks.
4. Generate code plus tests for each slice.
5. Review, iterate, ship, celebrate.

### Existing project workflow
1. Gather requirements from tickets, conversations, analytics, or even disgruntled Slack threads.
2. Compose a contextual prompt that joins those requirements with the relevant code paths.
3. Generate a Markdown specification with user stories, requirements, and Gherkin acceptance criteria.
4. Break the work into deployable tasks (auto-tasking) whenever it exceeds a day, touches more than five files, or feels like grater than a 3 on the Fibonacci scale.
5. Generate code and tests task by task, keeping feedback loops tight.

Every stage whispers the same mantra: *Slice it!* Smaller changes are easier to review, test, and ship.

## Step 5: Craft the contextual prompt

Here is the template I reach for when spinning up a spec:

```
I'd like you to create a markdown specification in `/documents` named `{{ticket_number}}.md`.
Use it to plan the functionality described in `{{ticket_description}}`.
Explore the existing codebase (especially `src/` and `components/`) to locate the right touchpoints.
Provide user stories, requirements, acceptance criteria in Gherkin, suggested files to modify, and any new files to create.
If the change would take more than a day, touch over five files, or score above 3 on Fibonacci complexity, break it into labelled subtasks that can be shipped independently.
```

Run this once per change, store the output in version control, and treat it as the living brief.
## Step 6: Move from spec to code with discipline
1. Ask the assistant to tackle the first task only, referencing the spec.
2. Demand tests with every slice; run the suite locally (or in CI) before you nod yes.
3. If the output wobbles, revert, refine the spec, and try again - or coach the model with explicit corrections.
4. Keep humans in the loop: review diffs, annotate decisions, capture follow-up work.

This is where SDD feels like pairing with an eager junior. You direct, it executes, and together you ship faster.
## Worked example: multiple Scrabble words in one turn
Here is the exact prompt I used when extending the Scrabble app:

> "Create a spec in `/docs` called `multiple-words.md` for the feature: when a player adds a word that also creates other words (e.g. DIGS making TRACKS), score all words in that turn. Ensure the solution scales to many incidental words. If the work exceeds a day, touches more than five files, or scores above Fibonacci 3, split it into subtasks."

The assistant produced user stories, requirements, and Gherkin scenarios, plus a sensible implementation outline. From there I:
- Checked the plan against my mental model (and updated it where reality differed).
- Generated code for the first slice.
- Layered on UI tweaks and validation checks, running tests between each slice.
- Updated the spec as decisions shifted so future Riley can follow the breadcrumbs.

## Troubleshooting and continuous improvement
- **Spot hallucinations early** by requesting smaller diffs and running lint or test suites after every change. Faster feedback, fewer surprises.
- **Keep specs evergreen**. Amend them when the plan pivots; never leave a stale document lurking in the repo.
- **Share learnings**. Drop standout prompts, scripts, or pitfalls into your team rule files so everyone levels up together.

## Final thoughts
Specification Driven Development is spec-tacular! 

Turns AI from a magic trick into a repeatable method. Give your assistant the right guardrails, own the outputs, and you unlock predictable, maintainable software at pace. Everything is a spec; context is king; and if you experiment with this approach, tell me how it goes so we can compare notes over ~~coffee~~ a seasonal sugary beverage.
