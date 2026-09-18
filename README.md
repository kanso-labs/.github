# .github

Organization-wide community health files for
[kanso-labs](https://github.com/kanso-labs).

## What this is

GitHub serves a fixed set of files from a repository named `.github` to every
other repository in the organization that does not carry its own copy. That is
what this repository is for: each shared document is written once here rather
than copied into five repositories and kept in step by hand.

The supported set is GitHub's, not ours:

| Path                       | Serves                              |
| -------------------------- | ----------------------------------- |
| `CODE_OF_CONDUCT.md`       | every repository                    |
| `CONTRIBUTING.md`          | every repository                    |
| `SECURITY.md`              | every repository                    |
| `SUPPORT.md`               | every repository                    |
| `ISSUE_TEMPLATE/`          | every repository, with `config.yml` |
| `PULL_REQUEST_TEMPLATE.md` | every repository                    |
| `DISCUSSION_TEMPLATE/`     | every repository                    |
| `FUNDING.yml`              | every repository                    |
| `profile/README.md`        | the organization's public page      |

`LICENSE`, `README.md`, `CHANGELOG.md`, `CODEOWNERS` and `AGENTS.md` cannot be
served this way and stay in the repository they belong to.

Two files here are served by nothing and are simply kept in the one place that
belongs to no single repository:

- **`CONVENTIONS.md`** — the canonical text each repository restates in its own
  `AGENTS.md`. A composite action in `github-actions` checks the copies against
  it.
- **`LICENSE`** — this repository's own. GitHub cannot serve a licence as a
  default, and it should not: a licence has to travel with the code, so every
  repository keeps its own copy of the same MIT text.

## Three rules worth knowing before editing

**This repository has to stay public.** A private `.github` serves nothing, and
nothing warns you — the defaults simply never appear.

**An override is all or nothing.** When a repository carries its own copy of one
of these files, none of the contents of the default are used. There is no
merging, so a repository wanting one extra section has to restate the whole
document. That is why the files here hold only what is true of every
repository, and anything repository-specific lives in that repository's
`README.md` or `AGENTS.md` instead.

**A default never appears in a file tree.** It shows in GitHub's interface
only, so someone reading a clone or a published npm tarball will not find it.
That is the cost of this arrangement, and the reason `LICENSE` is not part of
it even where GitHub would allow it.

A repository that does carry its own copy of one of these files is overriding
the default on purpose. Say so in that repository's `AGENTS.md`, so a later
tidy-up does not delete it for consistency.

## This is not the CI repository

[`kanso-labs/github-actions`](https://github.com/kanso-labs/github-actions)
holds the reusable workflows and composite actions that every repository calls.
Nothing here is called by a workflow. Community health files and starter
templates live here; anything with a `uses:` pointing at it lives there.
