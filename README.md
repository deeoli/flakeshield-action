# FlakeShield GitHub Action

**Detect flaky tests, reduce CI noise, and know what to fix first.**

FlakeShield turns repeated JUnit runs into a concise CI triage signal. Install it as a GitHub Action — no pip install required.

## Closed beta

During closed beta, the FlakeShield engine runs from a private container image on GHCR. Contact the maintainer to add your org or repository to the beta allowlist before adopting this action.

## Install

```yaml
- name: Run FlakeShield
  uses: deeoli/flakeshield-action@v0.6.0-beta.1
  with:
    reports: "outputs/junit_run*.xml"
    out_prefix: outputs/flake_report
    db_path: outputs/flakeshield.db
    enable_semantic: "true"
    warn_on_high: "true"
    fail_on_critical: "false"
```

## Example workflow

See [`examples/canonical-workflow.yml`](examples/canonical-workflow.yml) for a full pull-request workflow with DB caching, artifact upload, and PR comment posting.

## Outputs

The action writes:

- `flake_report.json` — structured report
- `flake_report.md` — human-readable markdown summary
- `flake_report_pr_comment.md` — compact PR comment body
- `flakeshield.db` — persistence for cross-run flake tracking

## License

MIT — applies to this action wrapper, examples, and documentation only. The FlakeShield runtime engine is proprietary.
