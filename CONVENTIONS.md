# Conventions

The conventions shared by every repository in the
[kanso-labs](https://github.com/kanso-labs) organization.

**This file is the canonical copy.** Each repository restates the bullets below
in its own `AGENTS.md`, under the heading
`Shared with the other kanso-labs repositories`, because an agent handed one
repository on its own reads that file and never sees this one. The duplication
is deliberate and the copies are checked against this text rather than trusted
— see "Keeping the copies honest" at the end.

**Edit between the markers, and expect to edit six files.** The
`shared-conventions` comments below delimit what the check compares, in this
file and in every copy. Changing the text here turns every repository's `Lint`
red until its copy follows, which is the mechanism working rather than failing
— but it means a change to the shared set is six pull requests, not one.

Unlike the other files here, GitHub does not serve this one to anything. It is
a plain document in the `.github` repository, which is simply the one place in
the organization that belongs to no single repository.

## The shared set

<!-- shared-conventions:start -->

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

<!-- shared-conventions:end -->

## Two notes that travel with them

**The `.tool-versions` rule reaches further than it looks.**
`actions/setup-node` defaults `node-version-file` to `.tool-versions`, in
`github-actions` and in every consumer, so that file is what a run actually
resolves. A version written into prose beside it goes stale on the next
Renovate bump while the pin moves on — so where a document needs to name the
version in a command, it reads it out of the file rather than repeating it:

```shell
mise exec node@"$(awk '/^nodejs/{print $2}' .tool-versions)" -- npm install
```

**Formatting is not shared, and assuming it is will send you to a command that
does not exist.** oxfmt formats `kanso-ui` and `unplugin-style-dictionary`;
Prettier formats `github-actions` through an `npm run format` script and
`home-assistant-applications` through bare `npx`, which has no root
`package.json` and so no script at all; `renovate` has no formatter. A roster of
what each one runs belongs in each one rather than here. Read the Commands
section of whichever repository you are actually in before reaching for a
formatting command.

## Keeping the copies honest

Nothing above is enforced by GitHub. The copies in each `AGENTS.md` are checked
against this file by a composite action in
[`kanso-labs/github-actions`](https://github.com/kanso-labs/github-actions),
called from each repository's `Lint` workflow.

The action lives there because that is where anything a workflow `uses:` lives.
The text lives here because reading it out of `github-actions` would make one
consumer repository the authority over its four peers; `.github` is nobody's
peer.
