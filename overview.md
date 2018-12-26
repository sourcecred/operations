# SourceCred

SourceCred is anchored by a simple goal: we want open-source contributors to
earn a living, and a share in the value created on top of their contributions.
At first, we focused on the obvious problem: where will the money come from? We
were inspired by the ability of cryptocurrencies to fund open-source projects,
and started [SourceGrain], with the goal of letting every open-source project
issue its own token.

However, as this idea evolved, we ran into a big problem: we don't know who
deserves credit in an open-source project, and thus we don't know how to
distribute the rewards. The obvious approaches, like counting commits or lines
of code, would be far too easy to game—and would in any case miss out on vital
work like design or issue triaging, not to mention that it would miss out on the
underlying quality of the commits or code.

This inability to quantify contributions accurately affects every method for
funding open-source. Projects need a fair system for deciding how to distribute
rewards regardless of whether they come through sponsorships, donations,
[cryptocurrency airdrops], or through any [other means]. SourceCred is designed
to do just that and we hope it will be used downstream by many to measure the
value derived from and thereafter fund open-source contributors' work.

[SourceGrain]: https://github.com/sourcegrain/mission/blob/master/README.md
[cryptocurrency airdrops]: https://en.wikipedia.org/wiki/Airdrop_(cryptocurrency)
[other means]: https://github.com/nayafia/lemonade-stand

## Overview

SourceCred assigns a score, called 'cred', to users and contributions in a
project. It does this by generating a 'contribution graph', for the project,
then running [PageRank] on it. The contribution graph can contain any kind of
contribution, and the relationships between them. For example, a GitHub
comment, StackOverflow answer, and npm package could all be contributions, and
'referenced another comment', or 'answered this question', or 'dependent on
that package' would be examples of relationships. The PageRank algorithm
ensures that every contribution gets cred based on its relationships to other
contributions, and in proportion to how valuable those other contributions were.

[PageRank]: https://en.wikipedia.org/wiki/PageRank

To get a feel for how this works, try exploring [SourceCred's own cred]. The
initial view will show you how much cred each user has; clicking the '+' next
to a person's lets you explore how that cred came from all the contributions
they've worked on. You can keep clicking '+' to dive down to the level of an
individual pull request or commit. Also, try using the dropdown slider to
filter by types of contributions; for example, you can use it to find all
of the GitHub issues in the repository, ranked by cred.

[SourceCred's own cred]: https://sourcecred.io/prototypes/sourcecred/sourcecred/

As you explore the UI, you'll also notice a 'Show weight configuration' button.
The weights allow you to assign levels of importance to different types of
contributions and relationships. For example: by default, pull requests have
more weight than comments, and being referenced yields more cred than
referencing something.

We also plan to add 'heuristics', which allow custom logic for evaluating
contributions. For example, a heuristic might increase the weight of pull
requests that add tests and documentation, but decrease the weight of comments
that just say "me too".

## Current Status

SourceCred is currently in an early beta stage, with much of the core
infrastructure in place, and a functioning prototype. Anecdotally, SourceCred
seems to do a good job of assigning cred to the major contributors of GitHub
projects; we've shown contributors' cred totals to the maintainers of several
projects, and the feedback has been quite positive. However, SourceCred doesn't
yet do a great job of assigning cred to individual pull requests, issues, or
commits. There isn't yet much data distinguishing pulls or commits from each
other, so whichever ones get more discussion often get to have the highest scores.

The next big frontier for improving cred quality is adding source-code
analysis. We'll do this by adding files and functions into the contribution
graph. We also plan to add "time-based cred", to answer questions like "who
made the most valuable contributions this month?"

## Getting Involved

We'd love to have you as a part of the SourceCred community! You can run SourceCred
on your own projects by following the instructions [in our GitHub repository], and
please drop by [our Discord chat] and say hello!

[in our GitHub repository]: https://github.com/sourcecred/sourcecred
[our Discord chat]: https://discordapp.com/invite/tsBTgc9

## FAQs

### Why Use Contribution Graphs?

SourceCred bases everything around contribution graphs because they are such an
abstract and flexible data structure. We love that they can encode a huge scope
of possible contribution types, and possible relationships between
contributions. That will allow us to incorporate more and more kinds of
contributions, like messages on a mailing list, or giving talks, or organizing
community meetups, etc. In the future, we imagine SourceCred being used for
entirely non-code projects, e.g. it could be used as a credit attribution
system within a scientific collaboration.


### Why Use PageRank?

We like the PageRank algorithm because it does a good job of assigning scores
to a cred graph, and is already reasonably gaming-resistent. Just creating a
bunch of spam posts won't earn very much cred, because not many contributions
will be connected to the spam.

As our needs develop, we'll make a number of modifications to PageRank.
Already, the weighting system described above isn't part of the base algorithm.
We see more modications [on the horizon].

[on the horizon]: (https://github.com/sourcecred/notes/issues/1)

### Won't people game SourceCred?

It's inevitable that once SourceCred is active, people will start to change
behavior in response to the metric. Actually, we're hoping for that: we want
SourceCred to incentivize people to do those important tasks, like writing docs
and triaging issues, that projects struggle with today.

However, if SourceCred is implemented poorly, it will reward people who focus
on irrelevant or even harmful activities. For example, a user might spam the
issue tracker with meaningless posts, or add an empty code review to every pull
request.

Community moderation can go a long way to stopping this kind of outright gaming.
Project maintainers can act as moderators and remove spam posts, or directly
dock the attackers' cred. However, some "gaming" will be a lot more subtle. For
example, users might write useful posts in a deliberately controversial way,
so as to generate more replies and then earn more cred.

For these types of problems, there is no silver bullet. (If there were, then
[Goodhart's law] wouldn't be a law.) However, we think that a two-pronged approach
will be effective.

[Goodhart's law]: https://en.wikipedia.org/wiki/Goodhart%27s_law

First, since open-source communities are communities, they can
develop social norms around using SourceCred, and regulate their own behavior. SourceCred's
focus on making the results highly transparent will make it easier to spot when
people are gaming.

Second, since SourceCred is itself open-source, anyone can propose new heuristics to
mitigate gaming. For example, the community could develop a machine learning model
to distinguish between threads that are constructive and threads that are flame wars,
and then greatly reduce the weight on the flame wars or likewise generally adapt
SourceCred to their project's specific needs.

### Is SourceCred open-source?

Yes, entirely! SourceCred is dual-licensed under MIT and Apache 2.0.

### Who's supporting SourceCred?

SourceCred is being developed with funding and support from [Protocol Labs].

[Protocol Labs]: https://protocol.ai/

### What's the relationship between SourceCred and SourceGrain?

You can think of SourceCred as the "IPFS" to SourceGrain's "Filecoin".
SourceCred is building a protocol for credit attribution independent of
economic incentives, and SourceGrain will add an incentive layer on top
using SourceCred. They can nonetheless exist independently from one
another, for instance with SourceCred being used for other purposes,
or SourceGrain being used atop another credit attribution system.
