# Kubernetes Community

Welcome to the Kubernetes community!

This is the starting point for becoming a contributor - improving docs, improving code, giving talks etc.

## Communicating

The [communication](communication.md) page lists communication channels like chat,
issues, mailing lists, conferences, etc.

For more specific topics, try a SIG.

## SIGs

Kubernetes is a set of projects, each shepherded by a special interest group (SIG).

A first step to contributing is to pick from the [list of kubernetes SIGs](sig-list.md).

A SIG can have its own policy for contribution,
described in a `README` or `CONTRIBUTING` file in the SIG
folder in this repo (e.g. [sig-cli/CONTRIBUTING](sig-cli/CONTRIBUTING.md)),
and its own mailing list, slack channel, etc.

If you want to edit details about a SIG (e.g. its weekly meeting time or its leads),
please follow [these instructions](./generator) that detail how our docs are auto-generated.

## How Can I Help?

Documentation (like the text you are reading now) can
always use improvement!

There's a [semi-curated list of issues][help wanted]
that should not need deep knowledge of the system.

To dig deeper, read a design doc, e.g. [architecture].

[Pick a SIG](sig-list.md), peruse its associated [cmd] directory,
find a `main()` and read code until you find something you want to fix.

There's always code that can be clarified and variables
or functions that can be renamed or commented.

There's always a need for more test coverage.

## Learn to Build

Links in [contributors/devel/README.md](contributors/devel/README.md)
lead to many relevant topics, including
 * [Developer's Guide] - how to start a build/test cycle
 * [Collaboration Guide] - how to work together
 * [Expectations] - what the community expects
 * [Pull Request Process] - how to prepare a pull request

## Your First Contribution

We recommend that you work on an existing issue before attempting
to [develop a new feature].

Start by finding an existing issue with the [help wanted] label;
these issues we've deemed are well suited for new contributors.
Alternatively, if there is a specific area you are interested in,
ask a [SIG lead](sig-list.md) for suggestions), and respond on the
issue thread expressing interest in working on it.

This helps other people know that the issue is active, and
hopefully prevents duplicated efforts.

Before submitting a pull request, sign the [CLA].

If you want to work on a new idea of relatively small scope:

  1. Submit an issue describing your proposed change to the repo in question.
  1. The repo owners will respond to your issue promptly.
  1. If your proposed change is accepted,
     sign the [CLA],
     and start work in your fork.
  1. Submit a [pull request] containing a tested change.


[architecture]: /contributors/design-proposals/architecture/architecture.md
[cmd]: https://git.k8s.io/kubernetes/cmd
[CLA]: CLA.md
[Collaboration Guide]: contributors/devel/collab.md
[Developer's Guide]: contributors/devel/development.md
[develop a new feature]: https://github.com/kubernetes/features
[expectations]: contributors/guide/community-expectations.md
[help wanted]: https://go.k8s.io/help-wanted
[pull request]: contributors/guide/pull-requests.md

[![Analytics](https://kubernetes-site.appspot.com/UA-36037335-10/GitHub/CONTRIBUTING.md?pixel)]()
