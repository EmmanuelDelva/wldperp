# Zero-cost public relay setup

Status: **configured and validated**.

`EmmanuelDelva/wldperp` is the public GitHub-hosted compute relay for the private WLD Sentinel calibration pipeline.

## Credential

The repository secret is named:

`PRIVATE_REPO_TOKEN`

It must remain a fine-grained token restricted to `EmmanuelDelva/claude-work` only, with repository **Contents: Read and write**. Never commit or paste it into issues, chat, workflow YAML, source code or logs.

The public workflow has already validated that it can:

1. pass the secret gate;
2. checkout private branch `agent/wld-sentinel-ios-v1`;
3. run the complete v3.1 research pipeline on a public GitHub-hosted runner;
4. verify the independent manifest;
5. write compact evidence back to a new private audit branch;
6. keep real-money trading disabled.

## Triggers

- Manual: Actions → `WLD Calibration Public Relay` → Run workflow.
- Automatic: day 2 of each month at 12:17 UTC.
- ChatGPT/automation relay: update `.github/public-relay-trigger.txt`.

## Output

Successful runs write evidence only to the private repository using:

`calibration/v31-public-<run-id>-<attempt>`

Failed runs can write detailed diagnostics only to the private repository using:

`diagnostics/v31-public-<run-id>-<attempt>`

Public logs expose no strategy metrics, entries, stops, targets or account data.

## Security invariants

- No Binance trading credentials are required or accepted by this relay.
- No `pull_request` or `pull_request_target` secret-bearing trigger exists.
- Public `GITHUB_TOKEN` remains read-only.
- Core GitHub actions are pinned to reviewed commit SHAs.
- Only `wld-sentinel-ios` is sparse-checked out from the private repository.
- A successful historical review cannot enable live trading or mutate the private calibration policy automatically.
