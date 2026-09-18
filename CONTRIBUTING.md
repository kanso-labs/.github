# Contributing

Thank you for contributing. This guide covers every repository in the
[kanso-labs](https://github.com/kanso-labs) organization, so it describes what
is true of all of them. Anything specific to one repository — how to build it,
how to test it, what its conventions are — lives in that repository's
`README.md` and `AGENTS.md`.

By participating, you are expected to uphold our
[code of conduct](CODE_OF_CONDUCT.md).

## Reporting Issues and Asking Questions

Before opening an issue, search the repository's issue tracker to make sure it
has not already been reported. See [SUPPORT.md](SUPPORT.md) for where each kind
of question belongs.

To report a security vulnerability, do not open an issue — see
[SECURITY.md](SECURITY.md).

## Development

Every repository documents its own setup. Read, in this order:

1. **`README.md`** — what the project is, and a Development section with the
   commands you need.
2. **`AGENTS.md`** — the conventions, the traps, and the reasoning behind
   both. It is written for coding agents and is equally the fullest thing a
   human contributor can read.

Two things hold across all of them:

- **The Node version is pinned in `.tool-versions`**, and CI resolves it from
  that file. Installing under a different version can rewrite the lockfile in
  ways that only fail on a CI runner. If `node --version` disagrees, prefix the
  command with `mise exec node@<version> --`.
- **The formatter is not the same everywhere.** Some repositories use oxfmt and
  some use Prettier, and reaching for the wrong one reformats the whole tree.
  Check the repository's own Commands section rather than assuming.

## New Features

Open an issue before building anything substantial, so the approach can be
agreed before it is written. Small, self-contained fixes do not need one.

## Submitting Changes

- Open a new pull request.
- Describe what the change does and why, from the reviewer's side.
- Reference any issue it closes with `Closes #N`.

**Your pull request title matters more than your commit messages.** Pull
requests are squash-merged with the title as the commit subject and an empty
body, so that title becomes the only commit on `main` and your branch commits
never reach history. It is also what `release-please` parses to decide the next
version and write the changelog:

| Title starts with | What gets released |
| ----------------- | ------------------ |
| `feat:`           | a minor            |
| `fix:` or `deps:` | a patch            |
| anything else     | nothing            |

A `!` after the type marks a breaking change. Below 1.0.0 that takes a minor
rather than a major, so check where the package's version actually is.

Some repositories check the title with commitlint and fail the build on a
malformed one; others do not check it at all, which means a mistake there is
silent rather than caught. Write it carefully either way.

Write your branch commits conventionally as well. They are what a reviewer
reads while the pull request is open, even though only the title survives.

## Attribution

This Contributing Guide is adapted from the
[React Redux Contributing Guide](https://github.com/reduxjs/react-redux/blob/master/CONTRIBUTING.md).
