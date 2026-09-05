# Folson Marketing Skills

Reusable AI agent skills built for Folson Marketing Agency's work. Every skill is a folder under `skills/` containing a `SKILL.md` file: YAML frontmatter naming the skill and describing when to use it, followed by the full instruction set. That one file is the source of truth and works unchanged in Claude, ChatGPT, Codex, and any other agent that reads the open Agent Skills format.

## Skills

| Skill | What it does |
|---|---|
| [`gtm-six-step-research`](skills/gtm-six-step-research/SKILL.md) | Runs a full go-to-market research pass on a new product or idea: total market, segmentation, positioning and competitor sweep, core message, one channel, and a monitor and iterate metric, ending in a styled HTML report plus a supplemental Markdown report. |

Each `SKILL.md` is written as an instruction set, not documentation. Read it top to bottom before using it. Every skill ends with a "Running outside Claude" section that maps the handful of Claude-specific tool names onto whatever tools your platform has.

## Quick install

**Claude Code** (terminal or desktop app). Run these two commands inside a Claude Code session:

```
/plugin marketplace add folson-marketing/folson-marketing-skills
/plugin install folson-marketing-skills@folson-marketing-skills
```

Skills then appear namespaced, for example `/folson-marketing-skills:gtm-six-step-research`, and Claude also picks them up automatically when a task matches a skill's description. Run `/plugin marketplace update` later to pull new versions.

**Claude Code, Codex, Cursor, and 70+ other agents** with the open-source `skills` installer:

```bash
npx skills add folson-marketing/folson-marketing-skills --agent claude-code -g
```

Swap `--agent claude-code` for `--agent codex` or another supported agent. Drop `-g` to install into the current project only.

**Any Claude Code session, no tooling.** Paste this prompt:

> Clone https://github.com/folson-marketing/folson-marketing-skills and copy every folder under `skills/` into `~/.claude/skills/`.

## Importing into claude.ai (web or desktop app)

claude.ai has no URL import. Upload a ZIP of the skill folder:

1. Download or clone this repo and zip the skill folder you want, for example `skills/gtm-six-step-research/` (the ZIP must contain the folder, with `SKILL.md` directly inside it).
2. In claude.ai, open Customize, then Skills, click the "+" button, choose "Create skill", then "Upload a skill", and upload the ZIP.
3. Toggle the skill on. It is then available in every conversation on that account.

## Importing into ChatGPT

**ChatGPT Skills** (Business, Enterprise, Healthcare, and Edu workspaces). ChatGPT accepts the same `SKILL.md` format directly:

1. Download the skill's `SKILL.md` from this repo.
2. In ChatGPT, open Plugins in the sidebar, switch to the Skills tab, click "+", and choose "Upload from your computer".
3. Upload the file. Share it with your workspace if you want teammates to have it.

**Custom GPT** (fallback for Free, Plus, and Pro plans, which do not have ChatGPT Skills):

1. Create a new GPT (Explore GPTs, then Create).
2. In the Configure tab, paste this into the Instructions field. The full procedure goes in Knowledge, not here, because the Instructions field is length limited:

   > You are a senior GTM strategist. Follow the attached document "SKILL.md" as your complete operating procedure whenever the user asks for go-to-market research, a GTM strategy, or help positioning a new product or idea. Read the whole document before starting, including its "Running outside Claude" section. Do the six steps in order, in the format it specifies, and produce both an HTML report and a Markdown report exactly as it describes.

3. Under Knowledge, upload the skill's `SKILL.md`.
4. Optionally, if you use GPT Actions, wire an Action to Apify's API (or another data provider) and tell the GPT in Instructions that the "Apify MCP" calls in the document map to that Action. Without one, the GPT should use its own browsing tool and say plainly when it could not verify something.

## Importing into OpenAI Codex

Codex reads `SKILL.md` from `.agents/skills/`. Either use the `npx skills add` command above with `--agent codex`, or ask Codex's built-in `$skill-installer` to install from this repo.

## Updating a skill

Edit `skills/<name>/SKILL.md` and nothing else. There is deliberately only one copy of each skill, so there is nothing to keep in sync. Bump `version` in `.claude-plugin/plugin.json` when you want Claude Code plugin users to receive the update, and run `claude plugin validate .` before pushing.

## License

No license file is included yet. This repo is public, but public visibility alone does not grant anyone reuse rights. Add a `LICENSE` file (for example MIT, if you want to explicitly permit others to copy and adapt these skills) once you have decided on terms.
