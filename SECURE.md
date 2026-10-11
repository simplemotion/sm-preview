<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/simplemotion/.github/main/assets/banners/SM-White.svg">
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/simplemotion/.github/main/assets/banners/SM-Black.svg">
    <img alt="SimpleMotion" src="https://raw.githubusercontent.com/simplemotion/.github/main/assets/banners/SM-Black.svg" width="800">
  </picture>
</p>

<p align="center">
  <em>Engineered for Architecture, Entertainment, Industry and Manufacturing.</em>
</p>

# SECURE — simplemotion/sm-preview

> Security posture, threat model, and secrets-handling notes for `simplemotion/sm-preview`.

## What this repo serves

This is the **public** binary-distribution surface for SimpleMotion's **preview** channel. It hosts GitHub Release assets (binaries + `.sha256` + `.sigstore.jsonl` sidecars) and nothing else.

- No source code.
- No build pipelines (those live in the per-product source repos).
- No installer scripts (those live in `simplemotion/sm-install`).

## Threat model

- **Adversary substitutes the binary at rest.** Mitigated by SHA256 sidecar verification on every download and by sigstore build-provenance verification against the per-product source repo.
- **Adversary smuggles a malicious release via dispatch.** `sm-publish-release.yml` whitelists the source-repo owner (`3400-0000-SM-Software`). A dispatch from any other owner is rejected.
- **Adversary compromises the SM-Binary-Bridge GitHub App.** Would gain `Contents:Write` on this repo. Mitigation: App's private key lives only in `BRIDGE_APP_PRIVATE_KEY` secret here and on dispatching source repos, base64-wrapped per the SimpleMotion convention. Rotate via `sm-get/scripts/admin/set-bridge-app-secrets.sh`.
- **Adversary publishes a malicious preview as a public release.** The preview channel is documented as early-access. Consumers on the release channel pull from `simplemotion/sm-release` and are unaffected. A promotion to this repo needs two approvals from two different admins (3400-0000-SM-Software/3400-9993-SM-Publish#30).
- **Adversary reads a package that is not for the public.** This repo is public, and anyone can download from it without a GitHub account. It has no team grants, so visibility is the only access control. Only public-eligible packages can come here. Internal-only packages stay on `sm-develop` and `sm-testing`, which are private.

## Secrets handling

- No credentials are committed to this repo.
- `BRIDGE_APP_PRIVATE_KEY` (secret) and `BRIDGE_APP_CLIENT_ID` (variable) are the only secrets used by `sm-publish-release.yml`. PEM follows the SimpleMotion `b64:<base64-payload>` envelope convention.
- All SimpleMotion credentials follow the `b64:<base64-payload>` envelope convention.

## Consumer verification

See [`simplemotion/sm-install/SECURE.md`](https://github.com/simplemotion/sm-install/blob/main/SECURE.md) for the full `gh attestation verify --bundle …` recipe. The verification is offline (Sigstore TUF root + Fulcio cert chain travel inside the bundle) and works without GitHub API access.

## Reporting issues

Email **security@simplemotion.com** for any vulnerability discovered in this repo or in a release published here.
