* Recording: [Link](https://www.youtube.com/watch?v=3NgANZNdSlo)
* Attendees: @decentralion, @wchargin, @anthrocypher, @BrianLitwin, @lpatmo, @sternhenri, @dignifiedquire

#### Contents

* **Intro**
* What's been going on with SourceCred lately? [0:00](https://www.youtube.com/watch?v=3NgANZNdSlo#t=0m00s)
* How do we use GraphQL? [2:03](https://www.youtube.com/watch?v=3NgANZNdSlo#t=2m03s)
* Idea: Embedding SourceCred output in READMEs [7:00](https://www.youtube.com/watch?v=3NgANZNdSlo#t=7m00s)
* Discussion: Time-based Cred [7:50](https://www.youtube.com/watch?v=3NgANZNdSlo#t=7m50s)
* **Community Building**
* How can we leverage Issue Labels to be more welcoming and accessible to new contributors? [10:23](https://www.youtube.com/watch?v=3NgANZNdSlo#t=10m23s)
* How can we be proactive about onboarding new contributors? [24:08](https://www.youtube.com/watch?v=3NgANZNdSlo#t=24m08s)
*  Logistics [37:00](https://www.youtube.com/watch?v=3NgANZNdSlo#t=37m00s)
* **Technical Deep-Dive**
* Plugins
* Why is SourceCred built around a plugin architecture? [39:30](https://www.youtube.com/watch?v=3NgANZNdSlo#t=39m30s)
* The Analysis Adapter [41:27](https://www.youtube.com/watch?v=3NgANZNdSlo#t=41m27s)
* The App Adapter [45:39](https://www.youtube.com/watch?v=3NgANZNdSlo#t=45m39s)
* Static vs dynamic adapters [49:20](https://www.youtube.com/watch?v=3NgANZNdSlo#t=49m20s)
* Why do we have separate Explorer Adapters and Analysis Adapters? [52:14](https://www.youtube.com/watch?v=3NgANZNdSlo#t=52m14s)
* Unit Testing with Snapshots [55:23](https://www.youtube.com/watch?v=3NgANZNdSlo#t=55m23s)
* Serialization/Deserialization [56:09](https://www.youtube.com/watch?v=3NgANZNdSlo#t=56m09s)

#### What's been going on with SourceCred lately? [0:00](https://www.youtube.com/watch?v=3NgANZNdSlo#t=0m00s)

* We recently published a 2019 [Plan](https://github.com/sourcecred/mission/blob/master/okrs_2019.md) in our Mission repository at [SourceCred/Mission](https://github.com/sourcecred/mission)
* [SourceCred/Mission](https://github.com/sourcecred/mission) will contain logistical or high-level planning for the project
* [SourceCred/SourceCred](https://github.com/sourcecred/sourcecred) will contain the codebase for the project
* The most exciting recent development 🎉 is that we're starting to see new contributors/contributions to the project such as [@anthrocypher](https://github.com/anthrocypher) at [#1044](https://github.com/sourcecred/sourcecred/pull/1044), [@brianlitwin](https://github.com/brianlitwin) at [#1032](https://github.com/sourcecred/sourcecred/pull/1032) and [@expravit](https://github.com/expravit) at [#1031](https://github.com/sourcecred/sourcecred/pull/1031).
* A big 2019 Q1 priority will be community building for the project. SourceCred is really a **social technology** in the sense that we're trying to come to a social consensus about who deserves cred and which things we value in a project. Building a community of people who are excited to try SourceCred is vital to the success of the project.
* Areas of focus to promote community-building: documentation, videos and events such as this Office Hours.

####  How do we use GitHub's GraphQl service? [2:03](https://www.youtube.com/watch?v=3NgANZNdSlo#t=2m03s)

* The first hurdle is that GitHub's GraphQL service is paginated, so you can only request 100 nodes at a time, eg 100 Issues or Comments at a time. So we request nodes in batches one after the other if we want more than 100.
* We also want to request multiple kinds of data in one query because there is a recursive structure to the data: A Repository will have a certain number of Pull Requests, each of which will have a certain number of Pull Request Reviews, etc.
* This isn't conceptually difficult, but getting the details right and tracking the state of these requests isn't trivial.
* The GraphQL logic lives in [src/graphql](https://github.com/sourcecred/sourcecred/tree/master/src/graphql)
* The [Schema](https://github.com/sourcecred/sourcecred/blob/master/src/graphql/schema.js) module is where we define what the remote GraphQL database that we're interested in looks like. Basically, we copy over parts of the GitHub database schema, but only the parts we care about.
* The [Mirror](https://github.com/sourcecred/sourcecred/blob/master/src/graphql/mirror.js) module maintains a local mirror of the subset of the remote database that we care about. The API for Mirorr is that we give it a connection to GitHub and we give it the GitHub Schema that we care about and then we can query it for things (such as a Repository) and it will go a fetch what we want, transitively fetch all the related objects (eg. People, Pull Requsts, Issues), and return a nicely formatted JavaScript object.
* The [Queries](https://github.com/sourcecred/sourcecred/blob/master/src/graphql/queries.js) module is where the queries are built.
* There are some design constraints we wanted to maintain, such as making it easy to inspect what caused the problem if something goes wrong, and being able to pause the download and resume it later: large repositories can take upwards of half an hour to download, and something could easily happen to disrupt that download.

####  Idea: Embedding SourceCred output in READMEs [7:00](https://www.youtube.com/watch?v=3NgANZNdSlo#t=7m00s)
* The idea would be to make is easy for projects to embed SourceCred output into their README; eg, if we had a script that loaded the SourceCred data and produced an SVG that had the scored totals in a nice graphic. We could put it on the top of our README at SourceCred, and write a script that updates it every week. It would be a cool artifact that people would see and want for their own project - and we would include a guide on how to generate it for your own project.

#### Time-based Cred [7:50](https://www.youtube.com/watch?v=3NgANZNdSlo#t=7m50s)
* A very impactful initiative will be **Time-Based Cred**, so that we can show the Cred for more recent, smaller time periods (eg. the last month, week, etc). Computing Cred over smaller time frames will provide opportunity for more mobility among contributors on their Cred lists: it will be exciting/inspiring to see your name rise on the most recent Cred list from the past month, for example. We could also include a section for contributors who are new to the project or who are picking up more valuable contributions, ie orient the Cred output metrics to **showcase new and up-and-coming contributors**.
* Big picture ambition for SourceCred as a social technology: **make it engaging to communities and something in which people find meaning**. Important orientation to take.
* Documentation: we should have documentation for exactly what the semantics of the algorithm are right now, so that it serves as a touchstone for discussing what the semantics of adding changes like timestamping should be.

####  How can we leverage Issue Labels to be more welcoming and accessible to new contributors? [10:20](https://www.youtube.com/watch?v=3NgANZNdSlo#t=10m20s)

* We could include labels that are more explicit about the difficulty of an Issue: "Contributions Welcome" currently includes Issues of varying degrees of difficulty, and it would help newcomers more easily find Issues that match their skill level and familiarity with the project if we were more explicit about the difficulty of Issues.
* A good starting point would be to use a label which communicates that the Issue would be a good first contribution to the project, eg "Good for Beginners" or "Good First Issue".
* Difficulty labels would also be great signal to SourceCred for how much cred to assign contributions. Eg. closing an Issue labeled "Hard" should award more Cred than an Issue labeled "Easy".
* This invites the problem of "Gaming", as whoever is in charge of assigning the labels has a lot of control over the flow of Cred. But part of our job in designing SourceCred is to build **transparency** and **visibility** into how Cred is awarded so that the Community is aware of and can correct potentially misaligned incentives.
* Another long-term ambition is to provide more granular heuristics with which to assign weight to nodes/ contributions
* If we had "Good First Issue", would we still need "Contributions Welcome" as a tag? [23:00](https://www.youtube.com/watch?v=3NgANZNdSlo#t=23m00s)
* One potential ambiguity in the "Contributions Welcome" label is that it sort of implies that other Issues are not welcome to contributions? Does an Issue without a Contributions Welcome label signify that contributors shouldn't try to take it on?

####  How can we be proactive about onboarding new contributors? [24:08](https://www.youtube.com/watch?v=3NgANZNdSlo#t=24m08s)
* Can we think of other ways, both in the way that SourceCred assigns Cred and in the management of the SourceCred project, to reward experienced contributors for actions that help onboard and ramp up new contributors?
* Pair program with newcomers/ help people with their first pull request
* Live coding [29:16](https://www.youtube.com/watch?v=3NgANZNdSlo#t=29m16s)?
* Find people who haven't contributed and reach out/ schedule a video call to walk them through the codebase
* What's the appropriate format? Should it be 1:1 with a maintainer or several people working at a time with the maintainer switching between helping each of them? Private verse public? Should this be separate from Office Hours or a section in Office Hours?
* A conservative, maneagable format to start: 1:1, private, half-an-hour timeframe, with the option to make the video public.
* Pair Programming with new contributors would signal to other new contributors that they can contribute to SourceCred.
* Beginners often ask great questions that reveal important blind spots/ limitations in the project and **it's important to communicate to new contributors that their "beginner" questions are valuable to the project/ that their contributions are welcomed and valued**.  

####  Logistics [37:00](https://www.youtube.com/watch?v=3NgANZNdSlo#t=37m00s)
* 👍to bi-weekly Office Hours

Technical Deep Dive [38:35](https://www.youtube.com/watch?v=3NgANZNdSlo#t=38m35s)

#### Plugins

#### Why is SourceCred built around a plugin architecture? [39:30](https://www.youtube.com/watch?v=3NgANZNdSlo#t=39m30s)

By decoupling the core graph infrastructure from any domain specific knowledge about what goes into the graph, we can apply the SourceCred analysis tools to a broader range of data sources and uses cases.

The Graph infrastructure knows nothing about the type of data it's analyzing; for exmaple, it doesn't know whether it's a graph of pull requests, scientific paper citations, or forum comments. If the graph required knowledge about the type of data it was analyzing, then we couldn't apply the same graph analysis tools to different types of data. For example, if the graph infrastructure required Git commit hashes to compute Cred scores, then we wouldn't be able to compute scores for data that didn't have commit hashes.

**Using Git and GitHub data is only part of the long-term aim of SourceCred**... we want to empower communities to compute Cred using whatever data type will provide the most meaning and value to that community. For example, perhaps the community is more oriented towards using StackOverflow, or suppose we want to help academic communities assign cred through paper citations.

#### The Analysis Adapter [41:27](https://www.youtube.com/watch?v=3NgANZNdSlo#t=41m27s)

The first conceptual step in SourceCred is to create graphs, containing different kinds of nodes, and assign scores to those nodes. That happens inside the [Analysis](https://github.com/sourcecred/sourcecred/tree/master/src/analysis) module.

The Analysis Module has an adapter called an [AnalysisAdapter](https://github.com/sourcecred/sourcecred/blob/master/src/analysis/analysisAdapter.js), which specifies the interface that a Plugin needs to provide in order for the Analysis module to compute scores for that Plugin's data.

The required interface is pretty simple: you need to provide a `PluginDeclaration` and a `load` method:


```javascript
export interface IAnalysisAdapter {
declaration(): PluginDeclaration;
load(sourcecredDirectory: string, repoId: RepoId): Promise<Graph>;
}
```
Each plugin, for example the Git and GitHub plugins, need to provide their own implementations of this AnalysisAdapter interface (Git [here](https://github.com/sourcecred/sourcecred/blob/master/src/plugins/git/analysisAdapter.js) and GitHub [here](https://github.com/sourcecred/sourcecred/blob/master/src/plugins/github/analysisAdapter.js)) in order to receive Cred scores for their data.

The [PluginDeclaration](https://github.com/sourcecred/sourcecred/blob/master/src/analysis/pluginDeclaration.js) that an Analysis Adapter returns at `declearation()` specifies the Plugin's `name`, `nodePrefix`, `edgePrefix`, `NodeTypes`, and `EdgeType`:

```javascript

export type PluginDeclaration = {|
+name: string,
+nodePrefix: NodeAddressT,
+edgePrefix: EdgeAddressT,
+nodeTypes: $ReadOnlyArray<NodeType>,
+edgeTypes: $ReadOnlyArray<EdgeType>,
|};
```

`NodePrefix` is particularly important, as it specifies a string prefix that all nodes of that Plugin will share, so that we have an easy way of  finding all the nodes that belong to that Plugin.  

The [NodeType](https://github.com/sourcecred/sourcecred/blob/master/src/analysis/types.js) also contains a string prefex that all nodes of that `NodeType` will share:

```javascript
export type NodeType = {|
+name: string,
+pluralName: string,
+prefix: NodeAddressT,
+defaultWeight: number,
|};
```
`NodeTypes` also have an important property called `defaultWeight`, which tells the Graph how to assign weights to each node type in the graph.

The second piece of the Plugin's contract with the Analysis Adapter is that it needs to provide a function that generates and saves the Graph, so that the Analysis Module can merge it into the rest of the SourceCred graph.

A summary list of the different types and properties involved in the Analysis Adapter interface:

* `declaration(): PluginDeclaration`
* name
* nodePrefix  --> shared by all nodes belonging to this Plugin
* edgePrefix
* nodeTypes
* name
* pluralName
* prefix  --> shared by all nodes belonging to this NodeType
* defaultWeight --> tell the graph how much weight to assign nodes of this type
* edgeTypes
* forwardName
* backwardName
* defaultForwardWeight
* defaultBackwardWeight
* prefix --> shared by all edges belonging to this EdgeType
* `load()` method  --> a function to generate and save the graph

#### Example: The [Git Plugin](https://github.com/sourcecred/sourcecred/tree/master/src/plugins/git)

The Git plugin's [Analysis Adapter](https://github.com/sourcecred/sourcecred/blob/master/src/plugins/git/analysisAdapter.js), found in the plugins/git directory, provides the `declaration()` and `load()` methods:

```javascript
export class AnalysisAdapter implements IAnalysisAdapter {
declaration() {
return declaration;
}

async load(sourcecredDirectory: string, repoId: RepoId): Promise<Graph> {
const file = path.join(                     // 1) specifies a filepath
sourcecredDirectory,
"data",
repoIdToString(repoId),
"git",
"graph.json"
);                                              
const rawData = await fs.readFile(file);        // 2) reads the file
const json = JSON.parse(rawData.toString());    // 3) parses the file as JSON
return Graph.fromJSON(json);                    // 4) uses the built-in graph
//    deserializer to get that JSON out
}
}
```
The `load` function in the Git Adapter's declaration 1) specifies a filepath and 2) reads the file, 3) parses it as JSON, and then 4) use the built-in Graph deserializer to get that JSON back out.

The Git plugin's [Declaration](https://github.com/sourcecred/sourcecred/blob/master/src/plugins/git/appAdapter.js) module provides the `PluginDeclaration` and definitions for the plugin's `NodeTypes` and `EdgeTypes`.

#### The App Adapter [45:39](https://www.youtube.com/watch?v=3NgANZNdSlo#t=45m39s)
(Probably should be named the Explorer Adapter)

The Analysis Adapter is only reponsible for computing scores. But if we look at the SourceCred Prototype, we can see the Explorer is rendering a bunch of additional type specific information, such as nicely formatted GitHub handles of contributors and links to their GitHub profiles.

The [App Adapter](https://github.com/sourcecred/sourcecred/blob/master/src/explorer/adapters/appAdapter.js) is where that magic happens. It loads display information about each node from the backend, because that display information is not in the Graph. Eg, the number, title, url of an Issue is stored in a separate database from the Graph.

The App Adapter is composed of two parts: the Static Adapter and the Dynamic Adapter.

The Static Adapter provides data without having to fetch it from the backend, while the Dynamic Adapter provides information that requires data to be loaded from the backend. Importantly, we don't generally know beforehand what data needs to be loaded from the backend. By keeping this loading logic at the interface level, SourceCred can remain unaware of how that loading logic is carried out, eg SourceCred doesn't care if you're loading a JSON blob or an SQlite database.

Again, the Git and GitHub plugins must both provide their own implementations of the App Adapter if they want to display their data in the Explorer (Git [here](https://github.com/sourcecred/sourcecred/blob/master/src/plugins/git/appAdapter.js) and GitHub [here](https://github.com/sourcecred/sourcecred/blob/master/src/plugins/github/appAdapter.js)).

#### Why do we have separate Explorer Adapters and Analysis Adapters? [52:14](https://www.youtube.com/watch?v=3NgANZNdSlo#t=52m14s)

We split these apart because we want to eventually run SourceCred on the backend, without any coupling to frontend logic. Separating the frontend logic from the logic for computing scores (a backend task) is a step in that direction.


#### Unit Testing with Snapshots [55:23](https://www.youtube.com/watch?v=3NgANZNdSlo#t=55m23s)
* Question: What happens when we make a change that requires a modification to a Test Snapshot?
* Answer: Update the Snapshot and we'll review the changes to the Snapshot in your Pull Request Review.

#### Serialization/Deserialization [56:09](https://www.youtube.com/watch?v=3NgANZNdSlo#t=56m09s)

**We do this a lot because data persistence is so prevelant in this project**
The "graph" natively lives in memory as an instance of a JavaScript class with a bunch properties (ES6 sets + maps etc) and its important that we be able to save graphs to disk and then reload them. Generally speaking, we serialize when we want to take something out of memory and make a fixed copy that we can save to disk. Deserialization is the process by which we reload the graph from disk.

The method we use to serialize a graph is [toJSON](https://github.com/sourcecred/sourcecred/blob/83fa29688ed97c996212fe8d02abe7d2a32ac4c1/src/core/graph.js#L605-L624) and the method we use to deserialize a graph is [fromJSON](https://github.com/sourcecred/sourcecred/blob/83fa29688ed97c996212fe8d02abe7d2a32ac4c1/src/core/graph.js#L629-L640).

We also have this [Compat Utility](https://github.com/sourcecred/sourcecred/blob/master/src/util/compat.js) that allows you to specify a version of the [graphJSON](https://github.com/sourcecred/sourcecred/blob/83fa29688ed97c996212fe8d02abe7d2a32ac4c1/src/core/graph.js#L146) you're using: if you make a change that updates the format, you'll get an error if you try to deserialize a graph that was created using any previous versions of graphJSON. The Compat Utility will throw a good Error that says you're using an outdated graphJSON format; otherwise, the error is confusing and hard to pinpoint.
