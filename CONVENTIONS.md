# Conventions

The conventions shared by every repository in the
[kanso-labs](https://github.com/kanso-labs) organization.

**This file is the canonical copy.** Each repository restates the bullets below
in its own `AGENTS.md`, under the heading
`Shared with the other kanso-labs repositories`, because an agent handed one
repository on its own reads that file and never sees this one. The duplication
is deliberate, and keeping the copies in step is done by hand — see "Keeping
the copies in step" at the end.

Unlike the other files here, GitHub does not serve this one to anything. It is
a plain document in the `.github` repository, which is simply the one place in
the organization that belongs to no single repository.

## The shared set

- **Keys in JSON and YAML are ordered by name.** Files whose order carries
  meaning are exempt: workflows, where step order is execution order;
  changelogs, which are chronological; and `package.json`, where the npm
  ecosystem expects `name` and `version` first.
- **A workflow's filename is the kebab-case of its `name:` field.** Reusable
  workflows, meaning those triggered only by `workflow_call`, take a leading
  underscore.
- **Job names and step names are imperative verb phrases.** Job ids, step ids,
  and matrix keys are exempt.
- **Actions are pinned to exact release tags**, `actions/checkout@v7.0.1`, never
  `@main` and never a tag the publisher moves — `@v7` and `@v7.0` both move.
  Renovate opens the bump pull requests, and it has nothing to open when the pin
  never changes: `frenck/action-app-linter@v2.21` sat still through a repository
  rename and a release that fixed something a consumer was working around,
  because the tag it named was moved onto both.
- **Dependency versions are pinned exactly.** Every `dependencies`,
  `devDependencies`, and `optionalDependencies` entry is a bare version,
  `1.2.3`, never `^1.2.3`, `~1.2.3`, `>=1.2.3`, `*`, `1.x`, or an `||` union.
  Renovate opens those bumps too. `peerDependencies` are the deliberate
  exception: they state what the consumer's own installed copy must satisfy, so
  ranges are correct there and stay.
- **`.tool-versions` pins a fully-specified version on every line**,
  `nodejs <major>.<minor>.<patch>`, never `nodejs 24` or `nodejs lts`.

## Two notes that travel with them

**The `.tool-versions` rule reaches further than it looks.**
`actions/setup-node` defaults `node-version-file` to `.tool-versions`, in
`actions` and in every consumer, so that file is what a run actually
resolves. A version written into prose beside it goes stale on the next
Renovate bump while the pin moves on — so where a document needs to name the
version in a command, it reads it out of the file rather than repeating it:

```shell
mise exec node@"$(awk '/^nodejs/{print $2}' .tool-versions)" -- npm install
```

**Formatting is not shared, and assuming it is will send you to a command that
does not exist.** oxfmt formats `kanso-ui` and `unplugin-style-dictionary`;
Prettier formats `actions` through an `npm run format` script and
`home-assistant-applications` through bare `npx`, which has no root
`package.json` and so no script at all; `renovate` has no formatter. A roster of
what each one runs belongs in each one rather than here. Read the Commands
section of whichever repository you are actually in before reaching for a
formatting command.

## Keeping the copies in step

Nothing enforces any of this. There is no check comparing a repository's copy
against this file, deliberately — the organization decided the cost of one was
not worth what it would catch.

So a change to the shared set is a change to six files, and the discipline is
the only thing holding them together:

1. Edit this file first. It is the one that is right by definition.
2. Open a pull request per repository carrying the same edit.

A copy that has drifted is not wrong because it disagrees with a checker. It is
wrong because the next agent to read it will follow it.
