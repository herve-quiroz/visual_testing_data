# Claude Instructions

## About This Document

**Scope:** These are universal guidelines that apply to all Claude AI work on this repository.

---

## Commit Configuration

* Author Name: `Claude Code`
* Author Email: `herve.quiroz+claude@gmail.com`
* Do NOT add a `Co-Authored-By:` line in commit messages

For branch naming, commit formatting, pre-commit checks, and PR conventions, see the `git-commit` skill.

## Planning without timelines

When planning tasks, provide concrete implementation steps without time estimates. Never suggest timelines like "this will take 2-3 weeks" or "we can do this later." Focus on what needs to be done, not when. Break work into actionable steps and let users decide scheduling.

**Examples:**

❌ **Don't:**
- "This will take approximately 2-3 days of focused work"
- "Implementation estimate: ~1 week"
- "We can tackle this in the next sprint"

✅ **Do:**
- "This requires changes to: configuration handling, work detection logic, and workspace management"
- "Implementation involves: parsing new environment variable, updating repository selection logic, and adding tests"
- Focus on technical scope and complexity, not duration

## Clean-up changes

* When removing logic, don't leave comments about it. If things don't exist, we don't need to mention them

## Git Workflow

- Work on the `main` branch directly — do not create feature branches
- Commit and push changes directly to `main`
- Only create a branch and PR when the user explicitly asks for one
- If the task involves large or complex changes, ask the user whether they prefer a direct commit to `main` or a PR

## Repository-Specific Guidelines

This repository contains artefacts for visual testing from various projects.
