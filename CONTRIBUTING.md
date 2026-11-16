# Contributing

Thanks for your interest in Mothfire Labs. We're a small, early-stage research lab, and questions, ideas, problems,
and pointers to related work help us as much as code does.

Everyone taking part — in issues, pull requests, and anywhere else — is expected to follow our
[code of conduct](CODE_OF_CONDUCT.md).

## Issues

- Search first. If an issue already covers it, add to that one.
- Choose a form: **Report a problem** for something wrong or unclear, **Suggest an idea** for a feature, a research
  question, or related work.
- Found a security problem? Don't open an issue; follow our [security policy](SECURITY.md).

## Pull requests

1. For anything bigger than a small fix, open an issue first, so we can agree on the approach before you write code.
2. Keep each pull request to one change, and link the issue it addresses.
3. Run the project's checks — its `AGENTS.md` lists how to set it up, check, and test it. CI runs them too, and must
   pass.
4. Update the docs, and the `Unreleased` section of `CHANGELOG.md`, if users will notice the change. If it could
   change performance, run the benchmarks described in `docs/benchmarks.md`.
5. We squash-merge, so the pull request's title becomes the commit message. Write it as a short imperative sentence:
   "Fix a broken link in the README".

A maintainer reviews every pull request before it merges. You're welcome to use AI tools; you're responsible for what
you submit, so review it and make sure it works, as you would your own code.

Contributions are licensed under the project's license — Apache-2.0, unless the project says otherwise — as section 5
of that license provides. We don't ask for a contributor license agreement.

## How we work

Project stages, milestones, decisions, and releases work the same way in every repository. They're described in our
[playbook](PLAYBOOK.md).
