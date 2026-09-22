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

Three files here are served by GitHub to nothing and are simply kept in the one
place that belongs to no single repository:

- **`CONVENTIONS.md`** — the canonical text each repository restates in its
  own `AGENTS.md`. Nothing enforces the match; the copies are kept in step by
  hand.
- **`LICENSE.md`** — this repository's own. GitHub cannot serve a licence as a
  default, and it should not: a licence has to travel with the code, so every
  repository keeps its own copy of the same MIT text. Every formatter in the
  organization is told to leave it alone, which is what keeps the copies byte
  for byte equal.
- **`default.json`** — the shared Renovate preset, described below. Unlike the
  other two it is not restated anywhere: it is read, not copied.

## The shared Renovate preset

`default.json` holds the Renovate settings that are true of every repository in
the organization. It is referenced as `local>kanso-labs/.github`, which is what
a bare repository reference resolves to — Renovate looks for `default.json` at
the root when no filename is given.

Everything Renovate manages extends it, after `config:recommended` so that
these values win:

| Extends it | Covers |
| --- | --- |
| `config.js` in [`kanso-labs/renovate`](https://github.com/kanso-labs/renovate) | Repositories that ship no config of their own |
| Each repository's own `.github/renovate.json` | That repository |

Both halves are needed, and this is the whole reason the file exists. A
repository's own config is merged *over* the runner's global config, and every
one of them re-extends `config:recommended` — so a setting written only in
`config.js` is reinstated by the preset everywhere except the repositories
carrying no config at all. Writing it here instead means one file to change
rather than six.

**The preset extends nothing itself, deliberately.** Pulling `config:recommended`
into it would reinstate that preset's defaults for a consumer that had chosen
otherwise, which is the failure it exists to prevent.

**A change here is live on the next Renovate run.** There is no tag and no pin,
so treat it like the community health files above rather than like
`kanso-labs/actions`.

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

[`kanso-labs/actions`](https://github.com/kanso-labs/actions)
holds the reusable workflows and composite actions that every repository calls.
Nothing here is called by a workflow. Community health files and starter
templates live here; anything with a `uses:` pointing at it lives there.

`default.json` does not blur that line. It is configuration Renovate reads, not
something a workflow calls — no `uses:` points at it, and the workflow that
runs Renovate lives in
[`kanso-labs/renovate`](https://github.com/kanso-labs/renovate) either way.
