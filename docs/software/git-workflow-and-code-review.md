# Software: Git workflow and code review

Document type: realistic sample document for the fictional Cedar Works demo company.
Classification: team-specific; Software.
Document owner: Software engineering lead.
Created: 2026-11-04 (simulated source date).
Last updated: 2026-11-09 (simulated source date).
Review status: AI-drafted; pending Evan's review for accuracy and realism.

This is synthetic evaluation content. Branch rules, approval requirements, and workflows describe fictional Cedar Works practices, not adopted company policy. Dates are simulated source metadata, not Git commit timestamps.

## Start a focused branch

Cedar Works uses a protected `main` branch and short-lived branches named for their purpose, such as `feature/course-progress`, `fix/duplicate-invitation`, or `docs/release-checklist`. Confirm the repository and current branch before editing. Fetch the latest remote state and start new work from an up-to-date `main`; do not discard local changes to make the checkout clean.

Keep one logical change in a branch. A change that spans independently versioned repositories needs a separate branch and review request in each repository, with the compatibility and release order explained. Follow the [backend development guide](backend-development.md) for the local environment rather than copying dependencies or configuration from another repository.

## Prepare commits and review evidence

Use descriptive commit messages that explain the behavior being changed. Stage only intended files, inspect the staged diff, and exclude generated credentials, ignored `.env` files, database dumps, and local build output. If a dependency changes, include its manifest and lockfile together.

Before requesting review, run the affected tests and repository-required checks. Include the command, result, and any known limitation in the review description. A schema change also requires the full integration suite against the migrated schema and the migration checks described in [Databases](databases.md). A passing targeted test does not replace those migration requirements.

## Open a PR or MR

A pull request (`PR`) and a merge request (`MR`) are names for the same review stage on different hosting platforms. This guide uses PR for either. Target `main`, explain the user-visible problem and resulting behavior, and identify changes to data, permissions, API contracts, or deployment requirements.

Keep the description understandable without an issue tracker. Include screenshots only when they help assess a visual change, and use synthetic records. Mark incomplete work as draft so reviewers can distinguish an early discussion from a request to merge. List any follow-up work explicitly rather than leaving unexplained TODOs in the implementation.

## Review code and address feedback

At least one engineer other than the author must approve each PR. The reviewer checks correctness, failure handling, test evidence, readability, and the effect on existing clients. Review comments should explain a concrete concern and distinguish required corrections from optional wording preferences.

Every migration needs a second engineer's review. A database reviewer must additionally approve migrations that drop or rename columns or are expected to run longer than one minute. The same person may satisfy the general reviewer requirement and a specialist requirement when qualified, but the author cannot approve their own change. API changes require the client-owner review described in [APIs](apis.md).

Authors respond to each blocking comment with a correction or an explanation supported by evidence. New code pushed after approval requires review of the changed portion and renewed approval. Resolve a discussion after the concern is addressed, and ask the reviewer when disagreement remains rather than silently closing it.

## Keep the branch current and merge

Update the branch using the repository's documented merge or rebase convention. Do not rebase a shared branch without coordinating with its collaborators. If an agreed rebase requires updating a remote feature branch, use `git push --force-with-lease` rather than an unconditional force push, and investigate any rejected update before retrying.

Before merging, confirm required approvals, resolved blocking discussions, and successful [continuous integration](testing-and-ci.md) for the current head commit SHA. Older pipeline results do not validate newer commits. Protected-branch rules prevent direct pushes to `main`; an urgent fix still follows review and CI requirements.

The author or designated maintainer merges the approved PR using the repository's configured merge method. Delete the feature branch only after confirming its changes are merged and no collaborator still needs it. Merging makes a change eligible for the [release process](deployment-and-releases.md); it does not prove the change is deployed.

## Knowledge check

How do PR and MR relate? Which approvals does a destructive migration require? Why must the successful CI result match the current head commit SHA?
