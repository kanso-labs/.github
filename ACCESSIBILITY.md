# Accessibility

This statement covers every repository in the
[kanso-labs](https://github.com/kanso-labs) organization. It says what we aim
for, what is checked automatically today, what is not, and how to tell us about
a barrier.

## Our Commitment

We aim for [WCAG 2.2](https://www.w3.org/TR/WCAG22/) level AA in everything a
person uses directly. A barrier that stops someone using one of our projects is
a bug, and we treat it as one rather than as an enhancement.

## What This Covers

Most of what this organization publishes has no interface of its own: a bundler
plugin, shared GitHub Actions workflows, a dependency-update runner and a Home
Assistant integration. The Home Assistant applications package other projects'
web interfaces, so a barrier inside one of those belongs with its upstream
project.

The statement applies to the projects people use directly:

| Project                                                                      | What is checked                                                              |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| [kanso-ui](https://github.com/kanso-labs/kanso-ui)                           | Every Storybook story, through axe, on every pull request                    |
| [react-native-kanso-ui](https://github.com/kanso-labs/react-native-kanso-ui) | Every story as React Native Web draws it, through axe, on every pull request |
| Daily                                                                        | Every route, through axe against WCAG 2.2 A and AA, on every pull request    |
| [kansolabs.org](https://kansolabs.org/)                                      | Built from kanso-ui components; the page itself is not scanned               |
| [docs.kansolabs.org](https://docs.kansolabs.org/)                            | Drawn by Mintlify's theme, which we do not control                           |

## How It Is Checked

**kanso-ui** is built on React Aria Components, which supplies keyboard
interaction, focus management and ARIA semantics.

- Every story runs through axe in headless Chromium, through Storybook's
  accessibility addon, and a violation fails the build.
- Every colour pair a component renders has to clear WCAG AA contrast, 4.5:1
  for text, in the light and dark themes alike.
- Focus indicators and control boundaries are drawn as borders or outlines,
  never as shadows alone, so they survive forced-colours modes such as Windows
  High Contrast.
- Components that animate drop their transitions under
  `prefers-reduced-motion`.
- An open overlay carries a visually hidden dismiss button for screen readers,
  named in the reader's language.

**react-native-kanso-ui** renders every story through React Native Web in
Chromium and runs it through axe, and a contrast or labelling violation fails
the build.

**Daily**'s end-to-end tests run axe against WCAG 2.2 A and AA on every route.
Each route is scanned in the light and dark themes, at a phone's width and a
desktop's, and again with focus inside a form field. A separate test checks
where focus lands as a person moves by keyboard.

## Known Limitations

- **Every automated check runs in Chromium.** Nothing scans Firefox or Safari.
- **No test drives a screen reader.** axe finds missing names, roles and
  contrast failures. It cannot say whether a page makes sense read aloud.
- **No test switches a browser into reduced motion or forced colours.**
  kanso-ui's tests read the compiled stylesheet to confirm the rules for both
  are written, which is not the same as watching a browser apply them.
- **react-native-kanso-ui is checked on the web, not on a phone.** The checks
  see what React Native Web draws, not what VoiceOver or TalkBack read from the
  native components.
- **kansolabs.org is not scanned as a page**, beyond the checks its kanso-ui
  components pass on their own.
- **docs.kansolabs.org uses Mintlify's theme**, so a barrier in the theme may
  need fixing upstream rather than here.

## Reporting a Barrier

Open an issue on the repository concerned, using its bug report form. Say what
you were trying to do, what got in the way, and what you were using: the
assistive technology and its version, the browser and the operating system.

If the project has no public repository, as with Daily, or you are not sure
which repository a barrier belongs to, open the issue on
[kanso-labs/.github](https://github.com/kanso-labs/.github/issues) instead.

## Contributing

A change to a component or a page keeps the checks above passing. Each
repository's `AGENTS.md` records how its checks run, and why any axe rule is
narrowed rather than met. kanso-ui narrows two, each for a documented gap in
axe rather than in a component.

This file lives in `kanso-labs/.github` and is served to every repository that
does not carry its own. It changes when a project's checks do.
