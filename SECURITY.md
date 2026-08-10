# Security policy

This repository is intentionally public and contains infrastructure only.

## Never commit

- API keys, PATs, runner registration tokens or APNs credentials;
- Binance account/order/position data;
- WLD trade signals, entries, stops, targets or journals;
- private WLD Sentinel source code;
- calibration reports containing private strategy details.

## Workflow trigger policy

The calibration workflow supports only `workflow_dispatch` and a trusted scheduled run. It intentionally has no `pull_request`, `pull_request_target` or fork-triggered secret-bearing workflow.

## Private repository token

`PRIVATE_REPO_TOKEN` must be a fine-grained token restricted to `EmmanuelDelva/claude-work` only. Grant only the repository permissions required to read the private calibration source and push a verified private audit branch.

Do not reuse a broad classic PAT. Rotate the token if exposure is suspected.

## Output policy

Public logs may state only execution state, private result branch identifier and safety PASS/FAIL. Strategy metrics and trade-level data remain private.

Real-money execution is outside the scope of this public relay. The relay must never receive Binance trading credentials.
