# Security Policy

This policy covers every repository in the
[kanso-labs](https://github.com/kanso-labs) organization.

## Supported Versions

Only the latest release of a given package is maintained. Fixes land on `main`
and ship in the next release rather than being backported, so upgrading is the
remedy for every vulnerability we fix.

| Version | Supported |
| ------- | --------- |
| Latest  | Yes       |
| Older   | No        |

## Reporting a Vulnerability

**Do not open a public issue.**

Use GitHub's private vulnerability reporting, which is enabled on every
repository here. On the affected repository, open the **Security** tab and
choose **Report a vulnerability**. That opens a private advisory only the
maintainers can see, and it is the preferred channel because the discussion,
the fix and the CVE all stay in one place.

If you cannot use it, email **vulnerability@kansolabs.org**. Say which
repository you mean — this address covers all of them.

Please include the steps to reproduce, the version you are on, and enough of
your environment to place the report: the runtime version, and whatever else
the affected project is built against. Each repository's own documentation
names the versions worth reporting for it.

We will acknowledge a report and tell you whether we consider it a
vulnerability. If it is, we will agree a disclosure timeline with you before
publishing.

## Scope

Most of what this organization publishes runs at build time or in CI rather
than in an end user's browser: a bundler plugin, a component library compiled
ahead of a consumer's build, shared GitHub Actions workflows, a self-hosted
dependency-update runner, and container images installed on a user's own
hardware. Judge a report against what the affected project actually does.

Two things are worth knowing before deciding whether something is a
vulnerability here:

- **A build-time tool that reads a project's configuration usually runs it.**
  Loading a JavaScript or TypeScript config file means executing it, so any
  validation happens after its side effects. Where a project can turn that
  discovery off, it documents how.
- **Every `npm ci` in CI passes `--ignore-scripts`**, and automerged dependency
  upgrades wait out a release-age grace period before they can land.

A repository with caveats of its own records them in its `README.md` or
`AGENTS.md`.
