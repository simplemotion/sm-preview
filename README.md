# simplemotion/sm-preview

**Preview channel** binary-distribution surface for SimpleMotion products.

- **Audience:** Early-access consumers — features in flight.
- **Stability:** Pre-stable. Releases here MAY regress. Use `--channel release` for stable builds.

## What's here

GitHub Release assets — one release per product version, three files per platform:

```
<package>-<host-triple>                  ← binary
<package>-<host-triple>.sha256           ← SHA256 sidecar
<package>-<host-triple>.sigstore.jsonl   ← sigstore build-provenance bundle
```

where `<host-triple>` is `aarch64-apple-darwin` (Apple silicon; Intel Macs are not supported since 2026-10-08), `aarch64-unknown-linux-gnu`, `x86_64-unknown-linux-gnu`, `aarch64-pc-windows-msvc`, or `x86_64-pc-windows-msvc`.

## How to install

Use the SimpleMotion installer and select this channel with `--channel preview`. Executive and employees cohorts use the internal installer copy. Freelance and customers cohorts use the external installer copy. This repo is public. Anyone can download from it without a GitHub account. This channel carries only packages that can go to the public `release` channel.

The [`simplemotion/sm-install` README](https://github.com/simplemotion/sm-install#readme) gives the install commands for each copy. This repo does not copy those commands, because the installer URL can change.

The installer (in [`simplemotion/sm-install`](https://github.com/simplemotion/sm-install)) handles platform detection, SHA verification, sigstore attestation verification, and install. Don't fetch binaries directly from this repo unless you're verifying them out-of-band.

## Verification

See [`simplemotion/sm-install/SECURE.md`](https://github.com/simplemotion/sm-install/blob/main/SECURE.md) for the consumer verification recipe (`gh attestation verify --bundle …`).

## How releases get here

Releases arrive automatically via `repository_dispatch` from per-product source repos under `3400-0000-SM-Software`. The source-repo `release.yml` tag-routes by suffix:

| Tag pattern | Target repo |
|---|---|
| `vX.Y.Z` | `simplemotion/sm-release` |
| `vX.Y.Z-preview-NNN` | `simplemotion/sm-preview` |
| `vX.Y.Z-develop-NNN` | `simplemotion/sm-develop` |
| `vX.Y.Z-testing-NNN` | `simplemotion/sm-testing` |

The receiver workflow here (`sm-publish-release.yml`) downloads the source-run artifacts and creates a GitHub Release.

## Reporting issues

- **Distribution / install bugs:** open an issue on [`simplemotion/sm-install`](https://github.com/simplemotion/sm-install).
- **Product bugs:** per-product source repo under `3400-0000-SM-Software` (internal).
- **Security:** email **security@simplemotion.com**.
