<!--
  project-context.md template — rendered by bin/kiro-bootstrap into
  <repo>/.kiro/steering/project-context.md
  authored once at bootstrap, hand-edited as the project evolves
-->

# project context — bryan-chasko-com

## what this repo is

bryan-chasko-com is a `hugo` repo in the heraldstack. specific purpose, audience, and runtime surface live in the project-specific facts section below — bootstrap fills in the type-derived defaults; the human author owns everything below the divider

## stack

# TODO: list stack components (e.g. hugo, papermod-derived theme, woodpecker)

## deploy targets

# TODO: fill in deploy targets (e.g. s3://awsaerospace.org via woodpecker)

---

## notable architectural facts

# TODO: document architectural facts (account-routing, deploy-exclusions, cross-repo runtime contracts)

(this section is human-authored. fill in: account-routing rules, cross-account artifact splits, runtime quirks, deploy-exclusion rules, repo-internal subscope conventions, anything an agent needs to know to operate correctly here that is NOT in the repo-type doc)

## the rule in one sentence

repo-type behaviors live in `~/.kiro/steering/repo-types/hugo.md`; only project-specific deviations and notable architectural facts belong here