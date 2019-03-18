#### Research Collaboration with [Block Science] 🚀 [0:00]

- First step is to set up a research environment to do exploratory data analysis
- A priority is to maintain alignment between the research layer and the implementation layer
- Example: A hypothesis is that one could approximate the SourcreCred algorithm pretty well by assigning a fixed score to every type of node that you author (that's not what we want, but may be the case). A synthetic graph generator could tell us whether the algorithm approximates that model under certain conditions.
- Another experiment may be to simulate attack graphs, e.g. a user that makes one comment on every issue.
- **NetworkX** is going to provide the ability to write _synthetic graph generator models_. These models are what will allow us to model human behavior. With NetworkX we can add nodes and edges and simulate static and dynamic conditions. Static conditions would be creating a graph and seeing how it scores; dynamic conditions would be see how the network state changes in response to new activity, e.g. how users respond to different feedback conditions.

#### Code Management in Research Repo [8:02]

- Collaborating on Python Notebooks: Sometimes we will collaborate on the same notebook to publish an experiment, but generally people will keep their own notebooks on their individual branches, and collaborate by grabbing code from each other. Research and experimentation will happen on individual branches.
- We want to setup an infrastructure (Infra) subdirectory, for tested, production-quality code that is heavily depended on, e.g.: validation tests, graph generators, a canonical pagerank implementation, etc.
- The canonical pagerank implementation is high priority so that we can use it as a benchmark against which to compare alternative methods.
- **What are the validation metrics?** => we will start with some simple things like "how does score correlate to degree?" and work our way up to things that are more meaningful. But because this project has a strong qualitative component, we'll be merging our technical proficiency with our intuition iteratively => The metrics we find meaningful may change over time. _Right now we are trying out metrics and deciding whether those metrics are good encodings of the things we care about_.
- Graph generator models will help use create small test cases (e.g. graphs with certain properties) that we can use for validation, visualization, documentation, and to create repeatable scientific experiments.
- There's a distinction between the test cases themselves and what we want to happen in those test cases.

#### Logos [15:47]

- [Logo Thread]
- SourceCred virtues and themes:
  - Growth (graph-sense and in nature)
  - Sunlight (shining a light on contributors)

#### Odyssey Hackathon [27:32]

- Our track will be Nature 2.0. Themes of Nature 2.0 are building systems that are more fair, biomimetic, and open.
- Some thoughts/ideas are:
  - Take a hack at implementing a multi-class variation of the pagerank algorithm
  - Prioritize a visual component to represent the math/algoirthms we are working on
  - The SourceCred UI for non-coders: Allow people to see how discrete items of work create a cred graph. I.e. manual mode SourceCred. See things visually and how they are interdependent.
  - Re-use the SourceCred algorithm and underlying philosophy in a non-programming context (perhaps a mobile experience?)
  - Perhaps bring someone that has shipped code at a hackathon before?

#### Architecture of Production Stack and Pagerank Algo [41:05]

- See video; Z and William discuss technical details of pagerank implementation
- William mentioned that he had written down some of this thoughts on this subject in [#534]

[block science]: https://github.com/blockscience
[logo thread]: https://github.com/sourcecred/pm/issues/5
[#534]: https://github.com/sourcecred/sourcecred/issues/534
[0:00]: https://www.youtube.com/watch?v=_FF-_Ej62Y0#&t=0m00s
[8:02]: https://www.youtube.com/watch?v=_FF-_Ej62Y0#&t=8m02s
[15:47]: https://www.youtube.com/watch?v=_FF-_Ej62Y0#&t=15m47s
[27:32]: https://www.youtube.com/watch?v=_FF-_Ej62Y0#&t=27m32s
[41:05]: https://www.youtube.com/watch?v=_FF-_Ej62Y0#&t=41m05s
