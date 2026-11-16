# Mothfire Labs playbook

How we plan, build, and release at Mothfire Labs. It's deliberately light: enough shared structure that every project
works the same way — for people, and for the AI agents we build with — and no more. Each project owns its scope, its
design, its roadmap, and its releases, and none depends on another. The
[organization profile](https://github.com/mothfirelabs) lists the projects.

## Principles

- **Build for what's new.** Target today's models, hardware, and agent workflows, and don't carry support for older
  ones. Having no legacy to support is an advantage; design to use it.
- **Do the essential, completely.** Solve the core problem fully, and leave auxiliary features out until people need
  them. Every feature has to earn its place in the design.
- **Benchmark from the start.** Every project names its benchmarks and baselines in its design, measures the strongest
  alternatives before its own system runs, and measures itself at every milestone, so each release can show where it
  stands.
- **First releases are complete.** The first public version number is small — v0.1 — but the release meets the full
  [release bar](#the-release-bar).
- **Design before code; docs as code.** Designs, decisions, and documentation live in the repository and change
  through pull requests, like code.
- **Use what we build.** We use each project in our own work before we release it.
- **Say only what's true.** No results we don't have, capabilities we haven't built, or dates we can't keep. Mark
  hypotheses as hypotheses.

## Names

- **Repository:** `mothfire-<name>`, lowercase.
- **Public name:** "Mothfire <Name>". Use the full name in titles, headings, and the first mention in any text; the
  short name alone is fine after that. Common words are too ambiguous to stand alone.
- **Web page:** `https://mothfirelabs.github.io/projects/<name>/`.
- **Packages:** `mothfire-<name>`, wherever the registry allows it.

## Stages

Every project is in exactly one stage, and says which in its README, on its web page, and on the organization profile.
A project moves on only when it meets the condition in the last column — not on a schedule.

| Stage | What it means | Moves on when |
| --- | --- | --- |
| **Research exploration** | We're studying the problem and designing the first release. | The charter is ratified and the design accepted. |
| **Active development** | We're building the first release, in a private repository until it ships. | The first release meets the [release bar](#the-release-bar) and is published. |
| **Publicly released** | The repository is public, and versioned releases ship with release notes. | — |

Projects move through the stages independently, and each goes public with its own first release
([going public](#going-public)). If we stop working on a project, we say so in its README and on its page, and archive
the repository when it's done.

## What every repository has

| File | What it's for |
| --- | --- |
| `README.md` | The standard header (below), what the project is, its stage, and how to follow along. |
| `LICENSE` | The Apache License 2.0, unless a recorded decision says otherwise (see [licensing](#contributions-and-licensing)). |
| `CHARTER.md` | Why the project exists: the problem, goals, non-goals, audience, principles, and open questions. Changing it is a [decision](#decisions). |
| `ROADMAP.md` | What we're working on now, next, and later. No dates until we can keep them. |
| `CHANGELOG.md` | User-facing changes in [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) format, newest first, under `Unreleased` until released. |
| `AGENTS.md` | Context, commands, and ground rules for AI coding agents such as GitHub Copilot — and for people. |
| `docs/design.md` | How the next release will work — components, formats, and milestones — written before it's built. |
| `docs/benchmarks.md` | What we measure, against which baselines, how, and every result so far (see [benchmarks](#benchmarks)). |
| `docs/landscape.md` | Related work: what exists, what we learn from it, and where the project differs. |
| `docs/decisions/` | One short record per [decision](#decisions). |
| `.github/CODEOWNERS` | Who reviews what; every pull request requests a review from its owners. |
| `.github/workflows/` | CI, which runs every check on every pull request, and `copilot-setup-steps.yml`, which gives Copilot cloud agent the same environment. |
| `.github/dependabot.yml` | Monthly, grouped updates for dependencies and Actions. |

The contribution guide, code of conduct, security policy, and issue and pull request templates come from this
repository, so they're the same everywhere. A project adds its own only when it needs something different.

Every README starts the same way, with the tagline copied from the project's web page:

```md
<a href="https://mothfirelabs.github.io/projects/<name>/"><img src="https://mothfirelabs.github.io/brand/mark.svg" alt="" height="40"></a>

# Mothfire <Name>

**<Tagline.>**

**Stage:** <stage> · [Website](https://mothfirelabs.github.io/projects/<name>/) · [Charter](CHARTER.md) · [Design](docs/design.md) · [Roadmap](ROADMAP.md) · [Blog](https://mothfirelabs.github.io/blog/)
```

## Repository settings

- **About:** the tagline as the description, the project's web page as the website, and topics that include
  `mothfire-labs`.
- **Features:** issues on; projects on, with the [board](#planning) linked; wiki off (see
  [documentation](#documentation)); Discussions on once the repository is public.
- **Pull requests:** squash merging only, with the pull request's title and description as the commit message; head
  branches deleted after merging.
- **Security:** Dependabot alerts and security updates on (see [code](#code)).
- **Default branch:** `main`, protected (see [code](#code)).

## Planning

- **One board.** The [Mothfire Labs project](https://github.com/orgs/mothfirelabs/projects/1) tracks the issues of
  every repository, with a Status (Todo, In Progress, In review, Done) and the organization's issue fields Priority
  (Urgent, High, Medium, Low) and Effort (Low, Medium, High). Its views — _By project_, grouped by milestone, and
  _Board_, by status — can be sliced by repository. An issue moves to In Progress when a pull request links it, and to
  Done when it closes.
- **Issues are the unit of work,** and every issue has a type:

  | Type | For |
  | --- | --- |
  | **Task** | A specific piece of work, such as a milestone in the design. |
  | **Bug** | Something wrong, broken, or unclear. |
  | **Feature** | A new capability, or an idea from outside. |
  | **Research** | An open question, or an experiment to run. |
  | **Decision** | A choice to make, then record (see [decisions](#decisions)). |

  An issue too big for one pull request is split into sub-issues; the parent shows their progress.
- **Milestones follow the design.** After `M0 — Foundation`, a repository's milestones are the milestones in its
  `docs/design.md`, named `M<n> — <Outcome>`, and the last one is the release. Each has one tracking issue of type
  Task — its goal, its scope, and how to check it's done, with a link to the design — and that issue is what a person
  or Copilot cloud agent picks up. Milestones get a due date only when we mean to keep it.
- **Triage:** within a few days, every new issue is on the board, with a type, a priority, and a milestone — or no
  milestone, which means later.
- **Labels** cover only what types and fields don't, such as `good first issue`.
- **Every week,** review the board — what moved, what's stuck, what's next — and sum it up in a status update on the
  board. Update the roadmap when a milestone closes.
- **Forms:** anyone can open an issue with _Report a problem_ or _Suggest an idea_; maintainers use _Task_,
  _Research question_, and _Decision_. The forms set the issue type, and add the issue to the board when the person
  opening it can edit the board.

## Code

- **Trunk-based.** `main` is always green and releasable. Work happens on short-lived branches and merges through pull
  requests, for people and agents alike.
- **Pull requests** change one thing, link the issue they address ("Closes #12"), pass CI, and update the docs and
  `CHANGELOG.md` when users will notice the change. Every pull request is reviewed before it merges: an agent's by a
  person, and a person's by a person or by Copilot code review. We squash-merge, so the title and description become
  the commit — the title a short sentence in the imperative mood, the description the why.
- **Protection:** `main` takes changes only through pull requests, keeps a linear history, and refuses force pushes
  and deletion; in an emergency, organization owners can merge a pull request that doesn't meet the rules. The rules
  are a repository ruleset, kept in [`rulesets/main.json`](rulesets/main.json); each project adds its CI checks as
  required. GitHub enforces rulesets in private repositories only on paid plans, so they apply when a repository goes
  public, or sooner if we upgrade.
- **Owners:** `.github/CODEOWNERS` requests reviews automatically.
- **AI agents** work like any contributor. `AGENTS.md` gives them the commands and the rules, `copilot-setup-steps.yml`
  prepares their environment, a milestone's tracking issue can be assigned to Copilot cloud agent, and their pull
  requests are reviewed like anyone's.
- **Dependencies** are added sparingly, locked, and kept current by Dependabot. A new language or tool is a decision.
- **Security:** Dependabot alerts and security updates are on everywhere. When a repository goes public, private
  vulnerability reporting, code scanning, and secret scanning with push protection are turned on too.

## Documentation

- **Docs live in the repository,** next to the code: versioned with it, reviewed in pull requests, and read by the
  agents that work on it. We don't use the GitHub wiki, which is versioned apart from the code, isn't reviewed, and
  drifts.
- **Every project documents:** why it exists (the charter), how the next release works (the design), why it's built
  the way it is (decisions), related work (the landscape), and where it stands (benchmarks). Once it's released, user
  documentation — a quick start, guides, and a reference — ships with the code.
- **The website** hosts the project pages and the blog. User documentation moves there when a project outgrows its
  README.

## Decisions

Decisions that shape a project — its scope, license, toolchain, or public interfaces — are discussed in an issue of
type Decision. Once made, they're recorded in `docs/decisions/NNNN-short-title.md`, numbered in order and never
renumbered:

```md
# NNNN. Title

- **Date:** YYYY-MM-DD
- **Status:** Accepted · or Superseded by [NNNN](NNNN-other-title.md)
- **Issue:** #123

## Context

What we needed to decide, and what constrained it.

## Decision

What we chose.

## Consequences

What follows, good and bad, and what we'd watch for.
```

## Benchmarks

- **Every project keeps `docs/benchmarks.md`:** the benchmarks it uses and why, the baselines — the strongest
  alternatives, configured fairly — the method, and every published result with its date, versions, hardware,
  configuration, and command.
- **Measure the baselines first,** before there's a system of our own to measure, so the project knows the bar it has
  to clear.
- **Measure at every milestone,** on a fixed subset, to show progress and catch regressions.
- **Keep it fair:** the same tasks, models, hardware, and budgets for every system, nothing measured on data a system
  was tuned on, and losses published alongside wins.
- **Publish with the release:** the comparison goes in the release post and in `docs/benchmarks.md`, with everything
  needed to run it again.

## Contributions and licensing

- **License:** every project is licensed under the
  [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0), unless a recorded decision says otherwise. Model
  weights and datasets get their terms with each release, stated in their cards.
- **Contributions** are accepted under the project's license, as section 5 of the Apache License provides. We don't ask
  for a contributor license agreement.
- **Conduct:** everyone taking part follows our [code of conduct](CODE_OF_CONDUCT.md).

## Releases

### The release bar

A release ships only when it is:

1. **Complete:** every milestone in the design is done, and the design and the docs describe what ships.
2. **Correct:** CI passes on every supported platform, tests cover every component, and there are no known critical or
   high-severity bugs.
3. **Measured:** the benchmarks are run against the baselines, and the results — wins and losses — are in
   `docs/benchmarks.md`.
4. **Documented:** a quick start that works from scratch, guides for the main uses, a reference for every command,
   format, and interface, and the changelog.
5. **Secure:** dependencies reviewed, permissions and secrets audited, and a threat model for anything that runs code
   or handles data.
6. **Used:** we've used it in our own work, and fixed what that turned up.
7. **Published properly:** packages install from their registry and are built in CI with provenance; model weights and
   datasets download from the Hugging Face Hub with their cards; everything carries its license and notices.

### How to release

1. **Versions** follow [Semantic Versioning](https://semver.org), starting at `0.1.0`. While a project is at `0.x`, a
   minor version may break things; the changelog says how.
2. **Prepare:** move the `Unreleased` changes in `CHANGELOG.md` under the new version and date, and tag `vX.Y.Z` on
   `main`.
3. **Publish from CI:** code packages to their registry with trusted publishing and provenance, model weights and
   datasets to the Hugging Face Hub, and a GitHub release with the changelog's notes.
4. **Announce** notable releases on the blog, with `topic: releases`.

### Going public

A project goes public with its first release, on its own schedule:

1. Make the repository public. Import the ruleset for `main` from [`rulesets/main.json`](rulesets/main.json), with the
   project's CI checks required, and turn on private vulnerability reporting, code scanning, secret scanning with push
   protection, and Discussions.
2. Mark its page on the website as public (`public: true` in `src/content/projects/<name>.md`), and set its stage to
   _Publicly released_ everywhere it appears (see [keeping things in sync](#keeping-things-in-sync)).
3. Add it to the organization profile, and to the Hugging Face organization card if it publishes there.
4. Publish the release post.

## Writing in public

- **The blog is our one publication channel:** [mothfirelabs.github.io/blog](https://mothfirelabs.github.io/blog/). Every
  post has one topic — Research, Engineering, Releases, or Announcements — and lists the projects it's about, so readers
  can follow a topic or a project. The website's README explains how to write a post.
- **Say only what's true today,** and mark hypotheses as hypotheses.
- **Write plainly,** and use the project's full name on first mention.

## Keeping things in sync

A project's name, tagline, and stage appear in up to five places. When one changes, change them all:

1. The project's `README.md` header.
2. The repository's description and website, under **About**.
3. The project's page on the website: `src/content/projects/<name>.md` in the website's source repository,
   `mothfirelabs/mothfire-web`.
4. The organization profile: [`profile/README.md`](profile/README.md) in this repository, once the project is public.
5. The [Hugging Face organization card](https://huggingface.co/spaces/mothfirelabs/README), once the project publishes
   there.

## Starting a project

1. Draft a charter, following the structure of an existing one.
2. Create `mothfirelabs/mothfire-<name>`, private, with the files above, and apply the settings.
3. Create `M0 — Foundation` with its issues: ratify the charter, write the design and the benchmark plan, choose a
   toolchain, and define the first experiment.
4. Add its page to the website, with `public: false` until it's released.
5. Announce it on the blog when it goes public.
