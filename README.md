List of resources on testing distributed systems curated by Andrey Satarin ([@asatarin](https://twitter.com/asatarin)).
If you are interested in my other stuff, [check out talks page](https://asatarin.github.io/talks/).
For any questions or suggestions you can reach out to me on Twitter ([@asatarin](https://twitter.com/asatarin)),
Mastodon (<a rel="me" href="https://discuss.systems/@asatarin">https://discuss.systems/@asatarin</a>)
or [LinkedIn](https://www.linkedin.com/in/asatarin/).

{% comment %}
Private notes https://docs.google.com/document/d/1xHt_PK9yGMTP6JNDMydQLF4SHIdlq-BF9IZeTOXtIOg/edit
{% endcomment %}

**Table of Contents**

[//]: # (@formatter:off)
* A Markdown unordered list which will be replaced with the ToC
{:toc}

[//]: # (@formatter:on)

## Overview of Testing Approaches

### Research Papers

#### Bugs

* [What Bugs Live in the Cloud? A Study of 3000+ Issues in Cloud Systems](https://dl.acm.org/doi/abs/10.1145/2670979.2670986)—
  study of actual bugs in different popular distributed systems (Hadoop MapReduce, HDFS, HBase, Cassandra, ZooKeeper
  and Flume)
* [TaxDC: A Taxonomy of Non-Deterministic Concurrency Bugs in Datacenter Distributed Systems](https://dl.acm.org/doi/abs/10.1145/2872362.2872374)—
  comprehensive taxonomy of bugs in distributed systems (Cassandra, Hadoop MapReduce, HBase, ZooKeeper)
* [An Empirical Study on Crash Recovery Bugs in Large-Scale Distributed Systems](https://dl.acm.org/doi/10.1145/3236024.3236030) —
  based on bug database from "What Bugs Live in the Cloud?" paper researchers focus specifically on crash recovery bugs
  in Hadoop MapReduce, HBase, Cassandra, ZooKeeper. There is review of this paper
  by [Murat Demirbas](https://twitter.com/muratdemirbas)
  in [his blog](https://muratbuffalo.blogspot.com/2019/01/paper-review-empirical-study-on-crash.html).
* [An empirical study on the correctness of formally verified distributed systems](https://blog.acolyer.org/2017/05/29/an-empirical-study-on-the-correctness-of-formally-verified-distributed-systems/)—
  study of bugs in formally verified distributed systems. Analysis includes
  Microsoft's [IronFleet distributed key-value store](https://www.microsoft.com/en-us/research/publication/ironfleet-proving-practical-distributed-systems-correct/)
  built from formal model.
* [What bugs cause cloud production incidents?](https://blog.acolyer.org/2019/06/21/what-bugs-cause-cloud-production-incidents/) —
  research focused on bugs (and their resolution strategies) that actually cause production incidents in large-scale
  distributed services at [Microsoft](#microsoft) Azure.

#### Testing

* [Simple Testing Can Prevent Most Critical Failures: An Analysis of Production Failures in Distributed Data-Intensive Systems](https://www.usenix.org/conference/osdi14/technical-sessions/presentation/yuan) —
  Great overview of how even simple testing can help a lot, you just need the right focus
* [Early detection of configuration errors to reduce failure damage](https://blog.acolyer.org/2016/11/29/early-detection-of-configuration-errors-to-reduce-failure-damage/)—
  why and how to test configuration files of your system
* [Why Is Random Testing Effective for Partition Tolerance Bugs?](https://dl.acm.org/doi/abs/10.1145/3158134) — just
  what it says in a title, authors try to explain why random testing ([Jepsen](#jepsen)) is effective and introduce
  notions of test coverage relating to network partition, see
  also ["The Morning Paper" review](https://blog.acolyer.org/2018/01/23/why-is-random-testing-effective-for-partition-tolerance-bugs/)
  or a [video](https://youtu.be/g5cehS7ZSJ8) from POPL 2018.
* [FlyMC: Highly Scalable Testing of Complex Interleavings in Distributed Systems](https://dl.acm.org/doi/pdf/10.1145/3302424.3303986) —
  novel approach of systematically exploring interleavings in distributed systems augmented with static analysis and
  prioritization. This approach is faster than previous techniques and found old and new bugs in several systems
  (Cassandra, Ethereum Blockchain, Hadoop, Kudu, Raft LogCabin, Spark, ZooKeeper).
* [Torturing Databases for Fun and Profit](https://www.usenix.org/system/files/conference/osdi14/osdi14-paper-zheng_mai.pdf) —
  checking ACID guarantees of open source and commercial databases under power
  loss, [additional material](https://www.usenix.org/node/186197)
* [Understanding and Detecting Software Upgrade Failures in Distributed Systems](https://dl.acm.org/doi/10.1145/3477132.3483577) —
  paper presents first study of upgrade failures in distributed systems (Cassandra, HBase, Kafka, Mesos, YARN,
  ZooKeeper, etc).
  Authors look at severity, symptoms, causes and triggers of these failures and summarize results in a number of
  findings.
  They propose two new tools to improve testing targeting upgrade failures specifically and apply those tools
  to a few systems with good results (new bugs and potential bugs found).
  I gave an [overview talk](https://asatarin.github.io/talks/2022-09-upgrade-failures-in-distributed-systems/) of the
  paper in September 2022.

#### Fault Tolerance

* [Redundancy does not imply fault tolerance: analysis of distributed storage reactions to single errors and corruptions](https://blog.acolyer.org/2017/03/08/redundancy-does-not-imply-fault-tolerance-analysis-of-distributed-storage-reactions-to-single-errors-and-corruptions/)—
  study of several distributed systems (Redis, ZooKeeper, MongoDB, Cassandra, Kafka, RethinkDB) on how fault-tolerant
  they are to data corruption and read/write errors
* [The Case for Limping-Hardware Tolerant Clouds](https://www.usenix.org/node/174577)— research on effect of limping
  hardware on performance of a distributed systems (aka limplock), see also great blog post by Dan Luu on a similar
  topic [Distributed systems: when limping hardware is worse than dead hardware](https://danluu.com/limplock/)
* [Toward a Generic Fault Tolerance Technique for Partial Network Partitioning](https://www.usenix.org/conference/osdi20/presentation/alfatafta) —
  overview of network partition failures in various distributed systems (MongoDB, HBase, HDFS, Kafka, RabbitMQ,
  Elasticsearch, Mesos, etc), common traits among them and strategies to mitigate those failures.
* [Understanding, Detecting and Localizing Partial Failures in Large System Software](https://www.usenix.org/conference/nsdi20/presentation/lou) —
  what happens if your system loses some functionality due to failure as opposed to full fail-stop?
  Authors study how these partial failures manifest in distributed systems (ZooKeeper, Cassandra, HDFS, Mesos) and what
  triggers them.
  They propose runtime approach to detect those failure with mimic-style intrinsic watchdogs and show how these
  watchdogs could be generated automatically.
  They managed to reproduce 20 out of 22 real world partial failures and detect them using intrinsic watchdogs with
  great code localization and reaction time within a few seconds.
  See also [overview talk](https://asatarin.github.io/talks/2022-05-understanding-partial-failures/) of the paper.

### Resilience In Complex Adaptive Systems

These materials are not directly related to testing distributed systems, but they greatly contribute to general
understanding of such systems.

* [Velocity NY 2013: Richard Cook, "Resilience In Complex Adaptive Systems"](https://youtu.be/PGLYEDpNu60)
* [Velocity 2012: Richard Cook, "How Complex Systems Fail"](https://youtu.be/2S0k12uZR14)
* [How Complex Systems Fail](hhttps://www.cs.jhu.edu/~huang/cs624/spring22/readings/how-complex-systems-fail.pdf)

### Jepsen

State-of-the-art approach to testing stateful distributed systems.

* [Jepsen Analyses](https://jepsen.io/analyses) — most recent Jepsen analyses of different distributed systems
* [Jepsen Talks](https://jepsen.io/talks) — talks by Kyle Kingsbury at various conferences
* [Aphyr's Jepsen posts](https://aphyr.com/tags/Jepsen) — older Jepsen analyses on Kyle Kingsbury's (Aphyr) personal
  site
* [Jepsen Talks on GitHub](https://github.com/aphyr/jepsen-talks) — Jepsen talks slides before 2015 on GitHub
* [Kyle Kingsbury on InfoQ](https://www.infoq.com/author/Kyle-Kingsbury)
* [Call me maybe: Jepsen and flaky networks](https://www.slideshare.net/shalinmangar/call-me-maybe-jepsen-and-flaky-networks) —
  talk on Jepsen, not by Kyle
* [Jepsen is used by Microsoft CosmosDB](https://twitter.com/dharmashukla/status/869104163510034432) — founder of Azure
  CosmosDB confirms, that they are using Jepsen
* [Consistency Models](https://jepsen.io/consistency) — overview of various consistency models for distributed systems
  with transactional and non-transactional semantics. This page gives bird's-eye view on guarantees distributed systems
  might provide with references to do a deep dive.

Elle transactional consistency checker for black-box databases:

* [Elle: Inferring Isolation Anomalies from Experimental Observations](https://github.com/jepsen-io/elle/raw/master/paper/elle.pdf) —
  paper on Elle design by Kyle Kingsbury and Peter Alvaro. You might also check out overview of the paper
  from [Murat Demirbas](https://muratbuffalo.blogspot.com/2020/04/elle-inferring-isolation-anomalies-from.html)
  or [The Morning Paper](https://blog.acolyer.org/2020/11/23/elle/) blog
* Elle [source code](https://github.com/jepsen-io/elle)
* [Black-box Isolation Checking with Elle](https://youtu.be/OPJ_IcdSqig) — talk Kyle gave
  at [CMU DB](https://db.cs.cmu.edu/) database seminar describing Elle and results obtained with it
* [Elle: Finding Isolation Violations in Real-World Databases](https://youtu.be/EjNf_kbx36E) — keynote by Kyle Kingsbury
  on Elle at PODC 2021
* [Elle: Opaque-box Serializability Verification](https://aphyr.com/media/talks/2021/vldb.mp4) — talk by Kyle Kingsbury
  and Peter Alvaro on Elle at VLDB 2021

Some notable Jepsen analyses:

* [CockroachDB beta-20160829](https://jepsen.io/analyses/cockroachdb-beta-20160829)
* [VoltDB 6.3](https://jepsen.io/analyses/voltdb-6-3)
* [Jepsen: RethinkDB 2.2.3 reconfiguration](https://aphyr.com/posts/330-jepsen-rethinkdb-2-2-3-reconfiguration)
* [Jepsen: RethinkDB 2.1.5](https://aphyr.com/posts/329-jepsen-rethinkdb-2-1-5)
* [Radix DLT 1.0-beta.35.1](https://jepsen.io/analyses/radix-dlt-1.0-beta.35.1)
* [Dgraph 1.1.1](https://jepsen.io/analyses/dgraph-1.1.1)

Jepsen is used by [CockroachDB](#cockroachlabs-cockroachdb), [VoltDB](#voltdb), [Cassandra](#cassandra),
[ScyllaDB](#scylladb), [YDB](#ydb) and others.

### Formal Methods

* [The verification of a distributed system By Caitie McCaffrey](https://queue.acm.org/detail.cfm?id=2889274)
  also [podcast](https://www.infoq.com/articles/podcast-caitie-mccaffrey)
  and [talk](https://www.infoq.com/presentations/distributed-systems-verification) on InfoQ.com
  and [accompanying materials](https://github.com/CaitieM20/Talks/tree/master/TheVerificationOfADistributedSystem) on
  GitHub and a [slidedeck](https://speakerdeck.com/caitiem20/qcon-newyork-2016-the-verification-of-a-distributed-system)
* [Comparisons of Alloy and Spin](https://www.pamelazave.com/compare.html)
* [Verdi — A framework for formally verifying distributed systems implementations in Coq](https://github.com/uwplse/verdi)
* [Network Semantics for Verifying Distributed Systems](https://homes.cs.washington.edu/~jrw12/network-semantics.html)
* [Proving that Android’s, Java’s and Python’s sorting algorithm is broken (and showing how to fix it)](https://web.archive.org/web/20220329052326/http://envisage-project.eu/proving-android-java-and-python-sorting-algorithm-is-broken-and-how-to-fix-it/)—
  using formal verification to find a bug in TimSort sorting algorithm
* [Proving JDK’s Dual Pivot Quicksort Correct](https://www.key-project.org/2017/08/17/dual-pivot/)— analyzing quicksort
  implementation in Java

#### TLA+

* [Designing Distributed Systems in TLA+](https://www.hillelwayne.com/talks/distributed-systems-tlaplus/) by Hillel
  Wayne, and talk [Everything about distributed systems is terrible](https://youtu.be/tfnldxWlOhM)
* [Designing distributed systems with TLA+](https://youtu.be/2PIgZ6hd-6I) by Hillel Wayne at Hydra Conference 2020
* [Distributed systems showdown — TLA + vs real code](https://youtu.be/sPSPEgz3o9U)
  by [Jack Vanlightly](https://twitter.com/vanlightly) at Hydra Conference 2021. Jack compares two approaches to testing
  distributed systems — formal verification of the design with TLA+ and testing with Maelstrom/Jepsen, comparing pros
  and cons.
* "Workshop: TLA+ in action" by [Markus Kuppe](https://twitter.com/lemmster) in four parts
  [1](https://youtu.be/rBVhDKfg9fQ), [2](https://youtu.be/N0WOXFWBnhc),
  [3](https://youtu.be/Im63Kl3tB2g), [4](https://youtu.be/FBEviGMuOK8) at Hydra Conference 2021
* [TLA+ Conference](https://conf.tlapl.us/home/) is a forum to present case studies tools and techniques using TLA+

Companies using TLA+ to verify correctness of algorithms:

* [Amazon Web Services](#amazon-web-services)
* [PingCap for TiDB](#pingcap-tidb)
* [Elastic](#elastic-elasticsearch)
* [MongoDB](#mongodb)
* [CockroachLabs](#cockroachlabs-cockroachdb)
* [Microsoft](#microsoft) for services in Azure cloud
* [Confluent](#confluent-kafka) for Apache Kafka

### Deterministic Simulation

Pioneered by [FoundationDB](#foundationdb), deterministic simulation approach to testing distributed systems gained
more popularity in recent years.

* ["Simulation Testing"](https://youtu.be/N5HyVUPuU0E) by Michael Nygard gives a good introduction into simulation
  testing
* [Designing Dope Distributed Systems for Outer Space with High-Fidelity
  Simulation](https://www.youtube.com/watch?v=prM-0i58XBM)— talk about using deterministic simulation to test
  distributed space telescope. With recommendations on how to move file IO, network, scheduling out of your program
  to make it more amenable to simulation.
* [What's the big deal about Deterministic Simulation Testing?](https://notes.eatonphil.com/2024-08-20-deterministic-simulation-testing.html) —
  Phil Eaton gives an introduction to deterministic simulation testing, discussing basics and challenges.

More companies and systems adopt deterministic simulation as a primary testing strategy:

* [FoundationDB](#foundationdb)
* [TigerBeetle](#tigerbeetle)
* [Convex](#convex)
* [RisingWave](#risingwave)
* [Amazon Web Services](#amazon-web-services) uses SimWorld to test Elastic Block Storage control plane
* [Red Planet Labs](#red-planet-labs)
* [Sled](#sled)

See also [autonomous testing](#autonomous-testing), [FoundationDB](#foundationdb).

### Autonomous Testing

This approach is currently represented by [Antithesis](https://antithesis.com/) — pioneers in autonomous testing,
defining the space and the state of the art. Will Wilson (of [FoundationDB](#foundationdb) fame) is one of the founders.

* [Testing a Single-Node, Single Threaded, Distributed System Written in 1985](https://youtu.be/m3HwXlQPCEU) by Will
  Wilson. This is a comprehensive introduction into autonomous testing by using Super Mario Bros. (game) as a testing
  target. The autonomous testing platform plays the game and achieves remarkable results leveraging simple interface and
  a straightforward goal. Will does a great job of delivering the talk and it's fascinating to watch. Copy of the talk
  video on Vimeo [Why Antithesis Works](https://vimeo.com/929637128).
* Accompanying blog post to the talk above (or vice
  versa) [Is something bugging you?](https://antithesis.com/blog/is_something_bugging_you/) with reasoning behind
  Antithesis and value proposition and history on [FoundationDB](#foundationdb). The post introduces Antithesis platform
  to deliver [FoundationDB](#foundationdb) style deterministic testing with autonomous capabilities to everybody.
  See [comprehensive discussion](https://news.ycombinator.com/item?id=39356920) on Hacker News.
* [Accelerating developers at MongoDB](https://antithesis.com/case_studies/mongodb_productivity/) — case study of using
  Antithesis as [MongoDB](#mongodb)
* [Testing the Ethereum merge](https://antithesis.com/case_studies/ethereum_merge/) — case study of using Antithesis for
  testing Ethereum
* [Autonomous Testing and the Future of Software Development](https://youtu.be/fFSPwJFXVlw) — Will Wilson
  talks about why testing sucks and how to fix it with the new autonomous testing approach by making testing less human
  involved. This talk is a precursor to above talks and posts on autonomous testing.
* [Torturing Postgres: extreme autonomous testing for distributed architectures](https://medium.com/@thinkx_/torturing-postgres-extreme-autonomous-testing-for-distributed-architectures-e1c4139ed72e)—
  how OrioleDB uses Antithesis to test the database
* [Chaos Testing Stardog Cluster for Fun and Profit](https://www.stardog.com/labs/blog/chaos-testing-stardog-cluster-for-fun-and-profit/)

See also [deterministic simulation](#deterministic-simulation), [FoundationDB](#foundationdb) and [fuzzing](#fuzzing).

### Lineage-driven Fault Injection

* [Lineage-driven Fault Injection](https://dl.acm.org/citation.cfm?id=2723711)
* [Abstracting the Geniuses Away from Failure Testing](https://queue.acm.org/detail.cfm?id=3155114)

[Netflix](#netflix) adopted lineage-driven fault injection techniques for testing microservices.

### Chaos Engineering

* [Principles of Chaos Engineering](https://principlesofchaos.org/)
* Free [Chaos Engineering](https://www.oreilly.com/webops-perf/free/chaos-engineering.csp) book by [Netflix](#netflix)
  engineers
* [A curated list of awesome Chaos Engineering resources](https://github.com/dastergon/awesome-chaos-engineering)

[Netflix](#netflix) pioneered chaos engineering discipline.

### Fuzzing

There are two flavors of fuzzing. First, randomized concurrency testing, where the ordering of messages is fuzzed:

* [Fuzzing Raft for Fun and Publication](https://colin-scott.github.io/blog/2015/10/07/fuzzing-raft-for-fun-and-profit/)
* [Combining AFL and QuickCheck for Directed Fuzzing by Dan Luu](https://danluu.com/testing/)

And input fuzzing, where message contents or user inputs are fuzzed:

* [DNS parser, meet Go fuzzer](https://blog.cloudflare.com/dns-parser-meet-go-fuzzer/)
* [Fuzz Testing with afl-fuzz (American Fuzzy Loop)](https://spin.atomicobject.com/2015/08/23/fuzz-testing-american-fuzzy-lop/)
* [Randomized testing for Go](https://github.com/dvyukov/go-fuzz) and talk on this
  tool [GopherCon 2015: Dmitry Vyukov — Go Dynamic Tools](https://www.youtube.com/watch?v=a9xrxRsIbSU)
* [Simple guided fuzzing for libraries using LLVM`s new libFuzzer](https://blog.llvm.org/2015/04/fuzz-all-clangs.html)
* [LibFuzzer – a library for coverage-guided fuzz testing](https://llvm.org/docs/LibFuzzer.html)
* [How Heartbleed could've been found](https://blog.hboeck.de/archives/868-How-Heartbleed-couldve-been-found.html) —
  example of how fuzzing could be used for finding famous HeartBleed vulnerability

See also [autonomous testing](#autonomous-testing).

### Microservices

Amazing and comprehensive overview of different strategies to test systems built with microservices by Cindy Sridharan.

* [Testing Microservices, the sane way](https://copyconstruct.medium.com/testing-microservices-the-sane-way-9bb31d158c16)

Series of blog posts specifically on testing in production — best practices, pitfalls, etc:

* [Testing in Production, the safe way](https://copyconstruct.medium.com/testing-in-production-the-safe-way-18ca102d0ef1)
* [Testing in Production: the hard parts](https://copyconstruct.medium.com/testing-in-production-the-hard-parts-3f06cefaf592)

### Performance and Benchmarking

* [Your Load Generator Is Probably Lying To You](https://highscalability.com/blog/2015/10/5/your-load-generator-is-probably-lying-to-you-take-the-red-pi.html)
* [Everything You Know About Latency Is Wrong](https://bravenewgeek.com/everything-you-know-about-latency-is-wrong/)—
  great overview of Gil Tene`s "How NOT to Measure Latency" talk
* ["How NOT to Measure Latency" by Gil Tene](https://www.youtube.com/watch?v=lJ8ydIuPFeU)
* ["Benchmarking: You're Doing It Wrong" by Aysylu Greenberg](https://www.youtube.com/watch?v=XmImGiVuJno)
* [Performance Analysis Methodology](https://www.brendangregg.com/methodology.html) — approaches developed by Brendan
  Gregg for analysing performance in systematic fashion

See also [benchmarking](#benchmarking) tools.

### Misc

* [Metamorphic Testing](https://www.hillelwayne.com/post/metamorphic-testing/) — overview of what metamorphic testing is
  and where it can help. For more details see
  paper ["Metamorphic Testing: A Review of Challenges and Opportunities"](https://www.cs.hku.hk/data/techreps/document/TR-2017-04.pdf).
* [Testing Distributed Systems for Linearizability](https://www.anishathalye.com/2017/06/04/testing-distributed-systems-for-linearizability/) —
  describes linearizability testing tool [Porcupine](https://github.com/anishathalye/porcupine), written in Go.

#### Testing in a Distributed World

Great overview of techniques for testing distributed systems from practitioner,
the [video](https://youtu.be/iZEXIN7-9tM) did age well and still an excellent overview of the landscape.
Additional materials could be found in [this GitHub repo](https://github.com/Randommood/RICON2014)

#### Game Days

* [Sometimes Kill -9 Isn’t Enough](https://bravenewgeek.com/sometimes-kill-9-isnt-enough/)

#### Technologies for Testing Distributed Systems

Colin Scott shares his viewpoint from academia on testing distributed systems,
specifically regression testing for correctness and performance bugs.

* [Technologies for Testing Distributed Systems, Part I](https://colin-scott.github.io/blog/2016/03/04/technologies-for-testing-and-debugging-distributed-systems/)
* See also
  post [Distributed Systems Testing: The Lost World](https://tagide.com/blog/research/distributed-systems-testing-the-lost-world/)
  by Crista Lopes

#### Test Case Reduction

* [Minimizing Faulty Executions of Distributed Systems](https://www.usenix.org/system/files/conference/nsdi16/nsdi16-paper-scott.pdf) —
  reducing the size of buggy executions to make them easier to understand. 60 minute
  talk [here](https://www.microsoft.com/en-us/research/video/minimizing-faulty-executions-distributed-systems/)
* [Troubleshooting Blackbox SDN Control Software with Minimal Causal Sequences](https://dl.acm.org/doi/pdf/10.1145/2619239.2626304) —
  similar to above, but requires less instrumentation.
* [Concurrency Debugging with Differential Schedule Projections](https://brandonlucia.com/pubs/symbiosis_final_pldi.pdf) —
  find and minimize concurrency bugs using program analysis. Shared memory systems are equivalent to message passing
  systems, so you can apply the same techniques to distributed systems.

## Specific Approaches in Different Distributed Systems

### Google

* [Efficient Exploratory Testing of Concurrent Systems](https://www.pdl.cmu.edu/PDL-FTP/associated/CMU-PDL-11-113.pdf)—
  They don't mention it but looks like they describe testing of Google Omega
* [Exploratory Testing Architecture (ETA) ](https://github.com/google/cluster-data/blob/master/ETAExplorationTraces.md)
* [Paxos Made Live — An Engineering Perspective](https://research.google.com/pubs/pub33002.html) has a section on
  testing
* [10 Years of Crashing Google](https://www.usenix.org/conference/lisa15/conference-program/presentation/krishnan)
  describes some war stories from Disaster Recovery Testing (DiRT) team at Google
* [Testing for Reliability](https://landing.google.com/sre/book/chapters/testing-reliability.html) chapter from Google
  Site Reliability Engineering book
* [Randomized Testing of Cloud Spanner](https://medium.com/@jcorbett_26889/randomized-testing-of-cloud-spanner-5286f1eaba75) —
  overview of randomized testing at Cloud Spanner, including how to scale it to large datasets and high concurrency
* [How chaos testing adds extra reliability to Spanner’s fault-tolerant design](https://cloud.google.com/blog/products/databases/chaos-testing-spanner-improves-reiliability) —
  high level overview of fault injection (chaos) testing in Google Spanner discussing various types of injected faults

### Amazon Web Services

* [The Evolution of Testing Methodology at AWS: From Status Quo to Formal Methods with TLA+](https://www.infoq.com/presentations/aws-testing-tla)
* [Use of Formal Methods at Amazon Web Services](https://research.microsoft.com/en-us/um/people/lamport/tla/formal-methods-amazon.pdf)
* [CACM Article "How Amazon Web Services Uses Formal Methods"](https://cacm.acm.org/magazines/2015/4/184701-how-amazon-web-services-uses-formal-methods/fulltext)
* [Debugging Designs by Chris Newcombie](https://www.hpts.ws/papers/2011/sessions_2011/Debugging.pdf) there is also
  a  [source bundle](https://www.hpts.ws/papers/2011/sessions_2011/amazonbundle.tar.gz)
* [Millions of tiny databases](https://blog.acolyer.org/2020/03/04/millions-of-tiny-databases/) — has section on testing
  which describes several approaches: SimWorld simulation resembling approach used at [Foundation DB](#foundationdb),
  use of [Jepsen](#jepsen) and [formal methods](#formal-methods) and [game days](#game-days).
* [Using lightweight formal methods to validate a key-value storage node in Amazon S3](https://www.amazon.science/publications/using-lightweight-formal-methods-to-validate-a-key-value-storage-node-in-amazon-s3) —
  paper on verifying correctness of a new key-value storage node implementation in S3. They are using property-based
  testing and stateless model checking extensively to balance trade-offs and follow pragmatic approach.
  I gave a talk ["Formal Methods at Amazon S3"](https://asatarin.github.io/talks/2022-02-formal-methods-at-amazon-s3/)
  on this paper for a reading group.

See also [formal methods](#formal-methods) and [deterministic simulation](#deterministic-simulation) sections.

### Netflix

Automated failure injection (see also [Lineage-driven Fault Injection](#lineage-driven-fault-injection)):

* [Monkeys in Lab Coats: Applying Failure Testing Research @Netflix](https://www.infoq.com/presentations/failure-test-research-netflix)
* [“Monkeys in Labs Coats”: Applied Failure Testing Research at Netflix](https://www.infoq.com/news/2016/03/failure-testing-netflix)
* [Automated Failure Testing](https://netflixtechblog.com/automated-failure-testing-86c1b8bc841f)
* [Automating Failure Testing Research at Internet Scale](https://dl.acm.org/doi/abs/10.1145/2987550.2987555)
  by P. Alvaro et. el.

Random/manual failure injection testing:

* [Netflix Simian Army](https://netflixtechblog.com/the-netflix-simian-army-16e57fbab116)
* [Failure Injection Testing](https://netflixtechblog.com/fit-failure-injection-testing-35d8e2a9bb2)
* [From Chaos to Control — Testing the resiliency of Netflix’s Content Discovery Platform](https://netflixtechblog.com/from-chaos-to-control-testing-the-resiliency-of-netflixs-content-discovery-platform-ce5566aef0a4)
* [Breaking Bad at Netflix: Building Failure as a Service](https://www.infoq.com/presentations/failure-as-a-service-netflix)
* [GTAC 2014: I Don't Test Often ... But When I Do, I Test in Production](https://www.youtube.com/watch?v=xkP70Zhhix4)—
  Netflix different testing strategies

See also [chaos engineering](#chaos-engineering) and [lineage-driven fault injection](#lineage-driven-fault-injection).

### Microsoft

* [Asynchronous programming, analysis and testing with state machines](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/paper-6.pdf) —
  Open source language for building distributed systems. Language is designed with tooling in mind, particularly,
  automatic exploration of message orderings in order to find bugs.
* [Uncovering Bugs in Distributed Storage Systems during Testing (not in Production!)](https://www.usenix.org/system/files/conference/fast16/fast16-papers-deligiannis.pdf)
* [Windows Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency](https://www.sigops.org/sosp/sosp11/current/2011-Cascais/11-calder-online.pdf)
  describes "Pressure Point Testing" approach used for Azure Cloud Storage
* [Inside Azure Search: Chaos Engineering](https://azure.microsoft.com/ru-ru/blog/inside-azure-search-chaos-engineering/)
* [TLA+ at Microsoft: 16 Years in Production](https://youtu.be/azx6cX-BlCs) by David Langworthy — how rejuvenation of
  TLA+ happened at Microsoft in 2016 and onwards

See also [formal methods](#formal-methods) section.

### Meta

* [BellJar: A new framework for testing system recoverability at scale](https://engineering.fb.com/2022/05/05/developer-tools/belljar/) —
  BellJar
  is a testing framework focused on answering question "What service dependencies are required for the service to
  recover after large scale disaster?". BellJar puts service in a vacuum environment with only handful of direct
  dependencies allow-listed to verify that recovery procedures succeed under those constraints. It checks those recovery
  procedures in CI/CD pipeline preventing unconstrained growth of dependency graph and circular dependencies. Based on
  BellJar tests one can construct the entire dependency graph of the services allowing to boostrap them in the
  correct order from bottom to top.
* [Vacuum Testing for Resiliency: Verifying Disaster Recovery in Complex](https://youtu.be/Qdn2MDMOmOo) — talk on how
  BellJar is used at Meta to test recovery of distributed systems

### FoundationDB

* ["Testing Distributed Systems w/ Deterministic Simulation" by Will Wilson](https://youtu.be/4fFDFbi3toc) — talk on
  FoundationDB simulation testing. Their architecture was built from the ground up to support fully deterministic
  simulation testing
* [Simulation and Testing](https://apple.github.io/foundationdb/testing.html) — public overview of FoundationDB
  simulation testing framework
* [FoundationDB or: How I Learned to Stop Worrying and Trust the Database](https://youtu.be/OJb8A6h9jQQ) by Markus
  Pilman from Snowflake — updated talk on testing FoundationDB with deterministic simulation. Markus goes into details
  of what it takes to build deterministic simulation into a database. He mentions that it took two years to build a
  simulation framework before FoundationDB team started working on a database.
* ["Buggify — Testing Distributed Systems with Deterministic Simulation"](https://transactional.blog/simulation/buggify.html) — [Alex
  Miller](https://www.linkedin.com/in/alexmillerdb/), one of developers at FoundationDB, describes BUGGIFY macros, which
  helps bias simulation tests towards doing dangerous and bug finding things. This is a good example of cooperation
  between testing efforts and production code.
* ["FoundationDB: A Distributed Unbundled Transactional Key Value Store"](https://sigmodrecord.org/publications/sigmodRecord/2203/pdfs/08_fdb-zhou.pdf) —
  SIGMOD 2021 paper on FoundationDB has a very detailed section on simulation testing at FoundationDB with discussions
  on determinism, test oracles, fault injection and limitations.
* ["Unlucky Simulation"](https://youtu.be/0h9l6Ug_l5E) — talk on using various scheduling strategies (LibFuzzer, random,
  etc) with simulation testing in FoundationDB

See also [deterministic simulation](#deterministic-simulation) and [autonomous testing](#autonomous-testing).

### Cassandra

* [Testing Apache Cassandra with Jepsen](https://www.datastax.com/dev/blog/testing-apache-cassandra-with-jepsen)
* [Testing Cassandra Guarantees under Diverse Failure Modes with Jepsen](https://www.slideshare.net/jkni/testing-cassandra-guarantees-under-diverse-failure-modes-with-jepsen-53168992)
* [Jepsen Cassandra Testing on Git](https://github.com/riptano/jepsen)
* [Netflix A STATE OF XEN — CHAOS MONKEY & CASSANDRA](https://vimeopro.com/user35188327/cassandra-summit-2015/video/140949186)
  from Cassandra Summit 2015
* [Testing Apache Cassandra with Jepsen: How to Understand and Produce Safe Distributed Systems](https://youtu.be/OnG1FCr5WTI)
  by Joel Knighton presented at Devoxx UK 2016
* [Testing Apache Cassandra 4.0](https://cassandra.apache.org/blog/2018/08/21/testing_apache_cassandra.html) — quick
  overview of approaches used to test next major version of Cassandra
* [Fallout](https://github.com/datastax/fallout) — tool to run distributed tests as a service. It is meant to easily
  orchestrate cluster creation and testing tools like [Jepsen](#jepsen), performance testing tools and others, though
  extension and combining them in various ways with environmental conditions. It could run tests either locally or on
  large scale clusters.
* [Cassandra Harry](https://github.com/apache/cassandra-harry) — [Fuzz testing](#fuzzing) / property-based testing tool
  for Apache Cassandra. Aims to provide reproducible workloads to test correctness of Apache Cassandra.
* [Fuzz Testing and Verification of Apache Cassandra with "Harry"](https://youtu.be/x885ck3mrZo) — talk on Harry fuzz
  testing tool by [Alex Petrov](https://twitter.com/ifesdjeen) at ApacheCon 2021
* [Harry, an Open Source Fuzz Testing and Verification Tool for Apache Cassandra](https://cassandra.apache.org/_/blog/Harry-an-Open-Source-Fuzz-Testing-and-Verification-Tool-for-Apache-Cassandra.html)
  by Alex Petrov — blog post about Harry fuzz testing tool for Apache Cassandra and how it helps to find bugs
* [Garden of Forking Paths](https://youtu.be/q5T5LDooS2w) — talk by Alex Petrov on property-based testing philosophy and
  core ideas based on his experience building Cassandra Harry.

### ScyllaDB

They published series of blog posts on testing ScyllaDB:

* [Scylla testing part 1: Cassandra compatibility testing](https://www.scylladb.com/2016/02/04/cassandra-compatibility-testing/)
* [Scylla testing part 2: Extending Jepsen for testing Scylla](https://www.scylladb.com/2016/02/11/jepsen-testing/)
* [CharybdeFS: a new fault-injecting filesystem for software testing](https://www.scylladb.com/2016/02/16/fault-injection-filesystem-software-testing/)
* [Testing part 4: Distributed tests](https://www.scylladb.com/2016/03/10/dtest-scylla/)
* [Testing part 5: Longevity testing](https://www.scylladb.com/2016/03/15/longevity-testing-scylla/)
* [Fault-injecting filesystem cookbook](https://www.scylladb.com/2016/05/02/fault-injection-filesystem-cookbook/)
  Video from Scylla Summit 2017 on testing
* [How We Constantly Try to Bring Scylla to its Knees](https://youtu.be/K38RDEdt070)
  and [slides](https://www.slideshare.net/ScyllaDB/scylla-summit-2017-cry-in-the-dojo-laugh-in-the-battlefield-how-we-constantly-try-to-bring-scylla-to-its-knees) —
  overview of different testing types at ScyllaDB
* [Project Gemini: An Open Source Automated Random Testing Suite for Scylla and Cassandra Clusters](https://www.scylladb.com/2019/12/11/project-gemini-an-open-source-automated-random-testing-suite-for-scylla-and-cassandra-clusters/) —
  random test generator comparing results from cluster with injected faults against single node running without faults.
  Works on tops of CQL API and suitable for testing any database implementing it. See also talk
  on [Project Gemini](https://youtu.be/QPnlpglmPcY) and [open source code](https://github.com/scylladb/gemini)
* [ScyllaDB NoSQL Database Testing](https://www.scylladb.com/product/technology/scylla-testing/) — highlights of testing
  approaches at Scylla

### Dropbox

* [Mysteries of Dropbox Property-Based Testing of a Distributed Synchronization Service](https://www.cis.upenn.edu/~bcpierce/papers/mysteriesofdropbox.pdf)—
  example of how to use QuickCheck to test synchronization in Dropbox and similar tools (Google Drive). John Hughes gave
  a [talk on this](https://youtu.be/H18vxq-VsCk). See also [QuickCheck](#quickcheck).
* [Data Checking at Dropbox](https://youtu.be/WUaMN2kywR4) — If you have lots of data, you have to verify that it did
  not suffer from bit rot and protect it against rare bugs (e.g. race conditions) to guarantee long term durability.
  This talks explains intricacies of building data consistency checker(s) at Dropbox scale.
* [Dropbox's Exabyte Storage System](https://www.facebook.com/atscaleevents/videos/1741691622770601/) (aka Magic Pocket)
  talk by James Cowling — describes number of strategies to achieve extremely high durability.
  This includes:
    - guard against faulty disks,
    - guard against software defects,
    - guard against black swan events,
    - operational safeguards to reduce blast radius,
    - safeguards against deletes with multi stage soft-delete,
    - comprehensive testing strategy in-depth with increased scale,
    - redundancy across various axis in software and hardware stacks,
    - continuous data integrity validation on many levels,
    - etc
* [Testing sync at Dropbox](https://dropbox.tech/infrastructure/-testing-our-new-sync-engine) — comprehensive overview
  of two test frameworks at Dropbox for new sync engine implementation. CanopyCheck — single threaded and fully
  deterministic randomized testing framework with minimization for synchronization planner component of the engine. The
  other framework Trinity focuses on concurrency and larger surface area of components. Great discussion on tradeoffs
  between determinism, strength of test oracles vs width of coverage and size of the
  system under test.

### Elastic (Elasticsearch)

* [Growing a protocol](https://blog.acolyer.org/2017/08/23/growing-a-protocol/) —
  applying [lineage driven fault injection](#lineage-driven-fault-injection) to test Elasticsearch replication protocol
* [Using TLA+ for fun and profit in the development of Elasticsearch](https://youtu.be/qYDcbcOVurc) by Yannick Welsch —
  Elasticsearch uses [TLA+](#formal-methods) to verify correctness of their replication protocol

See also [formal methods](#formal-methods) section.

### MongoDB

* [MongoDB’s JavaScript Fuzzer: Creating Chaos (1/2)](https://www.mongodb.com/blog/post/mongodbs-java-script-fuzzer-creating-chaos)
* [MongoDB’s JavaScript Fuzzer: Harnessing the Havoc (2/2)](https://www.mongodb.com/blog/post/mongodb-java-script-fuzzer-harnessing-havoc-2)
* [MongoDB's JavaScript Fuzzer](https://queue.acm.org/detail.cfm?id=3059007) article in ACM Queue
* [Fixing a MongoDB Replication Protocol Bug with TLA+](https://youtu.be/x9zSynTfLDE) by William Schultz — how MongoDB
  uses [formal verification](#formal-methods) with TLA+ to check correctness of their replication protocol. Describes
  how replication bugs could have been found with help of formal model.
* [eXtreme Modelling in Practice](https://arxiv.org/abs/2006.00915) — two attempts at MongoDB to check that code
  conforms to its formal model.
* [Formal Verification of a Distributed Dynamic Reconfiguration Protocol](https://youtu.be/VwCBlmS7XEA) — talk on
  formally verifying MongoDB Raft-based replication reconfiguration protocol with TLAPS.
  Paper [preprint](https://arxiv.org/abs/2109.11987).
* [Change Point Detection in Software Performance Testing](https://arxiv.org/abs/2003.00584) — paper on how MongoDB team
  automatically detects performance degradations in the presence of noise in continuous integration runs. The paper was
  presented at [ICPE 2020](https://youtu.be/rSBgcMFPkHU)

See also [formal methods](#formal-methods) section.

### Confluent (Kafka)

* [Kafka Fault Injection framework](https://cwiki.apache.org/confluence/display/KAFKA/Fault+Injection)
* [TLA+ specification of the Kafka replication protocol](https://github.com/hachikuji/kafka-specification) and talk
  about using TLA+
  for [hardening Kafka replication protocol](https://www.confluent.io/kafka-summit-sf18/hardening-kafka-replication)

See also [formal methods](#formal-methods) section.

### CockroachLabs (CockroachDB)

* [DIY Jepsen Testing CockroachDB](https://www.cockroachlabs.com/blog/diy-jepsen-testing-cockroachdb/)— great read about
  using Jepsen at Cockroach Labs
* [CockroachDB Beta Passes Jepsen Testing](https://www.cockroachlabs.com/blog/cockroachdb-beta-passes-jepsen-testing/)—
  CockroachDB tested by Kyle Kingsbury (Jepsen.io)
* [Introducing Pebble: A RocksDB Inspired Key-Value Store Written in Go](https://www.cockroachlabs.com/blog/pebble-rocksdb-kv-store/) —
  introduces new storage engine and includes thorough discussion on what it takes to properly test storage engine
* [ParallelCommits.tla](https://github.com/cockroachdb/cockroach/blob/master/docs/tla-plus/ParallelCommits/ParallelCommits.tla) —
  Formal specification in TLA+ of the [parallel commit](https://www.cockroachlabs.com/blog/parallel-commits/)
  transaction protocol. See also [formal methods](#formal-methods).
* [The importance of being earnestly random: Metamorphic Testing in CockroachDB](https://www.cockroachlabs.com/blog/metamorphic-testing-the-database/) —
  blog post talking about metamorphic testing at CockroachLabs to test Pebble storage engine

### SingleStore

Formerly known as MemSQL.

* [Running SingleStore’s 107 Node Test Infrastructure on CoreOS](https://www.singlestore.com/blog/running-memsqls-107-node-test-infrastructure-on-coreos/).
  See also accompanying [talk](https://youtu.be/uJirOCUg67o).
* [Practical Techniques to Achieve Quality in Large Software Projects](https://www.singlestore.com/blog/test-coverage-manage-long-tail-surfaced-bugs-using-force-multipliers/)
* [How to Make a Believable Benchmark](https://www.singlestore.com/blog/how-to-make-a-believable-benchmark/)
* [Building an Infinitely Scalable Testing System](https://www.singlestore.com/blog/building-an-infinitely-scalable-testing-system/) —
  description of internal test system PsyDuck

### Twitter

* [Diffy: Testing services without writing tests](https://blog.twitter.com/2015/diffy-testing-services-without-writing-tests)
* [How we break things at Twitter: failure testing](https://blog.twitter.com/2015/how-we-break-things-at-twitter-failure-testing)

### LinkedIn

* [Simoorg Failure inducer framework](https://github.com/linkedin/simoorg)— Failure inducer implemented in Python
* [A Deep Dive into Simoorg](https://engineering.linkedin.com/blog/2016/03/deep-dive-Simoorg-open-source-failure-induction-framework)
* [Dynamometer: Scale Testing HDFS on Minimal Hardware with Maximum Fidelity](https://engineering.linkedin.com/blog/2018/02/dynamometer--scale-testing-hdfs-on-minimal-hardware-with-maximum) —
  testing scalability of large Hadoop clusters (namely NameNode) with just fraction of nodes

### Salesforce

* [Go Fast and Don't Break Things: Ensuring Quality in the Cloud](https://www.hpts.ws/papers/2011/sessions_2011/HansmaHPTS2011.pdf)

### VoltDB

Series of post on testing at VoltDB:

* [How We Test at VoltDB](https://www.voltdb.com/blog/2015/09/30/how-we-test-at-voltdb/)
* [Testing at VoltDB: SQLCoverage](https://web.archive.org/web/20210126003050/https://voltdb.com/blog/2016/03/testing-voltdb-sqlcoverage/)—
  describes how they test SQL query functionality using 5 millions queries generated from templates and comparing
  results against HSQLDB
* [Testing VoltDB Against PostgreSQL](https://web.archive.org/web/20210830070918/https://www.voltdb.com/blog/2016/04/testing-voltdb-postgresql/)
* [VoltDB 6.4 Passes Official Jepsen Testing](https://www.voltdb.com/blog/2016/07/12/voltdb-6-4-passes-official-jepsen-testing/)—
  VoltDB hired Kyle Kingsbury ([Jepsen](#jepsen)) to tests their database, they share results in this post

Additional resources:

* ["All In With Determinism for Performance and Testing in Distributed Systems" by John Hugg](https://www.youtube.com/watch?v=gJRj3vJL4wE)
  and a slide
  deck [Hugg-DeterministicDistributedSystems.pdf](https://github.com/strangeloop/StrangeLoop2015/blob/master/slides/talks/Hugg-DeterministicDistributedSystems.pdf)
* [SelfCheck workload](https://github.com/VoltDB/voltdb/tree/master/tests/test_apps/txnid-selfcheck2)
* [TPC-C implementation](https://github.com/VoltDB/voltdb/tree/master/tests/test_apps/tpcc)

### PingCap (TiDB)

* [Use Chaos to test the distributed system linearizability](https://medium.com/@siddontang/use-chaos-to-test-the-distributed-system-linearizability-4e0e778dfc7d)—
  describes Jepsen-like framework implemented in Go and used at PingCap to test TiDB
* [A test framework for linearizability check with Go](https://github.com/siddontang/chaos) — Chaos is a Jepsen-like
  framework written in Go, uses [Porcupine](#misc) linearizability checker
* [Chaos Tools and Techniques for Testing the TiDB Distributed NewSQL Database](https://thenewstack.io/chaos-tools-and-techniques-for-testing-the-tidb-distributed-newsql-database/)
  and the same post on company [blog](https://pingcap.com/blog/chaos-practice-in-tidb/)
* [Official Jepsen report on TiDB 2.1.7](https://jepsen.io/analyses/tidb-2.1.7)
  and [companion blog post](https://pingcap.com/blog/tidb-passes-jepsen-test-for-snapshot-isolation-and-single-key-linearizability/)
  in company blog
* [Safety First! Common Safety Pitfalls in Distributed Databases Found by Jepsen Tests](https://pingcap.com/blog/safety-first-common-safety-pitfalls-in-distributed-databases-found-by-jepsen-tests/) —
  overview of Jepsen approach and tests with quick refresher on results for different databases to date
* [https://github.com/pingcap/tla-plus](https://github.com/pingcap/tla-plus) — formal specification in TLA+ of Raft
  consensus protocol and implementation of distributed transactions in TiDB
* [Testing Cloud-Native Databases with Chaos Mesh](https://youtu.be/FIB1qvLHYsw) — talk on Chaos Mesh and how it is used
  for testing TiDB at PingCap. Blog post
  with [introduction to Chaos Mesh](https://pingcap.com/blog/chaos-mesh-your-chaos-engineering-solution-for-system-resiliency-on-kubernetes)
  and how it integrates with Kubernetes.
  See also Chaos Mesh [source code](https://github.com/chaos-mesh/chaos-mesh)
  and [chaos engineering](#chaos-engineering) section.

See also [formal methods](#formal-methods) section.

### Cloudera

* [Quality Assurance at Cloudera: Fault Injection and Elastic Partitioning](https://web.archive.org/web/20190718225437/https://blog.cloudera.com/blog/2016/04/quality-assurance-at-cloudera-fault-injection-and-elastic-partitioning/)—
  Cloudera describes their approach to fault injection testing
* [Quality Assurance at Cloudera: Highly-Controlled Disk Injection](https://web.archive.org/web/20190701102035/http://blog.cloudera.com/blog/2016/08/quality-assurance-at-cloudera-highly-controlled-disk-injection/)

### Wallaroo Labs

* [Measuring Correctness of State in a Distributed System](https://web.archive.org/web/20220309161005/https://blog.wallaroolabs.com/2017/10/measuring-correctness-of-state-in-a-distributed-system/) —
  describes general idea and implementation how to test safety of distributed stream processing system
* [Performance testing a low-latency stream processing system](https://web.archive.org/web/20220309180234/https://blog.wallaroolabs.com/2018/03/performance-testing-a-low-latency-stream-processing-system/) —
  high level overview of what to look at when testing performance of stream processing system
* [How We Test the Stateful Autoscaling of Our Stream Processing System](https://web.archive.org/web/20220309173229/https://blog.wallaroolabs.com/2018/03/how-we-test-the-stateful-autoscaling-of-our-stream-processing-system/) —
  advanced safety tests for autoscaling stateful stream processing
* All [posts on testing](https://web.archive.org/web/20220309163659/https://blog.wallaroolabs.com/categories/testing/)
  from Walaroo engineering blog

There is also talk from Sean T. Allen on testing stream processing system at Wallaroo Labs (ex. Sendence)

* [Materials on Sean's blog "CodeMeshIO: How Did I Get Here?"](https://www.monkeysnatchbanana.com/2016/11/22/codemeshio-how-did-i-get-here/)
* [Video from QCon NY 2016 on InfoQ](https://www.infoq.com/presentations/trust-distributed-systems)
* [Video from CodeMeshIO on YouTube](https://www.youtube.com/watch?v=6MsPDtpe2tg)
* [Presentation on Speakerdeck](https://speakerdeck.com/seantallen/how-did-i-get-here-building-confidence-in-a-distributed-stream-processor-1)

### YugabyteDB

* [Jepsen Testing on YugabyteDB](https://blog.yugabyte.com/jepsen-testing-on-yugabyte-db-database/) — YugabyteDB
  describes how they use [Jepsen](#jepsen)
* [YugabyteDB 1.1.9 analysis by Kyle Kingsbury](https://jepsen.io/analyses/yugabyte-db-1.1.9) — Kyle explores safety of
  YugabyteDB. Accompanying post in company
  blog ["YugabyteDB 1.2 Passes Jepsen Testing"](https://blog.yugabyte.com/yugabyte-db-1-2-passes-jepsen-testing/)
  and ["Wrapping Up: Jepsen Test Results for YugabyteDB 1.2 Webinar"](https://blog.yugabyte.com/wrapping-up-jepsen-test-results-for-yugabyte-db-1-2-webinar/)
  post with webinar recording by Kyle and Karthik Ranganathan (Yugabyte CTO).
* [YugabyteDB 1.3.1](https://jepsen.io/analyses/yugabyte-db-1.3.1) — Jepsen analysis of YugabyteDB support for
  serializable SQL transactions.
  Companion [blog post](https://blog.yugabyte.com/yugabyte-db-distributed-sql-api-passes-jepsen-tests/) on the company
  website.

### FaunaDB

* [Verifying Transactional Consistency with Jepsen](https://medium.com/fauna/verifying-transactional-consistency-with-jepsen-and-faunadb-561eddd123c7) —
  results of internal [Jepsen](#jepsen) testing at FaunaDB
* [Jepsen: FaunaDB 2.5.4](https://jepsen.io/analyses/faunadb-2.5.4) — official [Jepsen](#jepsen) test for FaunaDB,
  write-up in Fauna [blog](https://fauna.com/blog/faunadbs-official-jepsen-results)

### Shopify

* [Resiliency Testing with Toxiproxy](https://www.usenix.org/conference/lisa17/conference-program/presentation/pittis)
* [Toxiproxy — A TCP proxy to simulate network and system conditions for chaos and resiliency testing](https://github.com/Shopify/toxiproxy)

### Hazelcast

* [Testing the CP Subsystem with Jepsen](https://hazelcast.com/blog/testing-the-cp-subsystem-with-jepsen/) — overview of
  how [Jepsen](#jepsen) is used to test Hazelcast in-memory data grid CP subsystem

### Basho (Riak)

* [Testing Eventual Consistency in Riak](https://www.erlang-factory.com/conference/ErlangUserConference2012/speakers/UlfNorell) —
  how to model eventually consistent database in [QuickCheck](#quickcheck) and find bugs in it`s implementation, video
  available [on YouTube](https://youtu.be/x9mW54GJpG0)
* [Modeling Eventual Consistency Databases with QuickCheck](https://vimeo.com/23220830)— another talk on testing Riak
  eventual consistency guarantees with [QuickCheck](#quickcheck)

### Etcd

* [Testing distributed systems in Go](https://web.archive.org/web/20170224103337/https://coreos.com/blog/testing-distributed-systems-in-go.html) —
  overview of failure injection testing for etcd. Or alternative url
  for [the same post](https://blog.gopheracademy.com/advent-2016/testing-distributed-systems-in-go/).
* [On the Hunt for Etcd Data Inconsistencies](https://youtu.be/IIMs0EjQZHg) — talk on how Etcd reimplemented
  Jepsen in Go using their existing test framework as a cluster runner and
  [Porcupine](#misc) as a linearizability checker

### Red Planet Labs

* [Where we’re going, we don’t need threads: Simulating Distributed Systems](https://tech.redplanetlabs.com/2021/03/17/where-were-going-we-dont-need-threads-simulating-distributed-systems/) —
  following [FoundationDB](#foundationdb) steps, Red Planet Labs uses deterministic simulation for testing. Their
  formula for success is "deterministic simulation = no parallelism + quantized execution + deterministic behavior".

See also [deterministic simulation](#deterministic-simulation) section.

### Atomix Copycat

* [A novel implementation of the Raft consensus algorithm](https://github.com/atomix/copycat)
* [Jepsen tests for Atomix Copycat](https://github.com/atomix/atomix-jepsen)

### Druid.io

* [Architecting Distributed Databases for Failure](https://www.infoq.com/presentations/data-integrity-distributed-systems)

### TigerBeetle

* [Simulation Tests in TigerBeetle](https://github.com/tigerbeetledb/tigerbeetle/blob/main/docs/HACKING.md#simulation-tests) —
  TigerBeetle is a distributed financial accounting database built in Zig programming language and uses simulation tests
  inspired by [Dropbox](#dropbox) and [FoundationDB](#foundationdb).

See also [deterministic simulation](#deterministic-simulation) section.

### Convex

* [Convex: Life Without a Backend Team](https://youtu.be/iizcidmSwJ4)
  by [James Cowling](https://twitter.com/jamesacowling) —
  talks about architecture and features of [Convex](https://www.convex.dev/).
  At the [end of the talk](https://youtu.be/iizcidmSwJ4?t=2788) James covers testing at Convex.
  They use approach inspired by [QuickCheck](#quickcheck) and [FoundationDB](#foundationdb) to test end-to-end
  guarantees with randomized initial state, workload, injected failures and thread interleaving. These tests validate
  correctness in production similar to [Dropbox](#dropbox) Magic Pocket system on which James worked previously.
* [Better Testing With Less Code Using Randomization](https://blog.convex.dev/randomized-testing/) — blog post
  describing approach Convex uses to develop randomized tests

See also [QuickCheck](#quickcheck), [FoundationDB](#foundationdb), [Dropbox](#dropbox), [Jepsen](#jepsen),
[deterministic simulation](#deterministic-simulation).

### RisingWave

In a series of two blog posts, RisingWave team talks about their experience using deterministic simulation for testing
distributed SQL-based stream processing platform:

* [Deterministic Simulation: A New Era of Distributed System Testing](https://www.risingwave.com/blog/deterministic-simulation-a-new-era-of-distributed-system-testing)
* [Applying Deterministic Simulation: The RisingWave Story](https://www.risingwave.com/blog/applying-deterministic-simulation-the-risingwave-story-part-2-of-2)
  They talk about few kinds of tests they built with the simulator (unit, end-to-end, recovery, scaling), pros, cons and
  challenges of this approach.

As a result of this work, they open sourced [MadSim](https://github.com/madsim-rs/madsim) — Magical Deterministic
Simulator for the Rust language ecosystem.

See also [deterministic simulation](#deterministic-simulation) section.

### YDB

* [Hardening YDB with Jepsen: Lessons Learned](https://blog.ydb.tech/hardening-ydb-with-jepsen-lessons-learned-e3238a7ef4f2) —
  how [Jepsen](#jepsen) tests for YDB helped find consistency and other bugs in YDB
* [jepsen.ydb](https://github.com/ydb-platform/jepsen.ydb) — code of Jepsen tests for YDB

See also [Jepsen](#jepsen).

## Single Node Systems

These examples are not about distributed systems, but they demonstrate testing concurrency and level of sophistication
required in distributed systems.

### Concurrency

Testing concurrent code is one of the challenges in single node as well as distributed systems. These tools help to
test both lock based and lock-free concurrent code on various platforms.

#### JCStress

* [JCStress](https://openjdk.org/projects/code-tools/jcstress/) — test harness to verify correctness of concurrency
  support in the JVM, class libraries, and hardware.
* [Workshop: Java Concurrency Stress (JCStress). Part 1](https://youtu.be/koU38cczBy8)
  and [Part 2](https://youtu.be/iTZNhknTGrg) by Aleksey Shipilëv
* [JCStress samples](https://github.com/openjdk/jcstress/tree/master/jcstress-samples/src/main/java/org/openjdk/jcstress/samples)
  showcasing what could be verified with the harness
* [Java Concurrency Stress Tests](https://shipilev.net/#jcstress) presentations by Aleksey Shipilëv on JCStress

#### LinCheck

* [LinCheck](https://github.com/JetBrains/lincheck) — framework for testing concurrent data structures on JVM
* [How We Test Concurrent Primitives in Kotlin Coroutines](https://blog.jetbrains.com/kotlin/2021/02/how-we-test-concurrent-primitives-in-kotlin-coroutines/)
  from JetBrains blog
* [Lin-Check: Testing concurrent data structures in Java](https://youtu.be/hwbpUEGHvvY) talk by Nikita Koval
* [Workshop. Lincheck: Testing concurrency on the JVM (Part 1](https://youtu.be/YNtUK9GK4pA)
  and [Part 2](https://youtu.be/EW7mkAOErWw) by Maria Sokolova

#### Other

* [ThreadSanitizer](https://clang.llvm.org/docs/ThreadSanitizer.html) — data race detection tool for C++
* ThreadSanitizer is used under the hood of the [Go language race detector](https://go.dev/doc/articles/race_detector)

### SQLite

SQLite is not a distributed system by any stretch of the imagination, but provides good example of comprehensive testing
of a database implementation.

* [Finding bugs in SQLite, the easy way](https://lcamtuf.blogspot.ru/2015/04/finding-bugs-in-sqlite-easy-way.html)— how
  fuzzing used in testing SQLite database
* [How SQLite Is Tested](https://www.sqlite.org/testing.html)

### Sled

* [Sled simulation guide (jepsen-proof engineering)](https://sled.rs/simulation) — guide on simulation testing (
  see [FoundationDB](#foundationdb)) in Sled database
* [Reliable Systems Series: Model-Based Testing](https://medium.com/@tylerneely/reliable-systems-series-model-based-property-testing-e89a433b360)

See also [deterministic simulation](#deterministic-simulation) section.

### Clickhouse

* [Fuzzing ClickHouse](https://clickhouse.com/blog/fuzzing-click-house) — high level overview of
  query [fuzzing](#fuzzing) at Clickhouse
* [ClickHouse Testing](https://clickhouse.com/docs/en/development/tests/) — documentation on various tests for
  ClickHouse database
  and how to contribute more tests

## Tools

* [Hermitage: Testing transaction isolation levels](https://github.com/ept/hermitage)
* [RapidCheck — QuickCheck port to C++](https://github.com/emil-e/rapidcheck)
* [faketime](https://manpages.ubuntu.com/manpages/trusty/man1/faketime.1.html)

### Network Simulation

* [Comcast — Simulating shitty network connections, so you can build better systems](https://github.com/tylertreat/comcast)
* [Muxy Simulating real-world distributed system failures](https://github.com/mefellows/muxy)
* [Namazu — Programmable fuzzy scheduler for testing distributed systems](https://github.com/osrg/namazu)
* [Toxiproxy — A TCP proxy to simulate network and system conditions for chaos and resiliency testing](https://github.com/Shopify/toxiproxy)
* [Traffic Control](https://www.funtoo.org/Traffic_Control)
* [Python API for Linux Traffic Control](https://github.com/praus/shapy)
* [Slow tool](https://github.com/ModusCreateOrg/slow/)
* [Blockade is a utility for testing network failures and partitions in distributed applications](https://github.com/dcm-oss/blockade)
* [DEMi: Distributed Execution Minimizer for Akka](https://github.com/NetSys/demi)
* [Chaos Mesh](https://chaos-mesh.org/) — [chaos engineering](#chaos-engineering) platform for Kubernetes. See
  also [PingCap](#pingcap-tidb), company behind Chaos Mesh.

### QuickCheck

* [PolyConf 14: Testing the Hard Stuff and Staying Sane / John Hughes](https://youtu.be/F6LzB6SdFKA)
* [The Joy of Testing](https://www.infoq.com/presentations/The-Joy-of-Testing)
* [John Hughes on InfoQ](https://www.infoq.com/author/John-Hughes)
* [Hansei: Property-based Development of Concurrent Systems](https://speakerdeck.com/jtuple/hansei-property-based-development-of-concurrent-systems)
* [QuickChecking Poolboy for Fun and Profit](https://web.archive.org/web/20230325231321/https://riak.com/posts/technical/quickchecking-poolboy-for-fun-and-profit/)—
  from Basho
* [Combining Fault-Injection with Property-Based Testing](https://dl.acm.org/doi/10.1145/2559627.2559629)
* [Testing Telecoms Software with Quviq QuickCheck](https://web.archive.org/web/20120325030155id_/http://www.quviq.com/documents/erlang001-arts.pdf)
* [Fuzz testing distributed systems with QuickCheck](https://making.pusher.com/fuzz-testing-distributed-systems-with-quickcheck/index.html) —
  using QuickCheck to test Raft protocol implementation in Haskell

### Benchmarking

* [OLTP-Bench: An Extensible Testbed for Benchmarking Relational Databases](https://www.vldb.org/pvldb/vol7/p277-difallah.pdf)
* [OLTP Benchmark on GitHub](https://github.com/oltpbenchmark)
* [Py-TPCC](https://github.com/apavlo/py-tpcc)
* [Netflix Data Benchmark: Benchmarking Cloud Data Stores](https://netflixtechblog.com/netflix-data-benchmark-benchmarking-cloud-data-stores-7266186ded11)

### Linkbench

* [LinkBench from Facebook](https://www.facebook.com/notes/facebook-engineering/linkbench-a-database-benchmark-for-the-social-graph/10151391496443920)
  and [Github.com repo](https://github.com/facebookarchive/linkbench)
* [LinkBenchX from Percona](https://www.percona.com/blog/2015/05/01/linkbenchx-benchmark-based-arrival-request-rate/)

### YCSB

* [Yahoo! Cloud System Benchmark (YCSB)](https://github.com/brianfrankcooper/YCSB)
* [YCSB+T: Benchmarking Web-scale Transactional Databases](https://www.researchgate.net/publication/269306582_YCSBT_Benchmarking_web-scale_transactional_databases)
* [YCSB++](https://www.pdl.cmu.edu/ycsb++/)
* [Correcting YCSB's Coordinated Omission problem](https://psy-lob-saw.blogspot.ru/2015/03/fixing-ycsb-coordinated-omission.html)

