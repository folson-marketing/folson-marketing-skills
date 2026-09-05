# Folson Marketing Skills

Reusable AI agent skills built for Folson Marketing Agency's work, packaged so they can be imported into either Claude (as a Claude Skill) or a ChatGPT Custom GPT.

## What is in this repo

| Skill | What it does | Claude version | ChatGPT version |
|---|---|---|---|
| `gtm-six-step-research` | Runs a full go-to-market research pass on a new product or idea: total market, segmentation, positioning and competitor sweep, core message, one channel, and a monitor and iterate metric, ending in a styled HTML report plus a supplemental Markdown report | `skills/gtm-six-step-research/SKILL.md` | `gpt-instructions/gtm-six-step-research.md` |

Each skill lives in its own folder under `skills/`, written as a Claude Skill (a Markdown file with YAML frontmatter naming it and describing when to use it). The `gpt-instructions/` folder holds an adapted, platform-neutral version of the same procedure for ChatGPT, with a short note at the top on the couple of places the two platforms differ (mainly: Claude's specific tool names versus whatever browsing or Actions your GPT has).

## Importing into Claude

Claude Skills live in a `skills/` folder and are picked up automatically by name. Depending on how you use Claude:

- **Claude Code or the Claude Agent SDK (including Cowork):** copy the skill's folder into your project's or your account's `.claude/skills/` directory, for example `.claude/skills/gtm-six-step-research/SKILL.md`. The skill becomes available the next time skills are loaded, and Claude will use it whenever the situation matches its `description` field, or when you invoke it by name.
- **claude.ai (Claude Skills in the web or desktop app):** open the Skills settings and upload the `SKILL.md` file for the skill you want, following the in-app upload flow.
- **As a plugin or marketplace entry:** if you maintain a Claude plugin or marketplace, this repo's `skills/` folder can be referenced directly or copied into the plugin's own skill directory.

No code changes are needed. Each `SKILL.md` is self-contained: read it top to bottom before using it, since it is written as an instruction set, not documentation.

## Importing into a ChatGPT Custom GPT

ChatGPT does not have an identical "Skill" concept, but the same operating procedure works well as a Custom GPT built from a short instruction plus an uploaded knowledge document. For each skill:

1. Open the corresponding file in `gpt-instructions/`, for example `gpt-instructions/gtm-six-step-research.md`.
2. Follow the short setup steps at the top of that file: create a Custom GPT, paste the short pointer instruction into the GPT's Instructions field, and upload the file itself as Knowledge.
3. Read the "Mapping notes" section at the top of the file. It explains how the handful of Claude-specific tool references in the procedure (an Apify research tool, a few UI conveniences) map onto whatever tools your GPT has, including a plain instruction to do the research manually and say so when no equivalent tool is connected.

The GPT version is generated from the Claude version by stripping the Claude-only frontmatter and adding that mapping guidance; the actual step-by-step procedure is identical.

## Updating a skill

The Claude version under `skills/<name>/SKILL.md` is the source of truth. When it changes, regenerate the matching file under `gpt-instructions/<name>.md` (strip the YAML frontmatter, keep the mapping preamble, append the rest) so the two stay in sync. Keeping both in the same repo, in the same commit, is the point: anyone importing either version always gets the same procedure.

## License

No license file is included yet. This repo is public, but public visibility alone does not grant anyone reuse rights. Add a `LICENSE` file (for example MIT, if you want to explicitly permit others to copy and adapt these skills) once you have decided on terms.
