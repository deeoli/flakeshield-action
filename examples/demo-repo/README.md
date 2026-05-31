# Demo Repo for FlakeShield

This tiny example repository shows how a real project can generate JUnit test output, run FlakeShield, and inspect the report.

## What it includes

- `tests/test_demo.py` — tiny suite with:
  - one always-passing test
  - one deterministic failure
  - one flaky test controlled by `DEMO_FLAKY`
- `outputs/` — generated JUnit XML and FlakeShield artifacts
- `requirements.txt` — minimal dependency list for `pytest`

## Run locally

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
mkdir -p outputs
pytest --junitxml=outputs/junit_run1_1.xml || true
DEMO_FLAKY=1 pytest --junitxml=outputs/junit_run2_1.xml || true
```

## Generate a FlakeShield report

```bash
flakeshield --reports "outputs/junit_run*.xml" \
           --out outputs/flake_report \
           --db outputs/flakeshield.db \
           --enable-semantic
```

## Expected outputs

- `outputs/flake_report.json`
- `outputs/flake_report.md`
- `outputs/flakeshield.db`
- `outputs/pr_comment.md`
