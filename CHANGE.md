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

# CHANGE.md

Changelog for this repo (`simplemotion/sm-preview`).

Versioning follows the SimpleMotion enterprise policy — `vX.Y.Z` releases, `vX.Y.Z-preview-NNN` candidates, `vX.Y.Z-cm-NNN` dev builds. Only releases and RCs are recorded here. **Full policy is in the appendix at the end of this file.**

This repo hosts release-asset binaries for the **preview** channel. Releases land here via repository_dispatch from per-product source repos.

---

## Changelog

| Version | Hash | Date | Author | Notes |
|---------|------|------|--------|-------|
| (auto) | &mdash; | 2026-08-27 02:05 UTC | Greg Gowans | **Add the sm-pr caller stub, so this repo's PRs are actually checked.** The repo carried the enterprise policy files but no PR gate, so nothing validated its changelog, IP assignment or repo shape on a pull request. The stub is the canonical file copied verbatim from 3400-9992-SM-PR examples/. It adds reporting only: no ruleset requires these contexts yet, so a failing check blocks nothing today, and the gate is landed in the fixed order of stub, then the has_pr_gate property, then the ruleset - reversed, a repo can never merge. |
| (auto) | &mdash; | 2026-08-17 | Greg Gowans | **Remove `sm-publish-release.yml` — dead since `sm-ci` moved its dispatch target.** This workflow received the `publish-binary` dispatch and created the release here. `sm-ci` now dispatches to `3400-0000-SM-Software/3400-9993-SM-Publish`, which writes the release into this repo cross-repo with a scoped SM-Binary-Bridge token, so nothing reaches this file any more. **Verified dead before deleting, not assumed:** an `sm-ci` run was re-run after the target changed, its dispatch job succeeded, and the resulting `repository_dispatch` run on the publisher completed successfully — the release was written here by the new path while this workflow sat idle. That was the last of four byte-identical copies of this logic, and on the two PUBLIC channels those copies could never have been deduplicated into a shared caller anyway, since a public repo cannot call an internal reusable workflow. With this gone the repo holds no workflows at all: it is an artifact store, which is the whole point of the arrangement. |
| (auto) | &mdash; | 2026-08-17 | Greg Gowans | Retired `sm-ci.yml` (cargo-cult stub on a repo with no Rust; as a public repo it could never call the internal reusable workflow, so every push since 2026-08-04 was a zero-job startup failure) and `sm-promote.yml` (promotion now runs cross-repo from `3400-9993-SM-Publish`). `sm-publish-release.yml` stays &mdash; it still receives the `publish-binary` dispatch. |

No releases have been cut yet; the first release tag will be `v0.1.0`.

---

## Versioning

This repo follows the SimpleMotion enterprise versioning policy. It is kept in
one canonical place rather than copied into every repo, so an amendment lands
once instead of being reconciled across the fleet:

<https://github.com/simplemotion/.github/blob/main/ANNEXE.md>
