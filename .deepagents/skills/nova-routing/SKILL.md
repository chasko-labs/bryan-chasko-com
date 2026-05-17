---
name: nova-routing
description: Use this skill when deciding model selection for an agent invocation — kill-switch first, persona-tier second, complexity third
---

# Skill: Nova Routing

## Decision tree

Apply in order — first match wins:

1. **Kill-switch**: read SSM parameter `/heraldstack/nova-custom/kill-switch` (us-west-2, kiro account 946179428633). If value is `on`, route to `ollama:qwen3:8b` regardless of tier. Cost-protection mode.
2. **Never-train tier**: persona in {liora, orin, ralph-monitor, kade-vox, solan} → `ollama:qwen3:8b`. Per the May 14 primary plan, these never train and never invoke Bedrock.
3. **Train-now tier**: persona in {voss-chasko-author, harald-anchor, tarn-mcp-forge} → `bedrock_converse:us.amazon.nova-pro-v1:0`. Pre-sprint-3, plain Nova Pro. Post-sprint-3, swap to trained LoRA endpoint per the planning doc.
4. **Defer-tier (sprint 5+)**: persona in {stratia-variants, myrren-variants, ellow-variants, kerouac-source-scribe} → `bedrock_converse:us.amazon.nova-pro-v1:0` if `complexity_score >= 0.7` or `token_estimate > 4000`, else `ollama:qwen3:8b`.
5. **Default**: `bedrock_converse:us.amazon.nova-pro-v1:0` — coordinator (Harald) class.

## AWS auth

Bedrock calls authenticate via IAM RolesAnywhere through the kiro account (946179428633, us-west-2). Credentials surface to boto3 via the `bryanchasko-kiro` profile in `~/.aws/config`. No long-lived IAM keys on disk. Cert lifecycle managed by `chasko-labs/secure-access`.

## Origin

Decision tree mirrors the `route()` function defined in `splintercells-deep-agents-cli/docs/nova-custom-planning/2026-05-14-primary-plan-summary.md`. That document is the origin spec — this skill is the live rule. If they diverge, this skill wins for runtime decisions; update both before merging.

## Kill-switch flip

Manual:

```bash
aws ssm put-parameter --name /heraldstack/nova-custom/kill-switch \
  --value on --type String --overwrite \
  --region us-west-2 --profile bryanchasko-kiro
```

Automated trigger: CloudWatch budget alarm at $280 training spend → SNS → Lambda → SSM put-parameter. Defined in `heraldstack-nova-custom` (private repo, not yet bootstrapped per May 14 plan sprint-0).
