# agent instructions — ci/cd

## purpose

guidance for agents working on bryan-chasko-com ci/cd

## pipeline files

- `.woodpecker/ci.yml` — quality gates on pull_request, push to main, manual trigger. runs biome + markdownlint. does not deploy
- `.woodpecker/deploy.yml` — hugo build + s3 sync + cloudfront invalidation. runs on push to main only

github actions are retired across all chasko-labs repos as of 2026-04-13 (see heraldstack memory `project_gh_actions_kill_switch.md`). do not re-add `.github/workflows/` here without a sign-off

## auth chain (zero long-lived iam keys)

```
ci workload cert at /workload.{crt,key}
  → aws_signing_helper at /usr/local/bin/aws_signing_helper
  → rolesanywhere ci-profile → heraldstack-ci-deploy
  → sts:AssumeRole → heraldstack-ci-bryanchasko (site-scoped)
  → s3 rw bryanchasko.com + cf invalidate E2E9BSL5RVN6DI
```

site-scoped role codified in cfn stack `heraldstack-ci-bryanchasko` at `~/code/heraldstack/secure-access/cfn/secrets-store/ci-bryanchasko-role.yaml`

## standardization matrix

| file type             | tool                        | enforcement                            |
| --------------------- | --------------------------- | -------------------------------------- |
| js, ts, mjs, json     | biome 2.4.10                | `.woodpecker/ci.yml` biome step        |
| css                   | biome 2.4.10 (formatter)    | `.woodpecker/ci.yml` biome step        |
| yml, yaml             | biome 2.4.10                | `.woodpecker/ci.yml` biome step        |
| md                    | markdownlint-cli2           | `.woodpecker/ci.yml` markdownlint step |
| toml                  | manual (single `hugo.toml`) | none                                   |
| hugo templates (html) | none — go template syntax   | accept as-is                           |
| perl (`scripts/*.pl`) | none                        | accept as-is                           |

biome config: `biome.json`. markdownlint config: `.markdownlint.json`

## test gate

- playwright webgl tests in `tests/` are local-only — not wired to ci (no gpu in microvm)
- run locally: `npm test`. update baselines: `npm run test:update-baselines`

## emergency operator deploy

normal path is `git push origin main` → woodpecker fires deploy.yml. for an out-of-band deploy from a workstation with operator credentials:

```bash
hugo --minify
aws s3 sync public/ s3://bryanchasko.com --delete --profile <operator-profile>
aws cloudfront create-invalidation --distribution-id E2E9BSL5RVN6DI --paths "/*" --profile <operator-profile>
```

operator profile must have permission against the bryanchasko.com bucket — the legacy `websites-bryanchasko` profile has been retired, configure a fresh sso-backed profile against account 211125425201 instead

## references

- `.woodpecker/ci.yml`, `.woodpecker/deploy.yml` — live pipeline source
- `biome.json`, `.markdownlint.json` — formatter configs
- `~/.claude/CLAUDE.md` secrets section — ssm + rolesanywhere pattern
- heraldstack memory `project_gh_actions_kill_switch.md` — github actions retirement

---

for project setup or css guidance, see the corresponding agent instruction fragment
