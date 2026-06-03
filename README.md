# garris-canvas-tools — `notion-to-canvas` skill

A Claude Code skill that builds **Canvas LMS content** — either migrated from a
Notion course or generated on request — as styled, accessible, sanitizer-safe HTML
pages, weekly modules, and (optionally) graded assignments / discussions / quizzes.
Re-runs are idempotent. Built and tested on the **MGCCC** Canvas instance; it reuses
cleanly for any Canvas school after a few setting tweaks.

> **This skill never reads student data.** By design it ships **no tools** that touch
> rosters, grades, or submissions, and its policy refuses such requests outright. It
> is safe for instructors to run on their own courses. (A separate admin/grading tool
> exists and is intentionally **not** included here.)

## Requirements
- **Claude Code** (custom skills/plugins are not available in the claude.ai web app or
  Claude Desktop).
- **PowerShell** (Windows PowerShell 5.1 is fine).
- A **Canvas API access token** for your own account, and your course's base URL +
  course id.
- For Notion-sourced builds only: a connected **Notion MCP** connector.

## Install

### Option A — as a plugin (recommended; versioned, one command)
1. Push this folder to a git repo (GitHub, public or a private org repo).
2. In Claude Code, add the marketplace and install:
   ```
   /plugin marketplace add billathekilla737/garris-canvas-tools
   /plugin install notion-to-canvas@garris-canvas-tools
   ```
3. Reload, then the skill is available (namespaced) as `notion-to-canvas`.
   You'll get a trust prompt on install — review the scripts first.

### Option B — simplest (copy the folder)
Copy `plugins/notion-to-canvas/skills/notion-to-canvas/` into your own
`~/.claude/skills/` so you have `~/.claude/skills/notion-to-canvas/SKILL.md`. Restart
Claude Code. Done.

## First-time setup (each instructor)
1. Generate a token: **Canvas → Account → Settings → New Access Token**. Save it as a
   one-line file `canvas.token` in your project folder. **Never commit it.** (If you
   pasted it into an `.rtf`, `scripts/Extract-CanvasToken.ps1` pulls it out.)
2. Make `canvas.config.<courseId>.json`:
   `{ "base_url": "https://YOURSCHOOL.instructure.com", "course_id": 12345 }`
3. Run a cheap read first to confirm auth: `GET /api/v1/courses/:id`.

## What to change for a non-MGCCC school
- **`references/style-guide.md`** — swap the navy/gold palette hexes for your colors
  (keep the structure; it's what survives the Canvas sanitizer).
- **`scripts/Trim-CanvasNav.ps1`** — the nav keep-list and LTI tab ids are MGCCC's;
  override `-Keep` (find your tab ids via `GET /courses/:id/tabs`).
- **`base_url`** in your config.

## Usage
Just ask Claude in natural language — e.g. "get my Notion course into Canvas",
"add a study guide page to Week 3", "build a final exam quiz". The skill walks the
pipeline (convert → verify → push → trim nav) and, before any push, **asks whether to
publish or leave content unpublished** (default: unpublished). See `SKILL.md` for the
full workflow and the hard-won Canvas/PowerShell gotchas.

## Notes / safety
- The example course ids in the script headers are placeholders (`12345` / `67890`).
- Scripts run with your token against your courses; Claude Code will prompt for
  permission to run them (you can allowlist after first use).
- **You** are responsible for FERPA. This skill won't read student data, but don't
  paste student PII into chats or commits, and don't commit `canvas.token`.

## License / origin
Authored by Zack Garris (MGCCC). Share freely with other instructors.
