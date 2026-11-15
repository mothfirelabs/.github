# Mothfire Labs playbook

How we run projects at Mothfire Labs. It's deliberately light: enough shared structure that every project looks and
works the same from the outside, and no more. Each project owns its scope, its roadmap, and its releases, and none
depends on another. The [organization profile](https://github.com/mothfirelabs) lists the projects.

## Names

- **Repository:** `mothfire-<name>`, lowercase.
- **Public name:** "Mothfire <Name>". Use the full name in titles, headings, and the first mention in any text; the
  short name alone is fine after that. Common words are too ambiguous to stand alone.
- **Web page:** `https://mothfirelabs.github.io/projects/<name>/`.
- **Packages,** once there are any: `mothfire-<name>`, wherever the registry allows it.

## Stages

Every project is in exactly one stage, and says which in its README, on its web page, and on the organization profile.
A project moves on only when it meets the condition in the last column — not on a schedule.

| Stage | What it means | Moves on when |
| --- | --- | --- |
| **Research exploration** | We're studying the problem; any code is an experiment. There's nothing to install. | The charter is ratified, the repository has code that runs, and the roadmap defines a first release. |
| **Active development** | We're building toward a first release. The code is public, but expect it to change. | A tagged release is published with release notes. |
| **Publicly released** | Versioned releases with release notes, ready for others to use. | — |

If we stop working on a project, we say so in its README and on its page, and archive the repository when it's done.

## What every repository has

| File | What it's for |
| --- | --- |
| `README.md` | The standard header (below), what the project is, its stage, and how to follow along. |
| `LICENSE` | The Apache License 2.0, unless a recorded decision says otherwise (see [licensing](#contributions-and-licensing)). |
| `CHARTER.md` | Why the project exists: the problem, goals, non-goals, audience, and open questions. Changing it is a [decision](#decisions). |
| `ROADMAP.md` | What we're working on now, next, and later. No dates until we can keep them. |
| `CHANGELOG.md` | User-facing changes in [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) format, newest first, under `Unreleased` until released. |
| `AGENTS.md` | Context and ground rules for AI coding agents such as GitHub Copilot. Update it when the toolchain or conventions change. |
| `docs/landscape.md` | Related work: what exists, what we learn from it, and where the project differs. |
| `docs/decisions/` | One short record per [decision](#decisions). |

The contribution guide, code of conduct, security policy, and issue and pull request templates come from this
repository, so they're the same everywhere. A project adds its own only when it needs something different.

Every README starts the same way, with the tagline copied from the project's web page:

```md
<a href="https://mothfirelabs.github.io/projects/<name>/"><img src="https://mothfirelabs.github.io/brand/mark.svg" alt="" height="40"></a>

# Mothfire <Name>

**<Tagline.>**

**Stage:** <stage> · [Website](https://mothfirelabs.github.io/projects/<name>/) · [Charter](CHARTER.md) · [Roadmap](ROADMAP.md) · [Blog](https://mothfirelabs.github.io/blog/)
```

## Repository settings

- **About:** the tagline as the description, the project's web page as the website, and topics that include
  `mothfire-labs`.
- **Features:** issues on; wiki and projects off. Documentation lives in the repository, where it's versioned and
  reviewed like code.
- **Pull requests:** squash merging only, and head branches deleted after merging.
- **Default branch:** `main`.

## Issues and milestones

- **Anyone can open an issue,** using the forms from this repository: _Report a problem_ or _Suggest an idea_.
- **Labels:** GitHub's defaults, plus two of our own:
  - `research`: an open question or an experiment to run.
  - `decision`: a choice to make, then record (see [Decisions](#decisions)).
- **Milestones** are named `M<n> — <Outcome>`, starting with `M0 — Foundation`, and describe an outcome rather than a
  list of tasks. They get a due date only when we mean to keep it.
- **Every project starts with `M0 — Foundation`:** ratify the charter, choose a toolchain, and define the first
  experiment.

## Decisions

Decisions that shape a project — its scope, license, toolchain, or public interfaces — are discussed in an issue
labeled `decision`. Once made, they're recorded in `docs/decisions/NNNN-short-title.md`, numbered in order and never
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

## Contributions and licensing

- **License:** every project is licensed under the
  [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0), unless a recorded decision says otherwise. Model
  weights and datasets get their terms with each release, stated in their cards.
- **Contributions** are accepted under the project's license, as section 5 of the Apache License provides. We don't ask
  for a contributor license agreement.
- **Conduct:** everyone taking part follows our [code of conduct](CODE_OF_CONDUCT.md).
- Pull requests change one thing, link the issue they address, and update the docs and `CHANGELOG.md` when users will
  notice the change.

## Releases

1. **Versions** follow [Semantic Versioning](https://semver.org), starting at `0.1.0`. While a project is at `0.x`, a
   minor version may break things; the changelog says how.
2. **To release,** move the `Unreleased` changes in `CHANGELOG.md` under the new version and date, tag `vX.Y.Z` on
   `main`, and publish a GitHub release with the same notes.
3. **Artifacts** go where people look for them: code packages on the language's registry, model weights and datasets on
   a model hub. Each project's README says where.
4. **Notable releases** get a blog post with `topic: releases`.
5. **A project's first release** moves it to _Publicly released_. Update its stage everywhere (see
   [Keeping things in sync](#keeping-things-in-sync)).

## Writing in public

- **The blog is our one publication channel:** [mothfirelabs.github.io/blog](https://mothfirelabs.github.io/blog/). Every
  post has one topic — Research, Engineering, Releases, or Announcements — and lists the projects it's about, so readers
  can follow a topic or a project. The website's README explains how to write a post.
- **Say only what's true today.** No results we don't have, capabilities we haven't built, or dates we can't keep. Mark
  hypotheses as hypotheses.
- **Write plainly,** and use the project's full name on first mention.

## Keeping things in sync

A project's name, tagline, and stage appear in four places. When one changes, change all four:

1. The project's `README.md` header.
2. The repository's description and website, under **About**.
3. The project's page on the website: `src/content/projects/<name>.md` in the website's source repository,
   `mothfirelabs/mothfire-web`.
4. The organization profile: [`profile/README.md`](profile/README.md) in this repository.

## Starting a project

1. Draft a charter, following the structure of an existing one.
2. Create `mothfirelabs/mothfire-<name>` with the files above, and apply the settings and labels.
3. Create `M0 — Foundation` with its issues.
4. Add the project to the website and the organization profile.
5. Announce it on the blog when it's ready to be public.
