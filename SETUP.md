# One-time setup for `EmmanuelDelva/wldperp`

The public relay repository is already created. The only remaining manual security step is to add one fine-grained GitHub token as an Actions secret. **Do not paste the token into chat or commit it to Git.**

## 1. Create a fine-grained personal access token

In GitHub, create a fine-grained personal access token restricted to repository:

`EmmanuelDelva/claude-work`

Required repository permission:

- **Contents: Read and write**

Do not grant organization/admin permissions and do not include unrelated repositories.

The write permission is required only because a verified calibration writes compact evidence back to a new private audit branch. The workflow never writes to `main`.

## 2. Add it as an Actions repository secret

Open:

`EmmanuelDelva/wldperp` → **Settings → Secrets and variables → Actions → New repository secret**

Name:

`PRIVATE_REPO_TOKEN`

Value:

Your fine-grained token.

## 3. Run the relay

Open:

**Actions → WLD Calibration Public Relay → Run workflow**

The workflow also runs automatically on day 2 of each month at 12:17 UTC.

## 4. Expected behavior

The public runner:

1. receives no Binance trading credentials;
2. checks out private WLD Sentinel code ephemerally;
3. installs the private backend on the temporary runner;
4. runs v3.1 parity, split, policy and empirical calibration checks;
5. performs actual-funding and cost-stress evaluation;
6. independently verifies the evidence;
7. deletes verbose runner output before publishing;
8. pushes verified compact evidence to a new private branch named `calibration/v31-public-<run-id>-<attempt>`;
9. exposes only PASS/FAIL and that private branch identifier in public logs;
10. never enables live trading.

## 5. What to verify after a successful run

In the private result branch require:

- `calibration_verification_manifest_v31.json` has `passed: true`;
- `real_money_enabled` is `false`;
- `automatic_policy_mutation` is `false`;
- report/review SHA-256 values are present;
- any profile promoted by the historical review is at most `FORWARD_SHADOW_CANDIDATE`.

The private WLD Sentinel policy remains authoritative. Historical calibration cannot authorize a real-money trade.
