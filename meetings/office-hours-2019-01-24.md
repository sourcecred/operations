* Recording: [Link](https://www.youtube.com/watch?v=7YuKPBLQeSI)
* Attendees: @decentralion, @wchargin, @BrianLitwin, @wpank

#### Contents
* Discussion:  GraphQL architecture solutions  [0:00]
* Milestones + weekly progress reports [9:00]
* SourceCred/Research [11:26]
* Case Studies [14:10]
* How are we doing ranking our own pull requests at Sourcecred? [22:10]
* Using lines of code changed as signal for cred [24:18]
* Evaluating the energy required/difficulty of a contribution [26:15]
* Thoughts on negative cred [36:00]
* The scenario where a maintainer spends a lot of time on your pull request [37:15]
* Project-specific behavior and heuristics [39:08]
* Short-term versus long-term feedback loops [40:22]
* Helping Open Source communities [46:01]

#### Discussion:  GraphQL architecture solutions  [0:00]
* There's a lot of overhead involved in our current system of mirroring a GraphQL database
* There are some solutions out there for GraphQL architectures
* Translating GQL schemas to relational db schemeas gets tricky
* [Prisma]
* The uptshot is getting a lot of built-in functionality, reusing code, less code to maintain, simpler to work with (only worrying about objects vs relational db schema/queries)
* Our architecture is designed to download the entire db instead of specific segments, which is not the intent of most GQL services
* That assumption is not set in stone; we may want to stream data from GQL in the future
* Websockets + GitHub's webhooks could enable us to recieve updates and push them from the backend to the frontend  

#### Milestones + weekly progress reports [9:00]
* There is room to impose more structure/clarity in our project organization
* "Mission" doesn't reflect what's currently going on in our Mission repo. Mission refers to what values are driving the project/ what are the intrinsic motivations. Our Mission repo is more of a project management/logistics repo. IPFS/Ethereum have good project management repos to model.
* We could set agendas for topics/themes to bring up during Office Hours
* We could put Office Hours notes in a separate folder

#### SourceCred/Research [11:26]
* A Sourecred/Research repo would be cool. We could put case studies in that repo.
* Research topic: Can we extrapolate the design patterns of what make Open Source communities work well?
* Research topic: The credit attribution problem is an open question
* Could use the Research to more rigorously document the algorithm. A tradeoff is that by keeping design docs that relate directly to the code in the same repo where that code lives enables updating the code and the docs in the same commit.  

#### Case Studies [14:10]
* Can we spin up an IPFS case study? Run the Sourcecred algo on IPFS and poke people in a public forum.
* How to solicit the feedback of maintainers/ folks with the most knowledge about a project?
* Creating attributions for a repository: anybody could create attributions and make them public and we could incorporate them into the graph
* Idea: A chrome extension to allow maintainers to spotlight certain contributions
* Give people in the community the ability to propose new nodes in the graph
* There are different ways to add 'arbitrary' nodes to the graph. What's the best implementation?
* We would like to be able to ask who has implementation versus logistics cred (based on contributions to diff repositories)
* We would like to be able to build toy graphs to easily reason about what the semantics should be and the actual semantics of the Sourcecred algo. These would also promote understanding of the algo in general by making it easier to understand for others.
* Transparency in how Sourcecred arrives at it's conclusions is important for Sourcecred's credibility.  
* Sourcecred on Sourcecred should be our first case study

#### How are we doing ranking our own pull requests at Sourcecred? [22:10]
* Fine; uneven; room for improvement
* Single-comment reviews: they create a review entity in GitHub's ontology and are kind of a bug

#### Using lines of code changed as signal for cred [24:18]
* Gets noisy/messed up by node modules/libraries/auto-generated code
* Lotta competing factors.
* Is more code not usually more cred-worthy than less code?
* Hypothesis: there's a positive correlation between lines of code and the value of a contribution but it's a weak correlation
* There are difficult, valuable, high-effort contributions that are not reflected in the number of lines of code changes, eg tracking down difficult bugs that require changing 3 lines of code.
* Using lines of code as a heuristic can be a bad incentive, because the writing the same commit in less code is usually better. But also, context is important: more test code or documentation is usually good.

#### Evaluating the energy required/difficulty of a contribution [26:15]
* Question: How can we assess the difficulty of a pull request?
* We don't currently have a principled mathemetical system for combining many heuristics on nodes. Should add documentation about why we've had trouble with this.
* Idea: Having the maintainer assessing the difficulty of a pull request, possibly by making a Chrome plugin where maintainers can rate Pull Requests on 1-3 scale from trivial to very hard.  
* Labels are an explicit way to assign cred and it would be nice to include them in the graph.
* Idea: let people assign weights to labels. (not trivial how to implement this => but we can start by getting the label data from Github)
* A consideration is how to implement label-cred so that empty issues aren't accumulating cred just because they have a label  

#### Thoughts on negative cred [36:00]
* Can't really express negative cred; but can semi-execute it through the weight metric by turning down the weight dial.

#### The scenario where a maintainer spends a lot of time on your pull request [37:15]
* In one sense, better PRs would require less time and energy from the maintainer, because maintainers are often time-constrained
* On the other hand, the maintainer's interaction is good signal that a PR is valuable and relatively difficult
* Sourcecred currently relies on the latter signal by accumulating cred where maintainers make more comments and reviews on PRs
* Is there a metric to distinguish between cases where maintainers are spending valuable time with you working your PR versus wasting their time eg reminding you to fix lint errors, etc?

#### Project-specific behavior and heuristics [39:08]
* Projects will all have unique behaviors and lots of variation between them, so it's important to keep our tools flexible
* Making it easy for users to write custom heuristics will be valuable for this reason

#### Short-term versus long-term feedback loops [40:22]
* Incentivizing positive behavior in OS communities is a really exciting long-term ambition
* We can do that by providing good tools that encourage people to change their behaviors
* How can we give people signal on the quality of their contributions so that they can adapt their behaviors to be more valuable? How can we improve people's decision making process on how they spend their time/energy?
* How has the algorithm incentivized us to change our behavior? Perhaps to be more conscious of emojies and using references.
* Building habits through short-term feedback loops could be very valuable, e.g. communicating the cred one has achieved immediately. Image: coins exploding after a particularly valuable pull request.  
* On the other hand, incentivizing behavior that benefits the project over the long-term, through long-term feedback loops, would also be great. We could incentivize people to, for instance, write code that's easier to maintain and more robust.
* Grain can also be a tool to use alongside cred to create feedback loops.

#### Helping Open Source communities [46:01]
* How could we help Flow?
* How does Cred work over time when the weights are changed? Eg one week you configure Sourcecred to prioritize Tests, and then you ajust those dials the next week to prioritize Documentation. Essentially, Grain is a better tool for that dynamic than Cred.
* How could you gather metrics on the state of a project using SourceCred? And how could you show that using SoucreCred can improve those metrics?  
* Open Collective would like to send out an auto-generated digest of project activity
* Can we create trial-runs for SourceCred? Small projects in which we distribute money based on the sourcecred algo. Or putting bounties on issues and see how people behave.
* Are there any legal boundaries to paying people bitcoin ie magic internet money?

[Prisma]: https://github.com/prisma
[0:00]: https://www.youtube.com/watch?v=7YuKPBLQeSI&#t=0m00s
[9:00]: https://www.youtube.com/watch?v=7YuKPBLQeSI&#t=9m00s
[11:26]: https://www.youtube.com/watch?v=7YuKPBLQeSI&#t=11m26s
[14:10]: https://www.youtube.com/watch?v=7YuKPBLQeSI&#t=14m10s
[22:10]: https://www.youtube.com/watch?v=7YuKPBLQeSI&#t=22m10s
[24:18]: https://www.youtube.com/watch?v=7YuKPBLQeSI&#t=24m18s
[26:15]: https://www.youtube.com/watch?v=7YuKPBLQeSI&#t=26m15s
[36:00]: https://www.youtube.com/watch?v=7YuKPBLQeSI&#t=36m00s
[37:15]: https://www.youtube.com/watch?v=7YuKPBLQeSI&#t=37m15s
[39:08]: https://www.youtube.com/watch?v=7YuKPBLQeSI&#t=39m08s
[40:22]: https://www.youtube.com/watch?v=7YuKPBLQeSI&#t=40m22s
[46:01]: https://www.youtube.com/watch?v=7YuKPBLQeSI&#t=46m01s
