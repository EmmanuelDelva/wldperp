# WLD Calibration Public Relay

Public, zero-cost GitHub-hosted compute relay for the **private** WLD Sentinel calibration pipeline.

## Status

**Operational and validated end-to-end.**

Validated hardened run: `31459101281`.

The relay successfully checks out only `wld-sentinel-ios` from the private repository, runs the complete v3.1 research/verification pipeline, and writes verified evidence back to a private audit branch. No user PC needs to remain powered on.

## Purpose

`EmmanuelDelva/wldperp` provides compute only. The WLD Sentinel strategy, signals, journal, account data and calibration evidence remain in the private repository `EmmanuelDelva/claude-work`.

The public runner temporarily checks out the private calibration code on an ephemeral GitHub-hosted runner, performs the v3.1 research pipeline, verifies the result, and writes verified compact evidence back to a new **private** audit branch.

## Security boundary

This public repository must never contain:

- Binance API keys or trading credentials;
- WLD signals, entries, stops or targets;
- journal/account/position data;
- private WLD Sentinel source code;
- private calibration JSON outputs;
- personal access tokens or other credentials.

The workflow uses one repository secret named `PRIVATE_REPO_TOKEN`. It must be a fine-grained token restricted to `EmmanuelDelva/claude-work` only.

## Zero-cost model

The workflow runs on GitHub-hosted `ubuntu-latest` from this **public** repository. No self-hosted PC is required and the user's computer can remain powered off.

## Execution

- Manual: **Actions → WLD Calibration Public Relay → Run workflow**.
- Automatic deep recalibration: day 2 of each month at 12:17 UTC, using completed-month data.
- Controlled relay trigger: update `.github/public-relay-trigger.txt`.

The public workflow has deliberately **no** `pull_request` or `pull_request_target` trigger. Core GitHub actions are pinned to reviewed commit SHAs and the private checkout uses sparse checkout limited to `wld-sentinel-ios`.

## Verification pipeline

The private v3.1 orchestrator performs:

1. calendar/live feature parity tests;
2. feed-depth and closed-candle tests;
3. purged train/validation/holdout split tests;
4. policy/API safety tests;
5. empirical Binance Data Vision calibration;
6. actual historical funding adjustment;
7. transaction-cost stress including 20 bps;
8. deterministic forward-shadow promotion review;
9. independent verification manifest and SHA-256 evidence.

A successful historical verification does not imply a profitable strategy and cannot enable real-money trading. Promotion gates remain authoritative and this relay cannot mutate the private live policy automatically.

## Private destination

Each verified run creates a new branch in `EmmanuelDelva/claude-work`:

`calibration/v31-public-<run-id>-<attempt>`

Failed runs can publish detailed diagnostics only to a private branch:

`diagnostics/v31-public-<run-id>-<attempt>`

Public logs expose no strategy metrics or trading credentials.

See `SETUP.md` for credential/security status and `SECURITY.md` for the public/private boundary.
