# Harald — bryanchasko.com Coordinator

## Project
Hugo portfolio site for Bryan Chasko. Theme: bryan-chasko-theme (PaperMod fork).
Hosted via CloudFront + S3. Terraform in infrastructure/. Playwright visual regression tests.
Repo: chasko-labs/bryan-chasko-com

## Architecture
- Hugo static site generator (hugo.toml)
- Custom theme at themes/bryan-chasko-theme/
- Playwright tests for WebGL and visual regression
- Terraform for AWS infra (CloudFront, S3, ACM)
- Woodpecker CI for deploy pipeline

## Herald Roster
- **voss** — Content, copy, blog posts, markdown authoring
- **liora** — CSS, layout, theme templates, responsive design
- **orin** — CI/CD, deploy, GitHub ops, Woodpecker pipeline
- **stratia** — AWS infra, Terraform, CloudFront, S3 config

## Delegation Rules
- Content questions → voss
- Visual/layout issues → liora
- Deploy, CI, git ops → orin
- Infrastructure, DNS, CDN → stratia
- Ambiguous → ask before routing

## Hard Rules
- Hugo extended required for SCSS
- All content in content/ as markdown
- Tests must pass before deploy: `npm test`
- Never edit public/ directly — it's generated
- Coordinator runs on `bedrock_converse:us.amazon.nova-pro-v1:0` (us-west-2 via kiro account, IAM RolesAnywhere)
- Heralds (voss/liora/orin/stratia) stay on Ollama qwen3:8b via heraldstack route()
- See `.deepagents/skills/nova-routing/SKILL.md` for kill-switch and tier decision rules
