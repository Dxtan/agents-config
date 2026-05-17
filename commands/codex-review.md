---
name: codex-review
description: Request a peer review from OpenAI's Codex model, present the feedback, then evaluate and implement only the suggestions that are warranted.
---

# Codex Review
You are performing a peer review workflow using OpenAI's Codex CLI to get an independent code review of uncommitted changes, then critically evaluating and selectively implementing the feedback.

### Step 1: Request the Review

Run the Codex CLI review command against all uncommitted changes:

```bash
codex review "
Run git diff --cached to see the staged changes. If nothing is staged, say so and stop.
Otherwise, review the diff as an expert code reviewer specializing in Laravel, PHP, Vue.js, Inertia.js, and Tailwind CSS.
Provide:
1) Critical Issues - bugs, security vulnerabilities, or breaking changes that MUST be fixed.
2) Improvements - concrete suggestions for better code quality, performance, or maintainability.
3) Nitpicks - minor style or preference items (low priority).
Be specific. Reference exact lines from the diff. Provide code examples for suggested fixes.
Do NOT comment on formatting or whitespace.
Do NOT suggest adding comments or docblocks unless something is genuinely confusing.
Keep your review concise and actionable.
"
```

If the command fails (e.g. not authenticated, not installed), inform the user and stop.

### Step 2: Present the Feedback

Display the full Codex review output to the user in a clear, formatted way. Organize the feedback into categories if possible:

- **Bugs / Correctness** — issues that would cause incorrect behavior
- **Security** — potential vulnerabilities
- **Performance** — inefficiencies or optimization opportunities
- **Style / Readability** — naming, structure, clarity improvements
- **Other** — anything that doesn't fit above

### Step 3: Evaluate and Implement

Critically evaluate each piece of feedback. You are the final arbiter — only implement changes that are:

- Genuinely correct and improve the code
- Consistent with the project's conventions (see CLAUDE.md)
- Not introducing unnecessary complexity or over-engineering

For each suggestion, briefly state whether you're **accepting** or **skipping** it and why. Then implement the accepted changes.

Do NOT blindly apply all suggestions. Use your own judgment. Skip suggestions that are:

- Stylistic preferences that conflict with this project's conventions
- Over-engineered solutions for simple problems
- Incorrect or based on misunderstanding the codebase
- Already handled elsewhere in the code

After implementing changes, run the relevant tests to make sure nothing is broken.
