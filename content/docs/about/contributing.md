+++
title =  "Contributing to Kubeflow"
description = "How to start contributing to Kubeflow"
weight = 3
aliases = ["/docs/contributing/"]
+++

Welcome to the Kubeflow project!

## Getting started as a Kubeflow contributor

This document is the single source of truth for how to contribute to the code base.
We'd love to accept your patches and contributions to this project. There are
just a few small guidelines you need to follow.

### Sign the CLA

Contributions to this project must be accompanied by a Contributor License Agreement (CLA). 
You (or your employer) retain the copyright to your contribution.
This gives us permission to use and redistribute your contributions as
part of the project. Head over to <https://cla.developers.google.com/> to see
your current agreements on file or to sign a new one.

You generally only need to submit a CLA once, so if you've already submitted one
(even if it was for a different project), you probably don't need to do it
again.

### Follow the code of conduct

Please make sure to read and observe our [Code of Conduct](https://github.com/kubeflow/community/blob/master/CODE_OF_CONDUCT.md).

### Consider participating in Kubeflow user research

Maggie Lynn, a user experience researcher, is conducting user studies to inform future developments for Kubeflow. These typically involve a one hour study session conducted online with a thank you gift for providing your feedback. As a member of the Kubeflow community, your feedback and expertise are extremely valuable to us, so if you have time in the next month, please consider participating. To gather your interest, availability, and some basic information about you, please fill out this form where you’ll find out more details about this research opportunity: [https://goo.gl/forms/sv5sRo3UfsgeUEjK2](https://goo.gl/forms/sv5sRo3UfsgeUEjK2)

## Joining the community

Follow these instructions if you want to

* Become a member of the Kubeflow GitHub org (see below)
* Become part of the Kubeflow build cop or release teams
* Be recognized as an individual or organization contributing to Kubeflow

### Joining the Kubeflow GitHub Org

Before asking to join the community, we ask that you first make a small number of contributions
to demonstrate your intent to continue contributing to Kubeflow. 

There are are a number of ways to contribute to Kubeflow

  * Submit PRs
  * File issues reporting bugs or providing feedback
  * Answer questions on Slack or GitHub issues

You can use this [table](http://devstats.kubeflow.org/d/9/developers-summary) to see how many contributions
you've made

  * **Note**: This only counts GitHub related ways of contributing

When you are ready to join

  * Send a PR adding yourself as a member in [org.yaml](https://github.com/kubeflow/internal-acls/blob/master/github-orgs/kubeflow/org.yaml#L19)  
  * After the PR is merged an admin will send you an invitation
    * This is a manual process that's generally run a couple times a week
    * If a week passes without receiving an invitation reach out on [kubeflow#community](https://kubeflow.slack.com/messages/C8Q0QJYNB/convo/CABQ2BWHW-1544147308.002500/)

### Companies/organizations

If you would like your company or organization to be acknowledged for contributing to
Kubeflow or participating in the community (being a user counts) please send a PR
adding the relevant info to
[member_organizations.yaml](https://github.com/kubeflow/community/blob/master/member_organizations.yaml).

If you want your employee's GitHub contributions to be attributed to your company please ask them to set
the company field in their GitHub profile.

### Community discussions

There are many ways to contribute! Join one of our communication channels, 
attend a community meeting, get to know the community. Read the details in
our [community guide](/docs/about/community).

## Your first contribution

### Find something to work on

Help is always welcome! For example, documentation (like the text you are reading
now) can always use improvement. There's always code that can be clarified and
variables or functions that can be renamed or commented. There's always a need
for more test coverage. You get the idea - if you ever see something you think
should be fixed, you should own it. Here is how you get started.

### Starter issues

To find Kubeflow issues that make good entry points, look at the following tags:

* [`good first issue`](https://github.com/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22+org%3Akubeflow)
* [`help wanted`](https://github.com/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22+org%3Akubeflow)

## Owners files and PR workflow

Our PR workflow is nearly identical to Kubernetes'. Most of these instructions are a
modified version of Kubernetes' [contributors](https://github.com/kubernetes/community/blob/master/contributors/guide/README.md)
and [owners](https://github.com/kubernetes/community/blob/master/contributors/guide/owners.md#code-review-using-owners-files)
guides.

### Overview of OWNERS files

OWNERS files are used to designate responsibility over different parts of the Kubeflow codebase.
Today, we use them to assign the **reviewer** and **approver** roles used in our two-phase code
review process. Our OWNERS files were inspired by [Chromium OWNERS
files](https://chromium.googlesource.com/chromium/src/+/master/docs/code_reviews.md), which in turn
inspired [GitHub's CODEOWNERS files](https://help.github.com/articles/about-codeowners/).

The velocity of a project that uses code review is limited by the number of people capable of
reviewing code. The quality of a person's code review is limited by their familiarity with the code
under review. Our goal is to address both of these concerns through the prudent use and maintenance
of OWNERS files

### OWNERS  <a name="owners-1"></a>

Each directory that contains a unit of independent code or content may also contain an OWNERS file.
This file applies to everything within the directory, including the OWNERS file itself, sibling
files, and child directories.

OWNERS files are in YAML format and support the following keys:

- `approvers`: a list of GitHub usernames or aliases that can `/approve` a PR
- `labels`: a list of GitHub labels to automatically apply to a PR
- `options`: a map of options for how to interpret this OWNERS file, currently only one:
  - `no_parent_owners`: defaults to `false` if not present; if `true`, exclude parent OWNERS files.
    Allows the use case where `a/deep/nested/OWNERS` file prevents `a/OWNERS` file from having any
    effect on `a/deep/nested/bit/of/code`
- `reviewers`: a list of GitHub usernames or aliases that are good candidates to `/lgtm` a PR

All users are expected to be assignable. In GitHub terms, this means they are either collaborators
of the repo, or members of the organization to which the repo belongs.

A typical OWNERS file looks like:

```
approvers:
  - alice
  - bob     # this is a comment
reviewers:
  - alice
  - carol   # this is another comment
  - sig-foo # this is an alias
```

#### OWNERS_ALIASES

Each repo may contain at its root an OWNERS_ALIAS file.

OWNERS_ALIAS files are in YAML format and support the following keys:

- `aliases`: a mapping of alias name to a list of GitHub usernames

We use aliases for groups instead of GitHub Teams, because changes to GitHub Teams are not
publicly auditable.

A sample OWNERS_ALIASES file looks like:

```
aliases:
  sig-foo:
    - david
    - erin
  sig-bar:
    - bob
    - frank
```

GitHub usernames and aliases listed in OWNERS files are case-insensitive.

### The code review process

- The **author** submits a PR
- Phase 0: Automation suggests **reviewers** and **approvers** for the PR
  - Determine the set of OWNERS files nearest to the code being changed
  - Choose at least two suggested **reviewers**, trying to find a unique reviewer for every leaf
    OWNERS file, and request their reviews on the PR
  - Choose suggested **approvers**, one from each OWNERS file, and list them in a comment on the PR
- Phase 1: Humans review the PR
  - **Reviewers** look for general code quality, correctness, sane software engineering, style, etc.
  - Anyone in the organization can act as a **reviewer** with the exception of the individual who
    opened the PR
  - If the code changes look good to them, a **reviewer** types `/lgtm` in a PR comment or review;
    if they change their mind, they `/lgtm cancel`
  - Once a **reviewer** has `/lgtm`'ed, [prow](https://prow.k8s.io)
    ([@k8s-ci-robot](https://github.com/k8s-ci-robot/)) applies an `lgtm` label to the PR
- Phase 2: Humans approve the PR
  - The PR **author** `/assign`'s all suggested **approvers** to the PR, and optionally notifies
    them (eg: "pinging @foo for approval")
  - Only people listed in the relevant OWNERS files, either directly or through an alias, can act
    as **approvers**, including the individual who opened the PR
  - **Approvers** look for holistic acceptance criteria, including dependencies with other features,
    forwards/backwards compatibility, API and flag definitions, etc
  - If the code changes look good to them, an **approver** types `/approve` in a PR comment or
    review; if they change their mind, they `/approve cancel`
  - [prow](https://prow.k8s.io) ([@k8s-ci-robot](https://github.com/k8s-ci-robot/)) updates its
    comment in the PR to indicate which **approvers** still need to approve
  - Once all **approvers** (one from each of the previously identified OWNERS files) have approved,
    [prow](https://prow.k8s.io) ([@k8s-ci-robot](https://github.com/k8s-ci-robot/)) applies an
    `approved` label
- Phase 3: Automation merges the PR:

  - If all of the following are true:

      - All required labels are present (eg: `lgtm`, `approved`)
      - Any blocking labels are missing (eg: there is no `do-not-merge/hold`, `needs-rebase`)

  - And if any of the following are true:

      - there are no presubmit prow jobs configured for this repo
      - there are presubmit prow jobs configured for this repo, and they all pass after automatically
        being re-run one last time

  - Then the PR will automatically be merged

### Quirks of the process

There are a number of behaviors we've observed that while _possible_ are discouraged, as they go
against the intent of this review process.  Some of these could be prevented in the future, but this
is the state of today.

- An **approver**'s `/lgtm` is simultaneously interpreted as an `/approve`
  - While a convenient shortcut for some, it can be surprising that the same command is interpreted
    in one of two ways depending on who the commenter is
  - Instead, explicitly write out `/lgtm` and `/approve` to help observers, or save the `/lgtm` for
    a **reviewer**
  - This goes against the idea of having at least two sets of eyes on a PR, and may be a sign that
    there are too few **reviewers** (who aren't also **approver**)
- Technically, anyone who is a member of the Kubeflow GitHub organization can drive-by `/lgtm` a
  PR
  - Drive-by reviews from non-members are encouraged as a way of demonstrating experience and
    intent to become a collaborator or reviewer
  - Drive-by `/lgtm`'s from members may be a sign that our OWNERS files are too small, or that the
    existing **reviewers** are too unresponsive
  - This goes against the idea of specifying **reviewers** in the first place, to ensure that
    **author** is getting actionable feedback from people knowledgeable with the code
- **Reviewers**, and **approvers** are unresponsive
  - This causes a lot of frustration for **authors** who often have little visibility into why their
    PR is being ignored
  - Many **reviewers** and **approvers** are so overloaded by GitHub notifications that @mention'ing
    is unlikely to get a quick response
  - If an **author** `/assign`'s a PR, **reviewers** and **approvers** will be made aware of it on
    their [PR dashboard](https://k8s-gubernator.appspot.com/pr)
  - An **author** can work around this by manually reading the relevant OWNERS files,
    `/unassign`'ing unresponsive individuals, and `/assign`'ing others
  - This is a sign that our OWNERS files are stale; pruning the **reviewers** and **approvers** lists
    would help with this
- **Authors** are unresponsive
  - This costs a tremendous amount of attention as context for an individual PR is lost over time
  - This hurts the project in general as its general noise level increases over time
  - Instead, close PR's that are untouched after too long (we currently have a bot do this after 90
    days)

## Automation using OWNERS files

### [`prow`](https://git.k8s.io/test-infra/prow)

Prow receives events from GitHub, and reacts to them. It is effectively stateless. The following
pieces of prow are used to implement the code review process above.

- [cmd: tide](https://git.k8s.io/test-infra/prow/cmd/tide)
  - per-repo configuration:
    - `labels`: list of labels required to be present for merge (eg: `lgtm`)
    - `missingLabels`: list of labels required to be missing for merge (eg: `do-not-merge/hold`)
    - `reviewApprovedRequired`: defaults to `false`; when true, require that there must be at least
      one [approved pull request review](https://help.github.com/articles/about-pull-request-reviews/)
      present for merge
    - `merge_method`: defaults to `merge`; when `squash` or `rebase`, use that merge method instead
      when clicking a PR's merge button
  - merges PR's once they meet the appropriate criteria as configured above
  - if there are any presubmit prow jobs for the repo the PR is against, they will be re-run one
    final time just prior to merge
- [plugin: assign](https://git.k8s.io/test-infra/prow/plugins/assign)
  - assigns GitHub users in response to `/assign` comments on a PR
  - unassigns GitHub users in response to `/unassign` comments on a PR
- [plugin: approve](https://git.k8s.io/test-infra/prow/plugins/assign)
  - per-repo configuration:
    - `issue_required`: defaults to `false`; when `true`, require that the PR description link to
      an issue, or that at least one **approver** issues a `/approve no-isse`
    - `implicit_self_approve`: defaults to `false`; when `true`, if the PR author is in relevant
      OWNERS files, act as if they have implicitly `/approve`'d
  - adds the  `approved` label once an **approver** for each of the required
    OWNERS files has `/approve`'d
  - comments as required OWNERS files are satisfied
  - removes outdated approval status comments
- [plugin: blunderbuss](https://git.k8s.io/test-infra/prow/plugins/assign)
  - determines **reviewers** and requests their reviews on PR's
- [plugin: lgtm](https://git.k8s.io/test-infra/prow/plugins/lgtm)
  - adds the `lgtm` label when a **reviewer** comments `/lgtm` on a PR
  - the **PR author** may not `/lgtm` their own PR
- [pkg: k8s.io/test-infra/prow/repoowners](https://git.k8s.io/test-infra/prow/repoowners/repoowners.go)
  - parses OWNERS and OWNERS_ALIAS files
  - if the `no_parent_owners` option is encountered, parent owners are excluded from having
    any influence over files adjacent to or underneath of the current OWNERS file

## Maintaining OWNERS files

OWNERS files should be regularly maintained.

We encourage people to self-nominate or self-remove from OWNERS files via PR's. Ideally in the future
we could use metrics-driven automation to assist in this process.

We should strive to:

- grow the number of OWNERS files
- add new people to OWNERS files
- ensure OWNERS files only contain org members and repo collaborators
- ensure OWNERS files only contain people are actively contributing to or reviewing the code they own
- remove inactive people from OWNERS files

Bad examples of OWNERS usage:

- directories that lack OWNERS files, resulting in too many hitting root OWNERS
- OWNERS files that have a single person as both approver and reviewer
- OWNERS files that haven't been touched in over 6 months
- OWNERS files that have non-collaborators present

Good examples of OWNERS usage:

- there are more `reviewers` than `approvers`
- the `approvers` are not in the `reviewers` section
- OWNERS files that are regularly updated (at least once per release)
