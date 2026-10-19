# GitHub Handoff — a Claude Code skill for designers

Hand off a coded project to a developer the right way, without knowing Git.

`github-handoff` is a [Claude Code](https://docs.claude.com/en/docs/claude-code/overview) skill that takes a designer by the hand through eight steps, one at a time. Claude does the technical work, explains each step in plain language, and asks for your "yes" before deleting, committing, or pushing anything.

## What it does

| Step | What happens |
|---|---|
| 0 | Asks for the project name, whether the developer already has a repo, and your Figma link |
| 1 | Sets up Git and GitHub on your computer (once) |
| 2 | Cleans up unused files and debug code — nothing visual changes |
| 3 | Moves API keys and secrets out of the code so they never reach GitHub |
| 4 | Collects colors, type, spacing, and radii into design tokens |
| 5 | Writes a `HANDOFF.md`: how to run it, what's prototype vs. production-ready, states, known gaps |
| 6 | Tests a fresh install using only the handoff docs |
| 7 | Pushes to a new private repo and invites the developer — or opens a pull request on their existing repo |
| 8 | Drafts the message to send the developer and suggests a 15-minute walkthrough |

Say **"skip"** at any step and it gets logged as a known gap in `HANDOFF.md`.

## Install

**Personal (all your projects):**

```bash
git clone https://github.com/doniaelwazery/github-handoff-skill-.git
mkdir -p ~/.claude/skills
cp -r github-handoff-skill-/skills/github-handoff ~/.claude/skills/
```

**One project only:** copy `skills/github-handoff` into that project's `.claude/skills/` folder.

**Claude.ai / Claude app:** zip the `skills/github-handoff` folder and upload it under Settings → Capabilities → Skills.

## Use

Open Claude Code in your project folder and type:

```
/github-handoff
```

Or just say "help me hand this project off to a developer."

## Who it's for

Designers who build with Claude Code and need to pass their work to a developer for production. Developers can use it too as a pre-handoff checklist.

## Contributing

Issues and pull requests are welcome — especially translations (Arabic and others) and improvements to the HANDOFF.md template.

## License

MIT — see [LICENSE](LICENSE).
