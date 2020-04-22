List of resources on testing distributed systems curated by Andrey Satarin ([@asatarin](https://twitter.com/asatarin)).

**Contents**
- [Overview of testing approaches](#overview-of-testing-approaches)
  - [Research Papers](#research-papers)
  - [Resilience In Complex Adaptive Systems](#resilience-in-complex-adaptive-systems)
  - [Jepsen](#jepsen)
  - [Formal Methods](#formal-methods)
  - [Lineage-driven Fault Injection](#lineage-driven-fault-injection)
  - [Chaos Engineering](#chaos-engineering)
  - [Fuzzing](#fuzzing)
  - [Game Days](#game-days)
  - [Performance and Benchmarking](#performance-and-benchmarking)
  - [Test Case Reduction](#test-case-reduction)
  - [Misc](#misc)
- [Specific approaches in different distributed systems](#specific-approaches-in-different-distributed-systems) 
  - [Amazon Web Services](#amazon-web-services)
  - [Netflix](#netflix)
  - [Twitter](#twitter)
  - [Datastax (Cassandra)](#datastax-cassandra)
  - [ScyllaDB](#scylladb)
  - [VoltDB](#voltdb)
  - [MemSQL](#memsql)
  - [CockroachLabs (CockroachDB)](#cockroachlabs-cockroachdb)
  - [PingCap (TiDB)](#pingcap-tidb)
  - [MongoDB](#mongodb)
  - [Cloudera](#cloudera)
  - [FoundationDB](#foundationdb)
  - [Wallaroo Labs](#wallaroo-labs)
  - [Google](#google)
  - [Microsoft](#microsoft)
  - [Dropbox](#dropbox)
  - [Atomix Copycat](#atomix-copycat)
  - [Onyx](#onyx)
  - [LinkedIn](#linkedin)
  - [Druid.io](#druidio)
  - [Salesforce](#salesforce)
  - [SQLite](#sqlite)
  - [InfluxDB](#influxdb)
  - [Shopify](#shopify)
  - [Confluent (Kafka)](#confluent-kafka)
  - [Elastic (Elastic Search)](#elastic-elastic-search)
  - [YugaByte DB](#yugabyte-db)
  - [FaunaDB](#faunadb)
  - [Hazelcast](#hazelcast)
  - [Basho (Riak)](#basho-riak)
  - [CoreOS (etcd)](#coreos-etcd)
- [Tools](#tools)
  - [Network Simulation](#network-simulation)
  - [QuickCheck](#quickcheck)
  - [Benchmarking](#benchmarking)
  - [Linkbench](#linkbench)
  - [YCSB](#ycsb)

## Overview of testing approaches

### Research Papers
* [Simple Testing Can Prevent Most Critical Failures: An Analysis of Production Failures in Distributed Data-Intensive Systems](https://www.usenix.org/conference/osdi14/technical-sessions/presentation/yuan) — Great overview of how even simple testing can help a lot, you just need right focus
* [What Bugs Live in the Cloud? A Study of 3000+ Issues in Cloud Systems](http://ucare.cs.uchicago.edu/pdf/socc14-cbs.pdf) — study of actual bugs in different popular distributed systems (Hadoop MapReduce, HDFS, HBase, Cassandra, ZooKeeper
and Flume)
* [TaxDC: A Taxonomy of Non-Deterministic Concurrency Bugs in Datacenter Distributed Systems](http://ucare.cs.uchicago.edu/pdf/asplos16-TaxDC.pdf) — comprehensive taxonomy of bugs in distributed systems (Cassandra, Hadoop MapReduce, HBase, ZooKeeper)
* [An Empirical Study on Crash Recovery Bugs in Large-Scale Distributed Systems](http://www.tcse.cn/~gaoyu15/paper/2018-fse-creb.pdf) — based on bug database from "What Bugs Live in the Cloud?" paper reseachers focus specifically on crash recovery bugs in Hadoop MapReduce, HBase, Cassandra, ZooKeeper. There is review of this paper by [Murat Demirbas](https://twitter.com/muratdemirbas) in [his blog](http://muratbuffalo.blogspot.com/2019/01/paper-review-empirical-study-on-crash.html).
* [Redundancy does not imply fault tolerance: analysis of distributed storage reactions to single errors and corruptions](https://blog.acolyer.org/2017/03/08/redundancy-does-not-imply-fault-tolerance-analysis-of-distributed-storage-reactions-to-single-errors-and-corruptions/) — study of several distributed systems (Redis, ZooKeeper, MongoDB, Cassandra, Kafka, RethinkDB) on how fault tolerant they are to data corruption and read/write errors
* [An empirical study on the correctness of formally verified distributed systems](https://blog.acolyer.org/2017/05/29/an-empirical-study-on-the-correctness-of-formally-verified-distributed-systems/) — study of bugs in formally verified distributed systems
* [The Case for Limping-Hardware Tolerant Clouds](https://www.usenix.org/node/174577) — research on effect of limping hardware on performance of a distributed systems (aka limplock), see also great blog post by Dan Luu on a similiar topic [Distributed systems: when limping hardware is worse than dead hardware](https://danluu.com/limplock/)
* [Early detection of configuration errors to reduce failure damage](https://blog.acolyer.org/2016/11/29/early-detection-of-configuration-errors-to-reduce-failure-damage/) — why and how to test configuration files of your system
* [Why Is Random Testing Effective for Partition Tolerance Bugs?](https://dl.acm.org/doi/abs/10.1145/3158134) — just what it says in a title, authors try to explain why random testing ([Jepsen](#jepsen)) is effective and introduce notions of test coverage relating to network partition, see also ["The Morning Paper" review](https://blog.acolyer.org/2018/01/23/why-is-random-testing-effective-for-partition-tolerance-bugs/)
* [FlyMC: Highly Scalable Testing of Complex Interleavings in Distributed Systems](https://ucare.cs.uchicago.edu/pdf/eurosys19-flyMC.pdf) — novel approach of systematically exploring interleavings in distributed systems augmented with static analysis and prioritization. This approach is faster than previous techniques and found old and new bugs in several systems (Cassandra, Ethereum Blockchain, Hadoop, Kudu, Raft LogCabin, Spark, ZooKeeper).
* [What bugs cause cloud production incidents?](https://blog.acolyer.org/2019/06/21/what-bugs-cause-cloud-production-incidents/) — research focused on bugs (and their resolution strategies) that actually cause production incidents in large-scale distributed services at [Microsoft](#microsoft) Azure.
* [Torturing Databases for Fun and Profit](https://www.usenix.org/system/files/conference/osdi14/osdi14-paper-zheng_mai.pdf) — checking ACID guarantees of open source and commercial databases under power loss, [additional material](https://www.usenix.org/node/186197)


#### Technologies for Testing Distributed Systems by Colin Scott
Colin Scott shares his viewpoint from academia on testing distributed systems,
specifically regression testing for correctness and performance bugs.
* [Technologies for Testing Distributed Systems, Part I](http://colin-scott.github.io/blog/2016/03/04/technologies-for-testing-and-debugging-distributed-systems/)
* See also post [Distributed Systems Testing: The Lost World](http://tagide.com/blog/research/distributed-systems-testing-the-lost-world/) by Crista Lopes

#### Testing in a Distributed World by Ines Sombra (RICON 2014)
Great overview of techniques for testing distributed systems from practitioner, the [video](https://youtu.be/iZEXIN7-9tM) did age well and still extremely good overview of the landscape.
Additional materials could be found in [this Github repo](https://github.com/Randommood/RICON2014)


### Resilience In Complex Adaptive Systems
These materials are not directly related to testing distributed systems, but they greatly contribute to general understanding of such systems.

* [Velocity NY 2013: Richard Cook, "Resilience In Complex Adaptive Systems"](https://youtu.be/PGLYEDpNu60)
* [Velocity 2012: Richard Cook, "How Complex Systems Fail"](https://youtu.be/2S0k12uZR14)
* [How Complex Systems Fail](http://web.mit.edu/2.75/resources/random/How%20Complex%20Systems%20Fail.pdf)


### Jepsen
State of the art approach to testing stateful distributed  systems.

* [Jepsen Analyses](http://jepsen.io/analyses) — most recent Jepsen analyses of different distributed systems
* [Jepsen Talks](http://jepsen.io/talks) — talks by Kyle Kingsbury on various conferences
* [Aphyr's Jepsen posts](https://aphyr.com/tags/Jepsen) — older Jepsen analyses on Kyle Kingsbury's (Aphyr) personal site
* [Jepsen Talks on Github](https://github.com/aphyr/jepsen-talks) — Jepsen talks slides before 2015 on Github
* [Kyle Kingsbury on InfoQ](http://www.infoq.com/author/Kyle-Kingsbury)
* [Call me maybe: Jepsen and flaky networks](http://www.slideshare.net/shalinmangar/call-me-maybe-jepsen-and-flaky-networks) — talk on Jepsen, not by Kyle
* [Jepsen is used by Microsoft CosmosDB](https://twitter.com/dharmashukla/status/869104163510034432) — founder of Azure CosmosDB confirms, that they are using Jepsen

Some notable Jepsen analyses:
* [Jepsen: CockroachDB beta-20160829](https://jepsen.io/analyses/cockroachdb-beta-20160829)
* [Jepsen: VoltDB 6.3](http://jepsen.io/analyses/voltdb-6-3)
* [Jepsen: RethinkDB 2.2.3 reconfiguration](https://aphyr.com/posts/330-jepsen-rethinkdb-2-2-3-reconfiguration)
* [Jepsen: RethinkDB 2.1.5](https://aphyr.com/posts/329-jepsen-rethinkdb-2-1-5)

Jepsen is used by [CockroachDB](#cockroachlabs-cockroachdb), [VoltDB](#voltdb), [Cassandra](#datastax-cassandra), [ScyllaDB](#scylladb) and others.


### Formal Methods
* [The verification of a distributed system By Caitie McCaffrey](http://queue.acm.org/detail.cfm?id=2889274) also [podcast](https://www.infoq.com/articles/podcast-caitie-mccaffrey) and [talk](https://www.infoq.com/presentations/distributed-systems-verification) on InfoQ.com and [accompanying materials](https://github.com/CaitieM20/Talks/tree/master/TheVerificationOfADistributedSystem) on GitHub and a [slidedeck](https://speakerdeck.com/caitiem20/qcon-newyork-2016-the-verification-of-a-distributed-system)
* [Designing Distributed Systems in TLA+](https://www.hillelwayne.com/talks/distributed-systems-tlaplus/) by Hillel Wayne, and talk [Everything about distributed systems is terrible](https://youtu.be/tfnldxWlOhM)
* [Comparisons of Alloy and Spin](http://www2.research.att.com/~pamela/model.html)
* [Verdi: Formally Verifying Distributed Systems](http://verdi.uwplse.org/)
* [Verdi — A framework for formally verifying distributed systems implementations in Coq](https://github.com/uwplse/verdi)
* [Network Semantics for Verifying Distributed Systems](https://homes.cs.washington.edu/~jrw12/network-semantics.html)
* [Proving that Android’s, Java’s and Python’s sorting algorithm is broken (and showing how to fix it)](http://envisage-project.eu/proving-android-java-and-python-sorting-algorithm-is-broken-and-how-to-fix-it/) — using formal verification to find a bug in TimSort sorting algorithm
* [Proving JDK’s Dual Pivot Quicksort Correct](https://www.key-project.org/2017/08/17/dual-pivot/) — analizying quicksort implementation in Java 

Companies using TLA+ to verify correctness of algorithms:
 * [Amazon Web Services](#amazon-web-services)
 * [PingCap for TiDB](#pingcap-tidb)
 * [MongoDB](#mongodb)
 * [Microsoft](#microsoft) for services in Azure cloud
 * [Confluent](#confluent-kafka) for Apache Kafka


### Lineage-driven Fault Injection
* [Lineage-driven Fault Injection](https://dl.acm.org/citation.cfm?id=2723711)
* [Abstracting the Geniuses Away from Failure Testing](http://queue.acm.org/detail.cfm?id=3155114)

[Netflix](#netflix) adopted lineage-driven fault injection techniques for testing microservices.


### Chaos Engineering
* [Principles of Chaos Engineering](http://principlesofchaos.org/)
* Free [Chaos Engineering](http://www.oreilly.com/webops-perf/free/chaos-engineering.csp) book by [Netflix](#netflix) engineers
* [A curated list of awesome Chaos Engineering resources](https://github.com/dastergon/awesome-chaos-engineering)

[Netflix](#netflix) pioneered chaos engineering discipline.


### Fuzzing
There are two flavors of fuzzing. First, randomized concurrency testing, where the ordering of messages is fuzzed:
* [Fuzzing Raft for Fun and Publication](https://colin-scott.github.io/blog/2015/10/07/fuzzing-raft-for-fun-and-profit/)
* [Combining AFL and QuickCheck for Directed Fuzzing by Dan Luu](http://danluu.com/testing/)

And input fuzzing, where message contents or user inputs are fuzzed:
* [DNS parser, meet Go fuzzer](https://blog.cloudflare.com/dns-parser-meet-go-fuzzer/)
* [Fuzz Testing with afl-fuzz (American Fuzzy Loop)](http://spin.atomicobject.com/2015/08/23/fuzz-testing-american-fuzzy-lop/)
* [Randomized testing for Go](https://github.com/dvyukov/go-fuzz) and talk on this tool [GopherCon 2015: Dmitry Vyukov — Go Dynamic Tools](https://www.youtube.com/watch?v=a9xrxRsIbSU)
* [Simple guided fuzzing for libraries using LLVM's new libFuzzer](http://blog.llvm.org/2015/04/fuzz-all-clangs.html)
* [LibFuzzer – a library for coverage-guided fuzz testing](http://llvm.org/docs/LibFuzzer.html)
* [How Heartbleed could've been found](https://blog.hboeck.de/archives/868-How-Heartbleed-couldve-been-found.html) — example of how fuzzing could be used for finding famous HeartBleed vulnerability


### Game Days
* [Game Day Exercises at Stripe: Learning from kill -9](https://stripe.com/blog/game-day-exercises-at-stripe)
* [Sometimes Kill -9 Isn’t Enough](http://bravenewgeek.com/sometimes-kill-9-isnt-enough/)


### Performance and Benchmarking
* [Your Load Generator Is Probably Lying To You](http://highscalability.com/blog/2015/10/5/your-load-generator-is-probably-lying-to-you-take-the-red-pi.html)
* [Everything You Know About Latency Is Wrong](http://bravenewgeek.com/everything-you-know-about-latency-is-wrong/) — great overview of Gil Tene`s "How NOT to Measure Latency" talk
* ["How NOT to Measure Latency" by Gil Tene](https://www.youtube.com/watch?v=lJ8ydIuPFeU)
* ["Benchmarking: You're Doing It Wrong" by Aysylu Greenberg](https://www.youtube.com/watch?v=XmImGiVuJno)
* [Performance Analysis Methodology](http://www.brendangregg.com/methodology.html) — approaches developed by Brendan Gregg for analysing performance in systematic fashion

See also [benchmarking](#benchmarking) tools.


### Test Case Reduction
* [Minimizing Faulty Executions of Distributed Systems](https://people.eecs.berkeley.edu/~rcs/research/nsdi16.pdf) — reducing the size of buggy executions to make them easier to understand. 60 minute talk [here](https://www.microsoft.com/en-us/research/video/minimizing-faulty-executions-distributed-systems/)
* [Troubleshooting Blackbox SDN Control Software with Minimal Causal Sequences](https://people.eecs.berkeley.edu/~rcs/research/sts.pdf) — similar to above, but requires less instrumentation.
* [Concurrency Debugging with Differential Schedule Projections](https://brandonlucia.com/pubs/symbiosis_final_pldi.pdf) — find and minimize concurrency bugs using program analysis. Shared memory systems are equivalent to message passing systems, so you can apply the same techniques to distributed systems.


### Misc
* ["Simulation Testing" by Michael Nygard](https://youtu.be/N5HyVUPuU0E)
* [Testing Distributed Systems for Linearizability](http://www.anishathalye.com/2017/06/04/testing-distributed-systems-for-linearizability/)


## Specific approaches in different distributed systems

### Amazon Web Services
* [The Evolution of Testing Methodology at AWS: From Status Quo to Formal Methods with TLA+](http://www.infoq.com/presentations/aws-testing-tla)
* [Use of Formal Methods at Amazon Web Services](http://research.microsoft.com/en-us/um/people/lamport/tla/formal-methods-amazon.pdf)
* [CACM Article "How Amazon Web Services Uses Formal Methods"](http://cacm.acm.org/magazines/2015/4/184701-how-amazon-web-services-uses-formal-methods/fulltext)
* [Experience of software engineers using TLA+, PlusCal and TLC](http://tla2012.loria.fr/contributed/newcombe-slides.pdf)
* [Debugging Designs by Chris Newcombie](http://www.hpts.ws/papers/2011/sessions_2011/Debugging.pdf) there is also a  [source bundle](http://www.hpts.ws/papers/2011/sessions_2011/amazonbundle.tar.gz)
* [Millions of tiny databases](https://blog.acolyer.org/2020/03/04/millions-of-tiny-databases/) — has section on testing which describes several approaches: SimWorld simulation resembling approach used at [Foundation DB](#foundationdb), use of [Jepsen](#jepsen) and [formal methods](#formal-methods) and [game days](#game-days).

See also [formal methods](#formal-methods) section.


### Netflix 
Automated failure injection (see also [Lineage-driven Fault Injection](#lineage-driven-fault-injection)):
* [Monkeys in Lab Coats: Applying Failure Testing Research @Netflix](http://www.infoq.com/presentations/failure-test-research-netflix)
* [“Monkeys in Labs Coats”: Applied Failure Testing Research at Netflix](http://www.infoq.com/news/2016/03/failure-testing-netflix)
* [Automated Failure Testing](http://techblog.netflix.com/2016/01/automated-failure-testing.html)
* [Automating Failure Testing Research at Internet Scale](https://scholar.google.ru/scholar?hl=en&q=Automating+Failure+Testing+Research+at+Internet+Scale&btnG=&as_sdt=1%2C5&as_sdtp=) by P. Alvaro et.el

Random/manual failure injection testing: 
* [Netflix Simian Army](http://techblog.netflix.com/2011/07/netflix-simian-army.html)
* [Failure Injection Testing](http://techblog.netflix.com/2014/10/fit-failure-injection-testing.html)
* [From Chaos to Control — Testing the resiliency of Netflix’s Content Discovery Platform](http://techblog.netflix.com/2015/08/from-chaos-to-control-testing.html)
* [Breaking Bad at Netflix: Building Failure as a Service](http://www.infoq.com/presentations/failure-as-a-service-netflix)
* [GTAC 2014: I Don't Test Often ... But When I Do, I Test in Production](https://www.youtube.com/watch?v=xkP70Zhhix4) — Netflix different testing strategies

See also [Chaos Engineering](#chaos-engineering).


### Twitter 
* [Diffy: Testing services without writing tests](https://blog.twitter.com/2015/diffy-testing-services-without-writing-tests)
* [How we break things at Twitter: failure testing](https://blog.twitter.com/2015/how-we-break-things-at-twitter-failure-testing)


### Datastax (Cassandra) 
* [Testing Apache Cassandra with Jepsen](http://www.datastax.com/dev/blog/testing-apache-cassandra-with-jepsen)
* [Testing Cassandra Guarantees under Diverse Failure Modes with Jepsen](http://www.slideshare.net/jkni/testing-cassandra-guarantees-under-diverse-failure-modes-with-jepsen-53168992)
* [Testing Cassandra Guarantees under Diverse Failure Modes with Jepsen](http://cassandrasummit-datastax.com/agenda/testing-cassandra-guarantees-under-diverse-failure-modes-with-jepsen/)
* [Jepsen Cassandra Testing on Git](https://github.com/riptano/jepsen)
* [Netflix A STATE OF XEN — CHAOS MONKEY & CASSANDRA](https://vimeopro.com/user35188327/cassandra-summit-2015/video/140949186) from Cassandra Summit 2015
* [Testing Apache Cassandra with Jepsen: How to Understand and Produce Safe Distributed Systems](https://youtu.be/OnG1FCr5WTI) by Joel Knighton presented at Devoxx UK 2016
* [Testing Apache Cassandra 4.0](https://cassandra.apache.org/blog/2018/08/21/testing_apache_cassandra.html) — quick overview of approaches used to test next major version of Cassandra
* [Fallout](https://github.com/datastax/fallout) — tool to run distributed tests as a service. It is meant to easily orchestrate cluster creation and testing tools like [Jepsen](#jepsen), performance testing tools and others, though extention and combining them in various ways with enviromental conditions. It could run tests either locally or on large scale clusters.


### ScyllaDB
They published series of blog posts on testing ScyllaDB:
* [Scylla testing part 1: Cassandra compatibility testing](http://www.scylladb.com/2016/02/04/cassandra-compatibility-testing/)
* [Scylla testing part 2: Extending Jepsen for testing Scylla](http://www.scylladb.com/2016/02/11/jepsen-testing/)
* [CharybdeFS: a new fault-injecting filesystem for software testing](http://www.scylladb.com/2016/02/16/fault-injection-filesystem-software-testing/)
* [Testing part 4: Distributed tests](http://www.scylladb.com/2016/03/10/dtest-scylla/)
* [Testing part 5: Longevity testing](http://www.scylladb.com/2016/03/15/longevity-testing-scylla/)
* [Fault-injecting filesystem cookbook](http://www.scylladb.com/2016/05/02/fault-injection-filesystem-cookbook/)
Video from Scylla Summit 2017 on testing
* [How We Constantly Try to Bring Scylla to its Knees](https://youtu.be/K38RDEdt070) and [slides](https://www.slideshare.net/ScyllaDB/scylla-summit-2017-cry-in-the-dojo-laugh-in-the-battlefield-how-we-constantly-try-to-bring-scylla-to-its-knees) — overview of different testing types at ScyllaDB
* [Project Gemini: An Open Source Automated Random Testing Suite for Scylla and Cassandra Clusters](https://www.scylladb.com/2019/12/11/project-gemini-an-open-source-automated-random-testing-suite-for-scylla-and-cassandra-clusters/) — random test generator comparing results from cluster with injected faults against single node running without faults. Works on tops of CQL API and suitable for testing any database implementing it. See also talk on [Project Gemini](https://youtu.be/QPnlpglmPcY) and [open source code](https://github.com/scylladb/gemini)


### VoltDB 
Series of post on testing at VoltDB:
* [How We Test at VoltDB](https://www.voltdb.com/blog/2015/09/30/how-we-test-at-voltdb/)
* [Testing at VoltDB: SQLCoverage](https://www.voltdb.com/blog/2016/03/30/testing-voltdb-sqlcoverage/) — describes how they test SQL query functionality using 5 millions queries generated from templates and comparing results against HSQLDB
* [Testing VoltDB Against PostgreSQL](https://www.voltdb.com/blog/2016/04/11/testing-voltdb-postgresql/)
* [VoltDB 6.4 Passes Official Jepsen Testing](https://www.voltdb.com/blog/2016/07/12/voltdb-6-4-passes-official-jepsen-testing/) — VoltDB hired Kyle Kingsbury ([Jepsen](#jepsen)) to tests their database, they share results in this post

Additional resources:
* ["All In With Determinism for Performance and Testing in Distributed Systems" by John Hugg](https://www.youtube.com/watch?v=gJRj3vJL4wE) and a slide deck [Hugg-DeterministicDistributedSystems.pdf](https://github.com/strangeloop/StrangeLoop2015/blob/master/slides/talks/Hugg-DeterministicDistributedSystems.pdf)
* [SelfCheck workload](https://github.com/VoltDB/voltdb/tree/master/tests/test_apps/txnid-selfcheck2)
* [TPC-C implementation](https://github.com/VoltDB/voltdb/tree/master/tests/test_apps/tpcc)


### MemSQL 
* [Running MemSQL’s 107 Node Test Infrastructure on CoreOS](http://blog.memsql.com/running-memsqls-107-node-test-infrastructure-on-coreos/)
* [Practical Techniques to Achieve Quality in Large Software Projects](http://blog.memsql.com/practical-techniques-to-achieve-quality-in-large-software-projects-3/)
* [How to Make a Believable Benchmark](http://blog.memsql.com/how-to-make-a-believable-benchmark/)
* [Building an Infinitely Scalable Testing System](http://blog.memsql.com/building-an-infinitely-scalable-testing-system/) — description of internal test system PsyDuck


### CockroachLabs (CockroachDB)
* [DIY Jepsen Testing CockroachDB](https://www.cockroachlabs.com/blog/diy-jepsen-testing-cockroachdb/) — great read about using Jepsen at Cockroach Labs
* [CockroachDB Beta Passes Jepsen Testing](https://www.cockroachlabs.com/blog/cockroachdb-beta-passes-jepsen-testing/) — CockroachDB tested by Kyle Kingsbury (Jepsen.io)


### PingCap (TiDB)
* [Use Chaos to test the distributed system linearizability](https://medium.com/@siddontang/use-chaos-to-test-the-distributed-system-linearizability-4e0e778dfc7d) — describes Jepsen-like framework implemented in Go and used at PingCap to test TiDB
* [A test framework for linearizability check with Go](https://github.com/siddontang/chaos) — Chaos is a Jepsen-like framework written in Go
* [Testing Distributed Systems for Linearizability](http://www.anishathalye.com/2017/06/04/testing-distributed-systems-for-linearizability/) — linearizability testing library used by Chaos framework
* [Chaos Tools and Techniques for Testing the TiDB Distributed NewSQL Database](https://thenewstack.io/chaos-tools-and-techniques-for-testing-the-tidb-distributed-newsql-database/) and the same post on company [blog](https://pingcap.com/blog/chaos-practice-in-tidb/) 
* [Official Jepsen report on TiDB 2.1.7](https://jepsen.io/analyses/tidb-2.1.7) and [companion blog post](https://pingcap.com/blog/tidb-passes-jepsen-test-for-snapshot-isolation-and-single-key-linearizability/) in company blog
* [Safety First! Common Safety Pitfalls in Distributed Databases Found by Jepsen Tests](https://pingcap.com/blog/safety-first-common-safety-pitfalls-in-distributed-databases-found-by-jepsen-tests/) — overview of Jepsen approach and tests with quick refresher on results for different databases to date
* [https://github.com/pingcap/tla-plus](https://github.com/pingcap/tla-plus) — formal specification in TLA+ of Raft consensus protocol and implementation of distributed transactions in TiDB

See also [formal methods](#formal-methods) section.


### MongoDB
* [MongoDB’s JavaScript Fuzzer: Creating Chaos (1/2)](https://engineering.mongodb.com/post/mongodbs-javascript-fuzzer-creating-chaos/)
* [MongoDB’s JavaScript Fuzzer: Harnessing the Havoc (2/2)](https://engineering.mongodb.com/post/mongodbs-javascript-fuzzer-harnessing-havoc/)
* [Fixing a MongoDB Replication Protocol Bug with TLA+](https://youtu.be/x9zSynTfLDE) by William Schultz — how MongoDB uses [formal verification](#formal-methods) with TLA+ to check correctness of their replication protocol. Describes how replication bugs could have been found with help of formal model.
* [Change Point Detection in Software Performance Testing](https://arxiv.org/abs/2003.00584) — paper on how MongoDB team automatically detects performance degradations in the presence of noise in continuous integration runs. The paper was presented at [ICPE 2020](https://youtu.be/rSBgcMFPkHU) 

See also [formal methods](#formal-methods) section.


### Cloudera
* [Quality Assurance at Cloudera: Fault Injection and Elastic Partitioning](http://blog.cloudera.com/blog/2016/04/quality-assurance-at-cloudera-fault-injection-and-elastic-partitioning/) — Cloudera describes their approach to fault injection testing
* [Quality Assurance at Cloudera: Highly-Controlled Disk Injection](http://blog.cloudera.com/blog/2016/08/quality-assurance-at-cloudera-highly-controlled-disk-injection/)


### FoundationDB 
* ["Testing Distributed Systems w/ Deterministic Simulation" by Will Wilson](https://www.youtube.com/watch?v=4fFDFbi3toc&feature=youtu.be)


### Wallaroo Labs

* [Measuring Correctness of State in a Distributed System](https://blog.wallaroolabs.com/2017/10/measuring-correctness-of-state-in-a-distributed-system/) — describes general idea and implementation how to test safety of distributed stream processing system 
* [Performance testing a low-latency stream processing system](https://blog.wallaroolabs.com/2018/03/performance-testing-a-low-latency-stream-processing-system/) — high level overview of what to look at when testing performance of stream processing system
* [How We Test the Stateful Autoscaling of Our Stream Processing System](https://blog.wallaroolabs.com/2018/03/how-we-test-the-stateful-autoscaling-of-our-stream-processing-system/) — advanced safety tests for autoscaling stateful stream processing
* All [posts on testing](https://blog.wallaroolabs.com/categories/testing/) from Walaroo engineering blog

There is also talk from Sean T. Allen on testing stream processing system at Wallaroo Labs (ex. Sendence)
* [Materials on Sean's blog "CodeMeshIO: How Did I Get Here?"](http://www.monkeysnatchbanana.com/2016/11/22/codemeshio-how-did-i-get-here/)
* [Video from QCon NY 2016 on InfoQ](https://www.infoq.com/presentations/trust-distributed-systems)
* [Video from CodeMeshIO on YouTube](https://www.youtube.com/watch?v=6MsPDtpe2tg)
* [Presentation on Speakerdeck](https://speakerdeck.com/seantallen/how-did-i-get-here-building-confidence-in-a-distributed-stream-processor-1)


### Google
* [Efficient Exploratory Testing of Concurrent Systems](http://www.pdl.cmu.edu/PDL-FTP/associated/CMU-PDL-11-113.pdf) — They don't mention it but looks like they describe testing of Google Omega
* [Exploratory Testing Architecture (ETA) ](https://github.com/google/cluster-data/blob/master/ETAExplorationTraces.md)
* [Paxos Made Live — An Engineering Perspective](http://research.google.com/pubs/pub33002.html) has a section on testing
* [10 Years of Crashing Google](https://www.usenix.org/conference/lisa15/conference-program/presentation/krishnan) describes some war stories from Disaster Recovery Testing (DiRT) team at Google
* [Testing for Reliability](https://landing.google.com/sre/book/chapters/testing-reliability.html) chapter from Google Site Reliability Engineering book


### Microsoft 
* [Asynchronous programming, analysis and testing with state machines](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/paper-6.pdf) — Open source language for building distributed systems. Language is designed with tooling in mind, particularly, automatic exploration of message orderings in order to find bugs.
* [Uncovering Bugs in Distributed Storage Systems during Testing (not in Production!)](http://research.microsoft.com/pubs/260939/paper.pdf)
* [Windows Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency](http://www.sigops.org/sosp/sosp11/current/2011-Cascais/11-calder-online.pdf) describes "Pressure Point Testing" approach used for Azure Cloud Storage
* [Inside Azure Search: Chaos Engineering](https://azure.microsoft.com/ru-ru/blog/inside-azure-search-chaos-engineering/)
* [TLA+ at Microsoft: 16 Years in Production](https://youtu.be/azx6cX-BlCs) by David Langworthy — how rejuvenation of TLA+ happened at Microsoft in 2016 and onwards

See also [formal methods](#formal-methods) section.


### Dropbox 
* [Mysteries of Dropbox Property-Based Testing of a Distributed Synchronization Service](http://www.cis.upenn.edu/~bcpierce/papers/mysteriesofdropbox.pdf) — example of how to use QuickCheck to test synchronisation in Dropbox and similar tools (Google Drive)
* [Data Checking at Dropbox](https://youtu.be/WUaMN2kywR4) — If you have lots of data, you have to verify that is doesn't bit rot and protect it against rare bugs (e.g. race conditions) to guarantee long term durability. This talks explains intricacies of building data consistency checker(s) at Dropbox scale.
* [Dropbox's Exabyte Storage System](https://www.facebook.com/atscaleevents/videos/1741691622770601/) (aka Magic Pocket) talk by James Cowling — describes number of strategies to achieve exteremely high durability. 
This includes:
  - guard against faulty disks,
  - guard against software defects,
  - guard against black swan events,
  - operational safeguards to reduce blast radius,
  - safeguards against deletes with multi stage soft-delete,
  - comprehensive testing strategy in-depth with increased scale,
  - redundancy across varios axis in software and hardware stacks,
  - continuous data integrity validation on many levels,
  - etc


### Atomix Copycat 
* [A novel implementation of the Raft consensus algorithm](https://github.com/atomix/copycat)
* [Jepsen tests for Atomix Copycat](https://github.com/atomix/atomix-jepsen)


### Onyx
* [Onyx Straps in For a Jepsening](http://www.onyxplatform.org/jekyll/update/2016/03/15/Onyx-Straps-In-For-A-Jepsening.html)
* [Jepsen test Onyx](https://github.com/onyx-platform/onyx-jepsen)


### LinkedIn 
* [Simoorg Failure inducer framework](https://github.com/linkedin/simoorg) — Failure inducer implemented in Python
* [A Deep Dive into Simoorg](https://engineering.linkedin.com/blog/2016/03/deep-dive-Simoorg-open-source-failure-induction-framework)
* [Dynamometer: Scale Testing HDFS on Minimal Hardware with Maximum Fidelity](https://engineering.linkedin.com/blog/2018/02/dynamometer--scale-testing-hdfs-on-minimal-hardware-with-maximum) — testing scalability of large Hadoop clusters (namely NameNode) with just fraction of nodes

### Druid.io 
* [Architecting Distributed Databases for Failure](http://www.infoq.com/presentations/data-integrity-distributed-systems)


### Salesforce 
* [Go Fast and Don't Break Things: Ensuring Quality in the Cloud](http://www.hpts.ws/papers/2011/sessions_2011/HansmaHPTS2011.pdf)


### SQLite 
SQLite is not a distributed system by any stretch of the imagination, but provides good example of comprehensive testing of database implementation.
* [Finding bugs in SQLite, the easy way](http://lcamtuf.blogspot.ru/2015/04/finding-bugs-in-sqlite-easy-way.html) — how fuzzing used in testing SQLite database 
* [How SQLite Is Tested](https://www.sqlite.org/testing.html)


### InfluxDB 
* [Jepsen and InfluxDB part 1](http://www.refactorium.com/distributed_systems/Hacking-up-a-testing-environment-for-jepsen-and-influxdb/)
* [Jepsen and InfluxDB part 2](http://www.refactorium.com/distributed_systems/InfluxDB-and-Jepsen-Chapter-II-Where-is-influxdb-on-the-cap-scale/)


### Shopify
* [Resiliency Testing with Toxiproxy](https://www.usenix.org/conference/lisa17/conference-program/presentation/pittis) 
* [Toxiproxy — A TCP proxy to simulate network and system conditions for chaos and resiliency testing](https://github.com/Shopify/toxiproxy)


### Confluent (Kafka)
* [Kafka Fault Injection framework](https://cwiki.apache.org/confluence/display/KAFKA/Fault+Injection)
* [TLA+ specification of the Kafka replication protocol](https://github.com/hachikuji/kafka-specification) and talk about using TLA+ for [hardening Kafka replication protocol](https://www.confluent.io/kafka-summit-sf18/hardening-kafka-replication)

See also [formal methods](#formal-methods) section.


### Elastic (Elastic Search)
* [Growing a protocol](https://blog.acolyer.org/2017/08/23/growing-a-protocol/) — applying [lineage driven fault injection](#lineage-driven-fault-injection) to test Elastic Search replication protocol


### YugaByte DB
* [Jepsen Testing on YugaByte DB](https://blog.yugabyte.com/jepsen-testing-on-yugabyte-db-database/) — YugaByte DB describes how they use [Jepsen](#jepsen)
* [YugaByte DB 1.1.9 analysis by Kyle Kingsbury](https://jepsen.io/analyses/yugabyte-db-1.1.9) — Kyle explores safety of YugaByte DB. Accompanying post in company blog ["YugaByte DB 1.2 Passes Jepsen Testing"](https://blog.yugabyte.com/yugabyte-db-1-2-passes-jepsen-testing/) 
and ["Wrapping Up: Jepsen Test Results for YugaByte DB 1.2 Webinar"](https://blog.yugabyte.com/wrapping-up-jepsen-test-results-for-yugabyte-db-1-2-webinar/) post with webinar recording by Kyle and Karthik Ranganathan (YugaByte CTO).
* [YugaByte DB 1.3.1](https://jepsen.io/analyses/yugabyte-db-1.3.1) — Jepsen analysis of YugaByte support for serializable SQL transactions. Companion [blog post](https://blog.yugabyte.com/yugabyte-db-distributed-sql-api-passes-jepsen-tests/) on company website.


### FaunaDB
* [Verifying Transactional Consistency with Jepsen](https://fauna.com/blog/verifying-transactional-consistency-with-jepsen-and-faunadb) — results of internal [Jepsen](#jepsen) testing at FaunaDB
* [Jepsen: FaunaDB 2.5.4](https://jepsen.io/analyses/faunadb-2.5.4) — official [Jepsen](#jepsen) test for FaunaDB, write-up in Fauna [blog](https://fauna.com/blog/faunadbs-official-jepsen-results)


### Hazelcast
* [Testing the CP Subsystem with Jepsen](https://hazelcast.com/blog/testing-the-cp-subsystem-with-jepsen/) — overview of how [Jepsen](#jepsen) is used to test Hazelcast in-memory data grid CP sybsystem


### Basho (Riak)
* [Testing Eventual Consistency in Riak](http://www.erlang-factory.com/conference/ErlangUserConference2012/speakers/UlfNorell) — how to model eventually consistent database in [QuickCheck](#quickcheck) and find bugs in it's implementation, video available [on youtube](https://youtu.be/x9mW54GJpG0)
* [Modeling Eventual Consistency Databases with QuickCheck](https://vimeo.com/23220830) — another talk on testing Riak eventual consistency guarantees with [QuickCheck](#quickcheck)


### CoreOS (etcd)
* [Testing distributed systems in Go](https://coreos.com/blog/testing-distributed-systems-in-go.html) — overview of failure injection testing for etcd


## Tools
* [Hermitage: Testing transaction isolation levels](https://github.com/ept/hermitage)
* [RapidCheck — QuickCheck port to C++](https://github.com/emil-e/rapidcheck)
* [faketime](http://manpages.ubuntu.com/manpages/natty/man1/faketime.1.html)


### Network Simulation
* [Comcast — Simulating shitty network connections so you can build better systems](https://github.com/tylertreat/comcast)
* [Muxy Simulating real-world distributed system failures](https://github.com/mefellows/muxy)
* [Namazu — Programmable fuzzy scheduler for testing distributed systems](https://github.com/osrg/namazu) 
* [Toxiproxy — A TCP proxy to simulate network and system conditions for chaos and resiliency testing](https://github.com/Shopify/toxiproxy)
* [Traffic Control](http://www.funtoo.org/Traffic_Control)
* [Python API for Linux Traffic Control](https://github.com/praus/shapy)
* [Slow tool](https://github.com/ModusCreateOrg/slow/)
* [Blockade is a utility for testing network failures and partitions in distributed applications](https://github.com/dcm-oss/blockade)
* [DEMi: Distributed Execution Minimizer for Akka](https://github.com/NetSys/demi)


### QuickCheck 
* [PolyConf 14: Testing the Hard Stuff and Staying Sane / John Hughes](https://youtu.be/F6LzB6SdFKA)
* [The Joy of Testing](http://www.infoq.com/presentations/The-Joy-of-Testing)
* [John Hughes on InfoQ](http://www.infoq.com/author/John-Hughes)
* [Hansei: Property-based Development of Concurrent Systems](https://speakerdeck.com/jtuple/hansei-property-based-development-of-concurrent-systems)
* [QuickChecking Poolboy for Fun and Profit](http://basho.com/posts/technical/quickchecking-poolboy-for-fun-and-profit/) — from Basho
* [Combining Fault-Injection with Property-Based Testing](https://dl.acm.org/doi/10.1145/2559627.2559629)
* [Testing Telecoms Software with Quviq QuickCheck](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.148.6554&rep=rep1&type=pdf)
* [Fuzz testing distributed systems with QuickCheck](https://making.pusher.com/fuzz-testing-distributed-systems-with-quickcheck/index.html) — using QuickCheck to test Raft protocol implementation in Haskell


### Benchmarking 
* [OLTP-Bench: An Extensible Testbed for Benchmarking Relational Databases](http://www.vldb.org/pvldb/vol7/p277-difallah.pdf)
* [OLTP Benchmark Wiki](http://oltpbenchmark.com/wiki/index.php?title=Main_Page)
* [OLTP Benchmark on Github](https://github.com/oltpbenchmark)
* [Py-TPCC](https://github.com/apavlo/py-tpcc)
* [Netflix Data Benchmark: Benchmarking Cloud Data Stores](http://techblog.netflix.com/2016/09/netflix-data-benchmark-benchmarking.html)


### Linkbench 
* [LinkBench from Facebook](https://www.facebook.com/notes/facebook-engineering/linkbench-a-database-benchmark-for-the-social-graph/10151391496443920) and [Github.com repo](https://github.com/facebookarchive/linkbench)
* [LinkBenchX from Percona](https://www.percona.com/blog/2015/05/01/linkbenchx-benchmark-based-arrival-request-rate/)


### YCSB 
* [Yahoo! Cloud System Benchmark (YCSB)](https://github.com/brianfrankcooper/YCSB)
* [YCSB+T: Benchmarking Web-scale Transactional Databases](http://www.researchgate.net/publication/269306582_YCSBT_Benchmarking_web-scale_transactional_databases)
* [YCSB++](http://www.pdl.cmu.edu/ycsb++/)
* [Correcting YCSB's Coordinated Omission problem](http://psy-lob-saw.blogspot.ru/2015/03/fixing-ycsb-coordinated-omission.html)

