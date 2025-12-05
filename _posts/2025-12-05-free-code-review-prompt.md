---
layout: post
title: "How being cheap led me to build a free code review prompt"
description: "When Cursor's PR reviews ran out, I asked it to write me a prompt to replicate the functionality. The result has been surprisingly useful."
permalink: /free-code-review-prompt/
tags: [ai, code-review, cursor, productivity]
---

I'd like to tell you a story about how my reluctance to spend money has led to a bit of an innovation.

Last week, I'd woken up early and decided to do some morning coding in Cursor on [Ticketlab](https://ticketlab.co.uk). I have my git repo connected to Cursor (to use background agents), and upon opening a new pull request, Cursor helpfully commented on my PR to point out a potential bug that I'd not spotted.

Having found that useful, I started paying attention to their comments, some of which were more helpful than others. As soon as I'd got use to the idea that Cursor was reviewing my code for me, they posted another PR comment saying I'd run out of my free reviews for the month (you get 5 under Cursor's regular plan I think). It invited me to pay them more money to get more review. 

Because I'm astonishingly cheap, and would always rather not pay for such things, I asked Cursor to write me a prompt that I could run to replicate this functionality without paying, and it (despite its best interests) obliged.

I shared it with a colleague at John Lewis, and he ran with it: quickly becoming a champion for running this review prompt as part of his regular development flow, and sharing it around the Partnership for others to benefit from. So I'm here now to share it with you.
## What makes it work

The prompt does a few things well:

1. **It checks your branch is up to date first** - There's no point reviewing code that's already out of sync with main. The prompt enforces this with a hard stop if your branch needs rebasing.

2. **It reads your README for context** - Understanding the project's purpose, tech stack, and testing approach helps it give more relevant feedback.

3. **It focuses on actionable findings** - Rather than just summarising the diff, it categorises issues into bugs, security concerns, quality suggestions, and testing gaps.

4. **It respects your workflow** - It assumes tests are passing and doesn't try to run migrations or modify your working tree. It's a review tool, not a build tool.

## The prompt
Here's the full prompt including enhancements from my colleague to ensure the current branch is compatible with the main branch and up to date. You can copy this into Cursor (or Claude, or Copilot etc.) and run it in your project:

```
---
description: 'This prompt is designed to pre-review a set of changes in your branch before opening a Merge Request'
---

## Purpose

Provide an automated pre–pull request review that inspects the current working branch against the main branch and highlights potential bugs, risky changes, security considerations, and follow-up suggestions before opening a PR. The command aims to surface issues early, mirroring the quality bar enforced by the TDD workflow.

## Workflow

**CRITICAL: Steps 3–7 must ONLY be executed if step 2 confirms the branch is up to date. If step 2 fails, the review MUST terminate immediately with no further analysis.**

1. *Update References*
    - Run `git fetch origin main` to ensure the comparison baseline is up-to-date.

2. *Verify Branch is Up-to-Date* **[MANDATORY CHECKPOINT - DO NOT PROCEED IF THIS FAILS]**
    - Run `git merge-base --is-ancestor origin/main HEAD`
      Check the exit code explicitly - if it's non-zero (command fails), the branch is not up to date
      Only proceed if the exit code is 0
    - **If the branch is not up to date:**
        - Output EXACTLY: "⚠️ Your branch is not up to date with `origin/main`. Please rebase before running the review."
        - **HALT EXECUTION IMMEDIATELY. DO NOT proceed to step 3 or any subsequent steps.**
        - **The review is COMPLETE. Your task is FINISHED. Do not perform diff analysis.**
        - **STOP HERE. OUTPUT NOTHING ELSE.**
    - **Only if the branch does NOT need rebasing, proceed to step 3.**

3. *Load Context*
    - read the README.md to understand the project purpose, tech stack, and testing approach.

4. *Diff Analysis*
    - Determine the target branch with `git rev-parse --abbrev-ref HEAD`. If the branch is already main, note that no comparison is needed.
    - Use `git --no-pager diff origin/main` to get the full diff of changes.
    - Pay special attention to:
        - Tests updated or missing (ensure TDD expectation).

5. *Risk Evaluation*
    - Categorise findings into potential bugs, security concerns, and improvement suggestions.

6. *Documentation Alignment*
    - Flag missing documentation updates as a review finding.

7. *Testing Gaps*
    - Verify whether new or modified behaviour is covered by automated tests.
    - Highlight absent tests or risky areas needing manual verification.

## Review Findings Output Template

## Potential Bug Reports

- [Severity] `path/to/file`: Short headline describing the issue.
    - Details: Explain why it is likely a bug, referencing diff context.
    - Recommendation: Suggested fix or mitigation.

## Security Considerations

- [Severity] `path/to/file`: Security or privacy risk summary.
    - Details: Reference specific lines and affected data flows.
    - Recommendation: Steps to address or verify.

## Quality Suggestions

- [Severity] `path/to/file`: Improvement opportunity (performance, readability, DX).
    - Details: Observation and rationale.
    - Recommendation: Optional refinements or follow-up tasks.

## Testing & Documentation Gaps

- [Severity] Area: Missing or insufficient automated tests updates.
    - Details: What is absent and why it matters.
    - Recommendation: Specific test cases or documentation updates to add.

## Additional Guidance

- Prefer British English in all feedback.
- Reference documentation where relevant.
- Highlight any dependency on background jobs, cron tasks, or external services that might mask live issues.

## Command Usage Notes

- **CRITICAL**: If step 2 fails (branch not up to date), you MUST stop immediately. Do not analyze the diff, do not provide findings, do not continue with any review activities. Simply output the warning message and end your task.
- You can assume the build is passing and the tests are green so you don't need to run the build.
- The command should NOT execute migrations or modify the working tree.
- Provide concise, actionable findings; avoid verbose summaries of obvious diff content.
- If no issues are discovered, explicitly state that no potential bugs, security concerns, or testing gaps were identified.
```

## How to use it

1. Open Cursor (or your AI assistant of choice) in your project directory.
2. Do your work and commit what you need to.
3. Paste the prompt above into a new chat and run it before opening your PR.
4. Review the findings and fix any issues it surfaces.
5. Profit (probably).

## Why it works
The prompt works because it's structured like a specification. It gives the AI clear steps to follow, explicit guardrails (like the branch check), and a consistent output format. It's not trying to be clever—it's trying to be thorough and predictable.

This is the same principle I use in [Specification Driven Development](https://ramone.co/ai-specification-driven-development/): give the AI clear instructions, and it'll give you better results. The prompt itself is a spec for how to review code.
## Customising it
You might want to tweak it for your workflow:

- Change the branch check from `origin/main` to your default branch
- Add project-specific checks (e.g., "verify all API routes have rate limiting")
- Adjust the severity levels to match your team's conventions
- Add checks for specific file types or patterns your project cares about

The beauty of having it as a prompt is that you can iterate on it. If it misses something important, update the prompt and try again.
## The cost of being cheap
In the end, my reluctance to pay for Cursor's PR reviews led me to build something that's actually more useful than the original feature and saves my team time reviewing my shoddy code! The prompt is free, unlimited, and I can customise it to my exact needs. Sometimes being cheap pays off.

If you try it out, let me know how it works for you. And if you improve it, share your version: I'm always looking to make my tools better.

