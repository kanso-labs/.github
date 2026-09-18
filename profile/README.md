# Kanso Labs

Design tokens, a component library built on them, the Home Assistant
applications that use it, and the shared CI that releases all of it.

_Kanso_ (簡素) is the Japanese principle of simplicity through elimination —
not what can be added, but what can be taken away. It is the working standard
here rather than a name: one canonical copy of anything shared, no dependency
left on a range, and a reason written down beside every decision that looked
obvious at the time.

## What is here

| Repository                                                                             | What it is                                                                                       |
| -------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| [kanso-ui](https://github.com/kanso-labs/kanso-ui)                                     | A React component library on React Aria Components, styled with StyleX. Every token carries a default, light and dark, so a component renders correctly the moment it is imported. |
| [unplugin-style-dictionary](https://github.com/kanso-labs/unplugin-style-dictionary)   | Compiles Style Dictionary design tokens ahead of your bundler. One implementation targets Vite, Rolldown, Rollup, Rspack and Webpack, with watching and HMR under Vite. |
| [home-assistant-applications](https://github.com/kanso-labs/home-assistant-applications) | Home Assistant applications for the arr stack, Plex, qBittorrent, NZBGet, Seerr and n8n. aarch64 and amd64, kept current automatically. |
| [actions](https://github.com/kanso-labs/actions)                                       | The shared CI surface — composite actions and reusable workflows, consumed by every repository above. |
| [renovate](https://github.com/kanso-labs/renovate)                                     | The self-hosted Renovate runner. One scheduled workflow keeps dependencies current everywhere, with `@renovate` comment commands. |
| [.github](https://github.com/kanso-labs/.github)                                       | This repository: the community health files every repository inherits, and the conventions they share. |

**[kanso-ui.kansolabs.org](https://kanso-ui.kansolabs.org/)** documents every
component in Storybook, published from the latest release.

## How this organization works

**Shared documentation lives once.** The code of conduct, contributing guide,
security policy and issue templates are served from this repository to every
other one. A repository carrying its own copy has overridden the default on
purpose, and says why in its `AGENTS.md`.

**Every repository writes for coding agents as well as people.** `AGENTS.md`
is the fullest reference in each: the conventions, the reasoning behind them,
and the traps that have already caught someone. It is worth reading even if you
never run an agent.

**Nothing is pinned loosely.** Dependencies are exact versions, actions are
exact tags, and language runtimes are fully specified in `.tool-versions`.
Renovate opens every bump.

## Contributing

Issues and pull requests are welcome on any repository. See
[CONTRIBUTING.md](https://github.com/kanso-labs/.github/blob/main/CONTRIBUTING.md)
for how to report and submit,
[SUPPORT.md](https://github.com/kanso-labs/.github/blob/main/SUPPORT.md) for
where each kind of question belongs, and
[SECURITY.md](https://github.com/kanso-labs/.github/blob/main/SECURITY.md) for
reporting a vulnerability privately.

Everything here is MIT licensed.
