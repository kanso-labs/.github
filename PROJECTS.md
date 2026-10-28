# Projects

How the [kanso-labs](https://github.com/kanso-labs) organization tracks work in
[GitHub Projects](https://github.com/orgs/kanso-labs/projects): what an issue
carries, what a project holds, and which views and workflows every project has.

**This file is the standard, and the Default Project Template is its
implementation.** A new project is copied from the template, so the fields,
views and workflows below are what a copy starts with. A project's own README
says only what is particular to it: the repositories it covers, where its items
came from, its Area options and any field it adds. Nothing here is repeated in
a project's README, so the two cannot drift.

GitHub serves this file to nothing. It sits in the `.github` repository because
that is the one place in the organization that belongs to no single repository.

## One home for each fact

**Every fact about a piece of work is recorded in exactly one place.** The
projects this standard replaces wrote the kind of work five times over: in a
project field, in a `kind:` label, in the issue type, in the title's
Conventional Commit prefix and in a line of the issue's body. Area, size and
phase were written two or three times each, and every audit found copies that
disagreed. A fact with one home cannot disagree with itself.

So each fact lives where GitHub keeps it natively, and nowhere else:

| Fact | Its one home | Not in |
| --- | --- | --- |
| What kind of work | The issue type | Labels, project fields, the body |
| The finer kind | The title's Conventional Commit prefix, `refactor(…)` | Anything else |
| What it belongs to | Its parent issue | A phase, a module field, a label |
| What must land first | Its blocked-by links | A "Depends on" section, phase numbers |
| How much it matters | The Priority issue field | A "Quick wins" bucket, column position |
| How big it is | The Effort issue field | A Size field, the body |
| Which release needs it | Its milestone | A phase |
| Where it stands | The project's Status field | A phase, a label |
| Which part it touches | The project's Area field | `area:` labels, the body |
| Which platform | Its repository | A Platform field, `platform:` labels |

Issue types, issue fields, sub-issues and blocked-by links belong to the issue
rather than to a project, so they show wherever the issue does: in its
repository, in search and on any project it sits on. Status and Area are
project fields because their meaning is the project's.

## Issues

### Types

The organization defines six issue types, and every issue carries one:

| Type | For |
| --- | --- |
| Epic | An outcome too big for one pull request, delivered by its sub-issues |
| Feature | Something the project does not do yet |
| Bug | Behaviour the project has and gets wrong |
| Task | Work that adds no behaviour and fixes none: tooling, CI, docs, tests, refactors |
| Decision | A choice to make before the work that assumes it |
| Spike | A question answered by experiment before anything is built |

The finer distinction a Task used to carry — docs, test, refactor, perf,
tooling — is already in its title. Titles are Conventional Commits,
`feat(…)`, `fix(…)`, `docs(…)`, because the title becomes the pull request's
title and release-please reads that.

### Bodies

A body says what the work is and how to know it is finished. It carries no
metadata: no Phase, Size, Kind or Area line, and no "Depends on" section, since
each of those has a home of its own above.

| Type | Sections |
| --- | --- |
| Feature, Bug, Task | What it is · What to build · How to know it worked · Definition of done |
| Epic | The outcome · In scope · Out of scope |
| Decision | The question · Options · Recommendation, then Decision once it is taken |
| Spike | The question · The experiment · What each answer changes |

A bug filed through the organization's bug report form keeps the form's own
sections instead.

### Epics and sub-issues

**An epic owns its work across repositories.** Its sub-issues may sit in any
repository its project covers, so one epic holds the web, the app and the shared
package's halves of a module, and the board shows them together. An epic lives
in the repository where most of its work does. It lists its work as sub-issues,
never as a task list in its body, so its progress is counted rather than ticked
by hand.

An epic may contain epics, for a programme the size of a new platform. The
board groups by the nearest parent, so keep that nesting shallow.

### Dependencies

**Order comes from blocked-by links, not from numbering.** Mark an issue as
blocked by the issues that must land first. An issue that something open still
blocks is not Ready, and GitHub shows the block on the issue, in search and on
the board. Phases used to encode the same thing more coarsely, and could not say
which items within a phase waited on which.

### Decisions and spikes

A Decision is an issue, never a draft item, so the work that assumes it can link
to it. An open one carries a recommendation. A taken one records the choice
under Decision and is closed as completed. A Spike is closed once its question
has an answer, and the answer is in it.

## Issue fields

Two of the organization's issue fields are part of the standard, and every issue
on a project carries both once it leaves Backlog:

- **Priority** — Urgent drops other work; High is next; Medium is the default;
  Low waits for room.
- **Effort** — Low is under half a day, Medium one to two days, High more.
  Relative effort, not a schedule.

**Start date** and **Target date** are optional. Set them where a date is real,
such as a release someone is waiting on, and a project's timeline view picks
them up.

The issue fields are visible to the organization's members only, so a
contributor outside it does not see them on a public repository. GitHub also
refuses to make a project public while it shows a field visible to members
only, which the Rollout section below takes up.

## Projects

### One project per product

**A project covers a product, not a repository.** A product that spans
repositories — a web app, its native app and the package they share — is one
project linked to all of them, so an epic and its sub-issues sit on one board.
The repositories that serve the whole organization share one project too, Kanso
Labs. List the projects and the repositories each one covers with:

```shell
gh api graphql -f query='{organization(login:"kanso-labs"){projectsV2(first:50){nodes{number title repositories(first:20){nodes{name}}}}}}'
```

**Every issue in a linked repository is on its project,** except the ones a bot
files for itself, such as Renovate's Dependency Dashboard.

### Status

| Status | Means |
| --- | --- |
| Backlog | Filed and not yet triaged |
| Ready | Area, Priority and Effort are set, and nothing open blocks it |
| In progress | Being worked on |
| In review | A pull request is linked |
| Done | Closed |

New items land in Backlog, and the workflows below move them from In progress
on. Moving an item from Backlog to Ready is the triage, and is done by hand.

### Area

Area is the one field each project defines for itself: the parts of the product,
one option per part, so the table grouped by Area reads as a map of it. Keep it
to the parts work is planned around, which is rarely more than a dozen.

### Fields a project adds

A project may add a field the standard cannot guess, such as the design
artboard an item builds or the primitives a component is made from. Its README
names each one and what it holds. A field that restates something in the table
at the top of this file is not added.

### Milestones

A milestone is a release: it is named after the version release-please will
cut, `v1.0.0`, and holds the issues that release needs. Milestones belong to a
repository, so a project spanning several uses one per repository.

## Views

Every project has these views, in this order and with these names:

| View | Layout | Shows |
| --- | --- | --- |
| Board | Board | Every item but epics, in Status columns, one row per parent, by Priority |
| Triage | Table | Backlog, oldest first, with Area, Priority and Effort to fill in |
| Epics | Table | Epics, with their sub-issue progress, Priority, milestone and Target date |
| By area | Table | Open items but epics, grouped by Area |
| Open questions | Table | Open decisions and spikes |

A project that sets dates adds **Timeline**, a roadmap of Start date to Target
date.

## Workflows

Every project runs GitHub's built-in workflows with these settings:

| Workflow | Setting |
| --- | --- |
| Item added to project | Status: Backlog |
| Item reopened | Status: In progress |
| Pull request linked to issue | Status: In review |
| Pull request merged | Status: Done |
| Item closed | Status: Done |
| Auto-close issue | On, when Status is set to Done |
| Auto-add sub-issues to project | On |
| Auto-archive items | `is:issue is:closed updated:<@today-1w` |

Item reopened matters more than it looks: without it, an issue reopened after a
merged pull request stays Done.

## Labels

**A label is kept only where a bot or a contributor relies on it.** Issue types,
issue fields and project fields carry everything else, and a label alongside
them is one more copy to drift. [`labels.yaml`](labels.yaml) is the canonical
list:

- `labels` — every repository carries these, with this colour and description.
  release-please and Dependabot mark their pull requests with three of them,
  and GitHub shows `good first issue` and `help wanted` to new contributors.
- `retired` — deleted from every repository. A trailing `*` matches every
  label with that prefix.

A label in neither list is left alone. Dependabot creates ecosystem labels such
as `javascript` for itself, and removing them only makes it create them again.

## Starting a project

1. Copy the Default Project Template, and rename the copy after the product.
2. Link it to the product's repositories.
3. Replace the template's Area options with the product's own parts.
4. Rewrite its README: the repositories it covers, where its items came from,
   its Area options and any field it adds.
5. Add every open issue in those repositories, and triage each out of Backlog.

## Rollout

The standard is ahead of the organization in four places, and this section
goes once each is done.

- **Public projects.** Priority, Effort, Start date and Target date are visible
  to the organization's members only, and GitHub will not make a project
  public while it shows one of them. So the Kanso Labs project is private for
  now, and Kanso UI, Unplugin Style Dictionary, Home Assistant Applications and
  Robot Vacuum Map, which are public, cannot take the fields as they stand.
  Making the four fields visible to everyone settles it for all of them.

- **Adding issues to projects.** A reusable `_add-to-project.yaml` in
  [`kanso-labs/actions`](https://github.com/kanso-labs/actions), run on
  `issues: opened` through the organization's GitHub App, is still to come. A
  project's built-in auto-add workflow covers only one repository on GitHub
  Free, which leaves the others of a multi-repository project uncovered.
- **Syncing labels.** A reusable workflow that applies `labels.yaml` to every
  repository is still to come, so the retired labels are still in place. They
  go once each project has migrated, since its items still use them.
- **The existing projects.** Kanso UI, Unplugin Style Dictionary, Home
  Assistant Applications, Daily and Robot Vacuum Map predate the standard.
  Each migrates in this order, so no value is lost before it has a new home:
  1. Kind becomes the issue type: Fix → Bug; Feature, Component, Variant,
     Integration and Application → Feature; Decision → Decision; Spike →
     Spike; everything else → Task.
  2. Size becomes Effort: S → Low, M → Medium, L → High. Where an issue
     already has an Effort that disagrees, Size wins, since it was the planned
     value.
  3. Each phase becomes what it meant: a module or programme becomes an epic
     with its items as sub-issues, a release becomes a milestone, Decisions
     and Quick wins dissolve into the issue type and Effort, and Later becomes
     Backlog with Low priority.
  4. "Depends on" sections become blocked-by links.
  5. The project's views and workflows are set as above.
  6. Phase, Kind, Size and Platform are deleted, and the repository's `kind:`,
     `area:` and `platform:` labels with them. Archived items are migrated
     too, since deleting a field clears its value on them.
  7. The repository's `AGENTS.md` stops describing the old fields and points
     here.
