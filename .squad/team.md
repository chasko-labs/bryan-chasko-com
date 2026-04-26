# Team Roster — bryanchasko.com

> Squad for Bryan Chasko's Hugo portfolio site. Covers content, theme development,
> WebGL/3D, AWS hosting infrastructure, and Playwright testing.

## Coordinator

| Name   | Role               | Notes |
| ------ | ------------------ | ----- |
| Harald | Lead (Coordinator) | Routes work, decomposes tasks, manages priority and scope. Delegates to specialists. |

## Members

| Name      | Role                              | Charter                             | Status     |
| --------- | --------------------------------- | ----------------------------------- | ---------- |
| Stratia   | Site Architecture & Hugo Strategy | `.squad/agents/stratia/charter.md`  | ✅ Active  |
| Orin      | Hugo Dev Environment Expert       | `.squad/agents/orin/charter.md`     | ✅ Active  |
| Solan     | Build & Deploy Pipeline           | `.squad/agents/solan/charter.md`    | ✅ Active  |
| Myrren    | AWS/CDN Infrastructure            | `.squad/agents/myrren/charter.md`   | ✅ Active  |
| Kade Vox  | Playwright Test Lead              | `.squad/agents/kade-vox/charter.md` | ✅ Active  |
| Scribe    | Session Logger                    | `.squad/agents/scribe/charter.md`   | 📋 Silent  |
| Ralph     | Work Monitor                      | `.squad/agents/ralph/charter.md`    | 🔄 Monitor |

## Coding Agent

| Name     | Role         | Status          |
| -------- | ------------ | --------------- |
| @copilot | Coding Agent | 🤖 Coding Agent |

### Good fit for @copilot

- Content edits and new Markdown pages
- CSS overrides in `assets/css/` (using existing variables)
- Layout template fixes in `layouts/`
- Playwright test additions and baseline updates
- `hugo.toml` / front matter changes
- `infrastructure/` JSON config updates

### Needs squad review

- New WebGL scenes or shader changes (→ Stratia review)
- CloudFront behavior changes (→ Myrren review)
- Structural theme changes affecting all pages (→ Stratia)
- Test strategy changes (→ Kade Vox)

## Project Context

- **Owner:** Bryan Chasko
- **Stack:** Hugo, custom `bryan-chasko-theme` (PaperMod fork + 3D/WebGL),
  AWS S3 + CloudFront, Playwright, Terraform
- **URL:** <https://bryanchasko.com>
- **Persona Source:** HeraldStack
- **Created:** 2026-03-08
