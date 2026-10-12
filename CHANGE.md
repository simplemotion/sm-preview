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
| &mdash; | &mdash; | 2026-09-13 | Greg Gowans | **Add the sm-ci caller stub, which this repo has never carried.** It held sm-pr.yml alone. The two are siblings: sm-ci owns push and tags, sm-pr owns pull_request. This repo already carries 2 tag(s), minted by something other than sm-ci - publish or promote - so the stream here was never sm-ci's to stamp and the existing tags are not evidence it ran. Copied verbatim from the canonical `examples/caller-stub.yml`, read live rather than from the copy vendored in the sibling repo, which was stale on 2026-08-01. Found by the fleet census `sm-audit --caller-stubs`, the only thing that can see a missing stub: a repo with no sm-ci.yml never runs sm-ci, so sm-ci can never report its own absence. One of 77 half-gated repos across 46 orgs. |
| (auto) | &mdash; | 2026-10-12 UTC | Greg Gowans | **Name the renamed installer repo, simplemotion/sm-install-int.** Greg renamed simplemotion/sm-install to sm-install-int on 2026-10-12, and the new repo sm-install-ext serves install.simplemotion.com. The old name redirects, but the docs now use the current name. |
| (auto) | &mdash; | 2026-10-11 UTC | Greg Gowans | **Use the new repo names for the external path.** Greg renamed the four public-path repos on 2026-10-11. This repo is now simplemotion/sm-preview-external. README.md, CLAUDE.md and SECURE.md now use the -external repo names, the words external path, and channels/external-packages.txt. |
| (auto) | &mdash; | 2026-10-11 UTC | Greg Gowans | **List the four -internal channel repos.** There are now two discrete release paths (3400-0000-SM-Software/3400-9993-SM-Publish#35). The repo tables in README.md and CLAUDE.md now show the public path and the internal path. |
| (auto) | &mdash; | 2026-10-11 UTC | Greg Gowans | **State that this repo is anonymously public.** Anyone can download from `sm-preview` without a GitHub account, and it has no team grants. README.md, CLAUDE.md and SECURE.md now say so. SECURE.md adds the threat of a package that is not for the public. A promotion here needs two admin approvals (3400-0000-SM-Software/3400-9993-SM-Publish#30). |
| (auto) | &mdash; | 2026-10-11 UTC | Greg Gowans | **State that freelance and customers cohorts can use the preview channel.** The README and CLAUDE.md said that they cannot. Freelance and customers cohorts now have read access to `release` and `preview`. `sm-preview` carries only public-eligible packages (3400-0000-SM-Software/3400-9993-SM-Publish#29). Related: simplemotion/sm-install#99. |
| (auto) | &mdash; | 2026-10-11 UTC | Greg Gowans | **Link to the sm-install README instead of the retired installer URL.** The installers moved from install.simplemotion.com to install.simplemotion.dev, which has an internal copy and an external copy. README.md and CLAUDE.md no longer contain an installer URL or command. They link to the sm-install README and say which copy applies, so the next move does not need a sweep. See simplemotion/sm-install#98. |
| &mdash; | &mdash; | 2026-10-08 UTC | Greg Gowans | **Stop listing x86_64-apple-darwin: Intel Macs are no longer supported.** Greg decided on 2026-10-08 that Intel Macs are no longer supported, fleet-wide, and sm-ci no longer builds or publishes that triple. README.md no longer lists it. |
| &mdash; | &mdash; | 2026-09-29 UTC | Greg Gowans | **Name SimpleMotion.Design Pty Ltd (ACN 611 618 770) as the IP owner in CLAUDE.md.** CLAUDE.md still said all IP is assigned to SimpleMotion.Global Pty Ltd, the company's name before its 24 Sep 2026 change of name, which now belongs to a different company (ACN 702 678 242). ASSIGN.md already named Design; only the ownership line in CLAUDE.md changed. Found by sm-maintain --audit entity-names. |
| — | — | 2026-09-23 11:14 UTC | Greg Gowans | **Name the IP assignee as SimpleMotion.Design Pty Ltd (ACN 611 618 770).** SimpleMotion.Global Pty Ltd (ACN 611 618 770) is being renamed SimpleMotion.Design Pty Ltd (Form 205 lodged 23 September 2026). The assignee is the same company under a new name; every occurrence in ASSIGN.md now carries the new name and the ACN so the assignment stays unambiguous once a new company takes the old name. No other file changed. |
| (auto) | &mdash; | 2026-08-28 09:58 UTC | Greg Gowans | **State the develop base explicitly: `.sm-version` = `0.1.0`.** sm-ci derives the base from a GA tag merged into HEAD, else `Cargo.toml`, else `.sm-version`, else a hardcoded `0.1.0` — and here it was coming from sm-ci's hardcoded fallback. The value written is the one already in effect, so this is not a version change: the resolver returns `v0.1.0-develop-027` before and after, asserted rather than assumed. What changes is that the floor is now readable in the repo instead of implied by CI, which is what lets it be reviewed, and gated. Single line, bare `X.Y.Z`, no `v` prefix: a version file has many naive readers and cannot control them all — a two-line draft of this convention was read as `0.1.0` by sm-ci and concatenated to `0.1.00.0.3` by sm-pr, neither erroring. Only 61 of 1398 repos carried the file before this pass, and only those with an sm-ci stub are being given one, since sm-ci is its only reader. |
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
