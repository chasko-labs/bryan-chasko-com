<!--
  project-scope.md template — rendered by bin/kiro-bootstrap into
  <repo>/.kiro/steering/project-scope.md
  scope governs what agents in this repo may touch
-->

# project scope — bryan-chasko-com

## what this file does

scope governs what agents operating in `bryan-chasko-com` may touch. this is a constraint document, not an aspirational one — work outside the in-scope table escalates upstream rather than landing here. scope drift in a session is a routing failure, not a coding decision

## in-scope work

| work type | owner agent |
| --------- | ----------- |
| TODO      | TODO        |

## out-of-scope work

| work type | escalates to |
| --------- | ------------ |
| TODO      | TODO         |

## escalation patterns

| trigger | route |
| ------- | ----- |
| TODO    | TODO  |

(when an agent observes a scope violation: name the violation, identify the receiving repo or collective, dispatch the appropriate cross-repo agent — never inline-fix work that belongs elsewhere)

## the rule in one sentence

agents in `bryan-chasko-com` only touch in-scope work; out-of-scope observations route to the receiving repo via the escalation pattern, never inline patches