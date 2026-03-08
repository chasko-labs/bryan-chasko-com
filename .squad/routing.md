# Routing Table — bryanchasko.com

## Pattern → Agent

| Pattern | Route To | Notes |
| ------- | -------- | ----- |
| Hugo content model, front matter, page structure | Stratia | Architecture decisions |
| `layouts/` template changes | Stratia + @copilot | Stratia reviews, @copilot implements |
| `themes/bryan-chasko-theme/assets/css/` | @copilot | CSS variables only; no hardcoded colors |
| `themes/bryan-chasko-theme/assets/css/core/` or `extended/` | Stratia + @copilot | Cross-page impact — Stratia reviews |
| New WebGL scene or major scene changes | Stratia | All scenes extend BaseScene.js |
| Minor WebGL scene fixes | @copilot | |
| WebGL asset sync to static/ | Solan | Must run before every build |
| `scripts/deploy.pl` or other deploy scripts | Solan | Perl scripts |
| `terraform/` changes | Myrren + Stratia | Plan before apply |
| S3 bucket policy, CORS, CloudFront behaviors | Myrren | Security-sensitive |
| `infrastructure/` JSON config snapshots | Myrren | Keep in sync with live state |
| Route 53, ACM, SSM | Myrren | |
| GitHub Actions (`deploy.yml`, `terraform.yml`, `webgl-tests.yml`) | Solan + Myrren | |
| Playwright tests, baseline updates | Kade Vox + @copilot | Kade Vox sets strategy |
| Local Hugo environment, submodule sync | Orin | |
| `agentic_instructions/` fragment updates | Stratia | Keep non-overlapping |
| Content Markdown (services, notes, topics) | @copilot | Preserve front matter |
| New services/offering pages | @copilot | Follow `content/services/` structure |

## Do Not Route to @copilot Without Review

- `themes/PaperMod/` — submodule, never touch
- IAM, bucket policy, or CloudFront behavior changes
- New WebGL scenes (→ Stratia first)
- Terraform module additions (→ Myrren + Stratia)
- `core/variables.css` or `extended/nebula.css` — cross-page impact

## Agentic Instruction Fragments

For detailed task-specific guidance, use `agentic_instructions/`:

| Task Area | Fragment |
| --------- | -------- |
| Home page CSS | `agent-instructions-css-home.md` |
| General CSS | `agent-instructions-css.md` |
| Project setup | `agent-instructions-setup.md` |
| CI/CD and deploy | `agent-instructions-cicd.md` |
| Kiro pair programming | `agent-kiro-pair-programming-with-copilot-instructions.md` |
