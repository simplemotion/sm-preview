# simplemotion/preview

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

where `<host-triple>` is `aarch64-apple-darwin`, `x86_64-apple-darwin`, `aarch64-unknown-linux-gnu`, `x86_64-unknown-linux-gnu`, `aarch64-pc-windows-msvc`, or `x86_64-pc-windows-msvc`.

## How to install

Use the SimpleMotion installer at `get.simplemotion.com` and pass `--channel preview`:

```bash
bash -c "$(curl -fsSL https://get.simplemotion.com/sm-welcome.sh)" sm-welcome --channel preview
```

The installer (in [`simplemotion/install`](https://github.com/simplemotion/install)) handles platform detection, SHA verification, sigstore attestation verification, and install. Don't fetch binaries directly from this repo unless you're verifying them out-of-band.

## Verification

See [`simplemotion/install/SECURE.md`](https://github.com/simplemotion/install/blob/main/SECURE.md) for the consumer verification recipe (`gh attestation verify --bundle …`).

## How releases get here

Releases arrive automatically via `repository_dispatch` from per-product source repos under `3400-0000-SM-Software`. The source-repo `release.yml` tag-routes by suffix:

| Tag pattern | Target repo |
|---|---|
| `vX.Y.Z` | `simplemotion/release` |
| `vX.Y.Z-preview-NNN` | `simplemotion/preview` |
| `vX.Y.Z-private-NNN` | `simplemotion/private` |
| `vX.Y.Z-testing-NNN` | `simplemotion/testing` |

The receiver workflow here (`publish-release.yml`) downloads the source-run artifacts and creates a GitHub Release.

## Reporting issues

- **Distribution / install bugs:** open an issue on [`simplemotion/install`](https://github.com/simplemotion/install).
- **Product bugs:** per-product source repo under `3400-0000-SM-Software` (internal).
- **Security:** email **security@simplemotion.com**.
