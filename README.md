# Datagram Messenger · organization home

This repository holds the public organization profile and shared contribution defaults for [Datagram Messenger](https://github.com/datagram-messenger). It is presentation and contributor infrastructure, not a messenger implementation.

## What lives here

| Path | Purpose |
| --- | --- |
| [profile/README.md](profile/README.md) | The organization overview shown on GitHub. |
| [profile/assets/datagram-hero.svg](profile/assets/datagram-hero.svg) | Original, self-contained packet-network hero artwork. |
| [CONTRIBUTING.md](CONTRIBUTING.md) | Repository routing, contribution workflow and safe reporting boundaries. |
| [ISSUE_TEMPLATE/](ISSUE_TEMPLATE/) | Lightweight bug and feature forms, plus chooser configuration. |
| [pull_request_template.md](pull_request_template.md) | Shared review context without an oversized checklist. |

## How the defaults work

GitHub reads organization profiles from `profile/README.md` in a public `.github` repository. Shared community files are fallbacks: a repository's own corresponding file takes precedence. They are not copied into other repositories and do not replace project-specific policies.

Issue forms and `config.yml` live together in this repository's root `ISSUE_TEMPLATE/` directory. A consuming repository with valid templates **or configuration** in its own `.github/ISSUE_TEMPLATE/` uses none of the default issue-template set. Keep that all-or-nothing behavior in mind when customizing a project.

See GitHub's [default community health files documentation](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file) and [issue forms syntax](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-githubs-issue-forms).

There is deliberately no shared security policy, code of conduct, funding file or invented contact channel here. Existing repository policies remain authoritative. Read [safe reporting guidance](CONTRIBUTING.md#security-and-sensitive-data) before sharing anything sensitive.

## Updating the profile

1. Verify claims against the relevant public repository and its documentation. Keep transport encryption separate from any future user-to-user E2EE design; describe privacy as a goal, not a certification.
2. Edit `profile/README.md`. Use canonical repository names: the application server is `datagram-messenger/server`, not `datagram-server`. Avoid pinned version, star-count, blanket-license or unverified CI badges.
3. Edit the SVG source locally. Keep its `viewBox`, accessible `title`/`desc`, high contrast and generous text sizes. The single navy canvas works in light and dark GitHub themes. No scripts, external images, web fonts or embedded stylesheets are needed.
4. Keep the profile image URL absolute: `https://raw.githubusercontent.com/datagram-messenger/.github/main/profile/assets/datagram-hero.svg`. Organization-profile rendering is not an ordinary repository README context. Use absolute organization/repository links there; use relative links inside this repository's own documentation.
5. Check local paths, SVG XML, issue-form YAML and `git diff --check`. Preview the Markdown on desktop and a narrow screen. After a maintainer publishes to `main`, verify the raw image URL, GitHub's SVG rendering and the organization page itself.

## Editorial direction

Lead with the engineering ecosystem: application toolkit, Go transport runtime, Rust client and inspection tooling. Keep the front door useful to readers with different goals. Show working concepts without implying a finished consumer product, independent audit, production readiness or exhaustive interoperability.

The artwork is authored here: a quiet navy field, cyan routes, lime packet markers and a DGP1 frame. Important text also exists in Markdown, so the profile remains useful if the image does not load. Stars are a welcome way to follow a relevant repository, not an outcome this design can guarantee.
