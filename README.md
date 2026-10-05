# .github

Shared GitHub configuration for [nbaburov](https://github.com/nbaburov)'s showcase repositories.

## Showcase CI

Every showcase repository runs the same pipeline: [`showcase.yml`](.github/workflows/showcase.yml), a reusable workflow with two jobs.

| Job | What it does |
|---|---|
| Secret scan | gitleaks over the full history |
| Verify | runs the repository's own `ci.sh` |

Each repository has the same `.github/workflows/ci.yml`, word for word:

```yaml
jobs:
  showcase:
    uses: nbaburov/.github/.github/workflows/showcase.yml@main
```

The full file is [`caller-ci.yml`](caller-ci.yml). What "verify" means for a repository (tests, a build, booting the stack and a smoke test) lives in that repository's `ci.sh`, which runs its checks in pinned containers. That keeps the workflow identical everywhere and makes `bash ci.sh` the same check locally as in CI.

Callers follow `main`, so a change here reaches every repository on its next run. Check it against one caller before merging.

## License

[PolyForm Noncommercial 1.0.0](LICENSE). This repository is a showcase, so it doesn't take issues or pull requests. Forks are welcome under the license. Commercial use needs a separate paid license; contact [NB Limited](https://nb-limited.com).
