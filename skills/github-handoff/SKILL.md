---
name: github-handoff
description: Walk a designer step by step through handing off a coded project to a developer via a GitHub repo: setup, cleanup, secrets, tokens, HANDOFF.md, test, push, invite.
---

# GitHub Handoff — guided, one step at a time

You are guiding a designer (not a developer) through handing off a coded project to a developer using GitHub. Assume they do not know Git. Your job is to do the technical work yourself and keep them in control of every decision.

## How to run this skill

- Do ONE step at a time. At the start of each step, say in plain words: the step number (e.g. "Step 3 of 8"), what this step does, and why it matters. Keep it to 2–3 sentences.
- Do the work yourself with your tools. Never ask the user to type terminal commands unless a step truly requires their hands (a browser login, a GitHub web page).
- Before anything that deletes files, rewrites many files, commits, or pushes: show what you're about to do and wait for the user's "yes".
- At the end of each step, give a one-line summary of what changed, then ask: "Ready for Step N+1?" Wait for the answer.
- Avoid jargon. If you must use a term (repo, commit, branch, .gitignore), explain it in one short phrase the first time.
- If something fails, explain the problem simply, fix it if you can, and only then continue.
- The user can say "skip" for any step; note it as a known gap in HANDOFF.md.

## Step 0 — Ask before starting

Ask these together (use AskUserQuestion if available):
1. What's the project name? (used for the repo name)
2. Does the developer already have a GitHub repo for this project? (New repo / Their existing repo)
3. Do you have the Figma link handy? (optional, can add later)

Then confirm you're in the right project folder by listing its top-level files and asking "Is this the project?"

## Step 1 of 8 — Set up GitHub (once per computer)

- Check whether `git` and the GitHub CLI `gh` are installed. Install whatever is missing (Homebrew on macOS, winget on Windows, the package manager on Linux).
- Run `gh auth status`. If not logged in, run `gh auth login` (GitHub.com, HTTPS, login with browser) and tell the user exactly what to click and the one-time code to paste.
- Make sure git has a name and email set (`git config --global user.name` / `user.email`); ask the user for them if missing.
- If they have no GitHub account, tell them to create one at github.com and come back.

## Step 2 of 8 — Clean up the project

- Find unused files, leftover experiments, duplicate assets, and `console.log` / debug statements.
- Show the list grouped by type. Wait for approval. Then remove only what was approved.
- Rule: never change how anything looks or behaves.

## Step 3 of 8 — Protect secrets

- Search the code for API keys, tokens, passwords, and private URLs.
- If found: move them to `.env`, make sure `.env` is in `.gitignore`, and create `.env.example` with placeholder values.
- Also ensure `.gitignore` covers `node_modules`, build output folders, `.DS_Store`, and editor folders.
- If a secret was already committed in earlier git history, warn the user plainly that the key should be rotated (replaced) with the service that issued it.
- If no secrets: say so and move on.

## Step 4 of 8 — Organize design tokens

- Collect colors, font families, font sizes, spacing, radii, and shadows into one source of truth (CSS variables in a tokens file, or the Tailwind config if the project uses Tailwind).
- Show the user the token list with proposed names before replacing hardcoded values. Let them rename.
- Replace hardcoded values with tokens.
- Run the project and ask the user to check visually that nothing changed. If a preview or screenshot tool is available, take before/after screenshots.

## Step 5 of 8 — Write HANDOFF.md

Create `HANDOFF.md` at the project root with these sections:
1. **What this is** — one paragraph, plus the Figma link.
2. **How to run it** — required Node version, install and start commands, env vars (point to `.env.example`).
3. **Project structure** — the main folders and what lives where.
4. **Design tokens** — where they live and how to use them.
5. **Prototype vs. production-ready** — an honest table of what's solid and what's throwaway (hardcoded data, fake API calls, missing validation).
6. **Interaction states** — hover, focus, empty, loading, error, and which are done vs. missing.
7. **Intentional decisions** — anything that might look like a bug but isn't.
8. **Known gaps / TODOs** — accessibility, tests, edge cases, browser support, skipped steps.
9. **Contact** — the designer's name and how to reach them.

Ask the user to review it and fill in anything only they know. Offer to create a `docs/` folder for screenshots or a screen recording and tell them to drop files there.

## Step 6 of 8 — Test a fresh install

- Clone or copy the project into a temporary folder, install dependencies, and start it using ONLY the instructions in HANDOFF.md.
- If anything fails, fix the project or the docs and try again.
- Tell the user: "A developer can now run this on day one without asking you anything."

## Step 7 of 8 — Push to GitHub

**If it's a new repo:**
- `git init` if needed. Make a few logical commits with clear messages (e.g. "Add layout and components", "Add design tokens", "Add handoff docs") — show the plan first.
- Create a **private** repo with `gh repo create <project-name> --private --source=. --push`.
- Share the repo URL.
- Tell the user how to invite the developer: on github.com open the repo → Settings → Collaborators → Add people → enter their username or email. Offer to do it with `gh api` if they give you the developer's GitHub username.

**If the developer has an existing repo:**
- Ask for the repo URL. Clone it, create a branch called `design-handoff`, bring the work in, commit, push, and open a pull request with `gh pr create`, using a summary of HANDOFF.md as the PR description.
- Share the PR link and explain: "A pull request lets the developer review your work before it goes into their main code."

## Step 8 of 8 — Walkthrough

Draft a short message the user can send the developer with: the repo or PR link, a one-line summary, a pointer to HANDOFF.md, and a request for a 15-minute call. Suggest they ask questions through GitHub Issues so everything stays in one place.

## Finish

Give a short recap: repo/PR link, what was cleaned, whether secrets were found, and any skipped steps listed as known gaps. Don't repeat every step.
