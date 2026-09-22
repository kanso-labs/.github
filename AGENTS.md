# AGENTS.md

Guidance for coding agents working in this repository.

## What this is

The organization's community health files, which GitHub serves to every
repository in `kanso-labs` that carries no copy of its own, plus the canonical
conventions the repositories restate and the shared Renovate preset they
extend.

**[`README.md`](README.md) is the reference, and this file does not repeat it.**
It lists which paths GitHub serves and which it does not, the three rules that
govern editing anything here, and why `CONVENTIONS.md` and `LICENSE.md` live in
a repository that serves neither. Read it before changing a file.

Duplicating it here would create exactly the drift this repository exists to
remove: two descriptions of one contract, diverging the first time only one of
them is updated.

## What is different about working here

**A change here reaches every repository immediately.** There is no release, no
tag and no pin: GitHub reads these files from `main`. So a half-finished edit to
`CODE_OF_CONDUCT.md` is live the moment it is pushed, in six repositories at
once.

`default.json` is the same, by a different route. Renovate resolves
`local>kanso-labs/.github` from `main` on every run, so a change to the shared
preset reaches every managed repository within three hours — and a malformed
one does not fail loudly, it errors each repository's config resolution. There
is no CI here to catch it, so validate a change against a consumer before
merging: add the setting to that repository's own config on a branch and run
`renovate-config-validator --strict` there.

**Nothing formats or lints this repository.** There is no `package.json`, no
Prettier and no oxfmt — the same arrangement as `renovate`. Match the
surrounding style by hand: prose wrapped at 80 columns, tables left to run past
it.

**`CONVENTIONS.md` is copied into five `AGENTS.md` files, by hand.** A change to
it is six pull requests, and nothing fails if you only make one. That is stated
in the file itself, under "Keeping the copies in step", and it is the one thing
here most likely to go quietly wrong.

## Commands

None. There is nothing to build, test or format.
