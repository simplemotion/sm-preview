# SECURE — simplemotion/preview

> Security posture, threat model, and secrets-handling notes for `simplemotion/preview`.

## What this repo serves

This is the **public** binary-distribution surface for SimpleMotion's **preview** channel. It hosts GitHub Release assets (binaries + `.sha256` + `.sigstore.jsonl` sidecars) and nothing else.

- No source code.
- No build pipelines (those live in the per-product source repos).
- No installer scripts (those live in `simplemotion/install`).

## Threat model

- **Adversary substitutes the binary at rest.** Mitigated by SHA256 sidecar verification on every download and by sigstore build-provenance verification against the per-product source repo.
- **Adversary smuggles a malicious release via dispatch.** `publish-release.yml` whitelists the source-repo owner (`3400-0000-SM-Software`). A dispatch from any other owner is rejected.
- **Adversary compromises the SM-Binary-Bridge GitHub App.** Would gain `Contents:Write` on this repo. Mitigation: App's private key lives only in `BRIDGE_APP_PRIVATE_KEY` secret here and on dispatching source repos, base64-wrapped per the SimpleMotion convention. Rotate via `sm-get/scripts/admin/set-bridge-app-secrets.sh`.
- **Adversary publishes a malicious preview as a public release.** Preview channel is documented as early-access. Consumers on the release channel pull from `simplemotion/release` and are unaffected.

## Secrets handling

- No credentials are committed to this repo.
- `BRIDGE_APP_PRIVATE_KEY` (secret) and `BRIDGE_APP_CLIENT_ID` (variable) are the only secrets used by `publish-release.yml`. PEM follows the SimpleMotion `b64:<base64-payload>` envelope convention.
- All SimpleMotion credentials follow the `b64:<base64-payload>` envelope convention.

## Consumer verification

See [`simplemotion/install/SECURE.md`](https://github.com/simplemotion/install/blob/main/SECURE.md) for the full `gh attestation verify --bundle …` recipe. The verification is offline (Sigstore TUF root + Fulcio cert chain travel inside the bundle) and works without GitHub API access.

## Reporting issues

Email **security@simplemotion.com** for any vulnerability discovered in this repo or in a release published here.
