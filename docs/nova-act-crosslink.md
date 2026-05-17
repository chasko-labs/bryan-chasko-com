# splintercells nova-act — awareness note

this site's playwright suite covers the orbit and constellation webgl scenes (`tests/webgl/orbit-scene.spec.js`, `tests/webgl/constellation-interaction.spec.js`), the menu-click cross-browser flow (`tests/menu-click.spec.js`), and webgl performance benchmarks (`tests/webgl/performance.spec.js`). ripple, skills-network, and transition scene specs are not yet authored. local playwright is the primary verification mechanism for visual regression on this repo, run via `npm test` or per-browser `npm run test:chromium|firefox|webkit`.

the splintercells deepagents harness provides a complementary cloud-hosted tier: AWS Nova Act can exercise browser workflows from a remote host without requiring a local chromium instance. this is not a replacement.

## entry point

`invoke_nova_act_workflow` tool on the heraldstack-nova-mcp server at `http://rocm-aibox.local:8170/mcp` (or localhost:8170 from rocm-aibox).

rate limit: 3 concurrent invocations, 30-minute timeout per slot (valkey semaphore).

## when nova-act is appropriate for this repo

- scheduled visual-regression checks that run without a local playwright session
- verifying the bryanchasko.com cloudfront distribution (E2E9BSL5RVN6DI) from a remote host
- multi-instance parallel webgl scene checks
- ci runs that fire from microvms where chromium is not provisioned

## when local playwright testing is correct

- interactive sessions against the local hugo dev server (`hugo server --config hugo.toml`)
- baseline image regeneration (`npm run test:update-baselines`)
- anything requiring the egl/rocm gpu path for webgl surface verification
- debugging a specific scene with `npm run test:debug` or `npm run test:headed`

## implementation reference

`BryanChasko/splintercells-deep-agents-cli` — see `docs/architecture.md` for tool signatures, aws auth, and rate limiter behavior.

## aws account note

nova-act runs in the kiro account (946179428633, us-east-1). this site deploys to a separate aws account via IAM RolesAnywhere → ci-deploy → ci-bryanchasko, with cloudfront distribution E2E9BSL5RVN6DI invalidated on each deploy. these are distinct accounts — nova-act invocations do not touch this site's S3 bucket (s3://bryanchasko.com) or cloudfront distribution unless explicitly wired.
