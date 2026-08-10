# WLD Calibration Public Relay

Public, zero-cost GitHub Actions compute relay for the **private** WLD Sentinel calibration pipeline.

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

The public workflow has deliberately **no** `pull_request` or `pull_request_target` trigger.

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

A successful historical result may at most become `FORWARD_SHADOW_CANDIDATE`. This relay cannot enable real-money trading and cannot mutate the private live policy automatically.

## Private destination

Each verified run creates a new branch in `EmmanuelDelva/claude-work`:

`calibration/v31-public-<run-id>-<attempt>`

Only compact verified evidence is committed. Verbose runner logs are not pushed back.

See `SETUP.md` for the one-time private credential setup and `SECURITY.md` for the public/private boundary.
