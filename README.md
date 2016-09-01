## Overview of  testing approaches

### RICON 2014: Ines Sombra, Fastly - Testing in a Distributed World
https://youtu.be/KSdNYi55kjg

Great overview of techniques for testing distributed systems.
Additional materials for this talk could be found in [this Github repo](https://github.com/Randommood/RICON2014)


### Technologies for Testing Distributed Systems by Colin Skott
Colin Skott shares his viewpoint from academia on testing distributed systems.
* [Technologies for Testing Distributed Systems, Part I](http://colin-scott.github.io/blog/2016/03/04/technologies-for-testing-and-debugging-distributed-systems/)
* See also post [Distributed Systems Testing: The Lost World](http://tagide.com/blog/research/distributed-systems-testing-the-lost-world/) by Crista Lopes


### Research papers on testing distributed systems
* [Simple Testing Can Prevent Most Critical Failures: An Analysis of Production Failures in Distributed Data-Intensive Systems](https://www.usenix.org/conference/osdi14/technical-sessions/presentation/yuan) -- Great overview of how even simple testing can help a lot, you just need right focus.
* [What Bugs Live in the Cloud? A Study of 3000+ Issues in Cloud Systems](http://ucare.cs.uchicago.edu/pdf/socc14-cbs.pdf)  -- study of actual bugs in different popular distributed systems (Hadoop MapReduce, HDFS, HBase, Cassandra, ZooKeeper
and Flume)


### Richard Cook
* [Velocity NY 2013: Richard Cook, "Resilience In Complex Adaptive Systems"](https://www.youtube.com/watch?v=PGLYEDpNu60&feature=youtu.be)
* [Velocity 2012: Richard Cook, "How Complex Systems Fail"](https://www.youtube.com/watch?v=2S0k12uZR14&feature=youtu.be)
* [How Complex Systems Fail](http://web.mit.edu/2.75/resources/random/How%20Complex%20Systems%20Fail.pdf)

###  Misc testing approaches
* ["Simulation Testing" by Michael Nygard](http://www.youtube.com/watch?v=N5HyVUPuU0E&feature=youtu.be)

### Aphyr's Jepsen
* [Kyle Kingsbury on InfoQ](http://www.infoq.com/author/Kyle-Kingsbury)
* [Jepsen: RethinkDB 2.1.5](https://aphyr.com/posts/329-jepsen-rethinkdb-2-1-5)
* [Jepsen: RethinkDB 2.2.3 reconfiguration](https://aphyr.com/posts/330-jepsen-rethinkdb-2-2-3-reconfiguration)
* [Aphyr's Jepsen posts](https://aphyr.com/tags/Jepsen)
* [Jepsen Talks](https://github.com/aphyr/jepsen-talks)
* [Call me maybe: Jepsen and flaky networks](http://www.slideshare.net/shalinmangar/call-me-maybe-jepsen-and-flaky-networks)
* [Test scaffolding](https://github.com/aphyr/jepsen/blob/master/doc/scaffolding.md) -- start page if you want to write Jepsen test


### Formal Methods
* [Comparisons of Alloy and Spin](http://www2.research.att.com/~pamela/model.html)
* [Verdi: Formally Verifying Distributed Systems](http://verdi.uwplse.org/)
* [Network Semantics for Verifying Distributed Systems](https://homes.cs.washington.edu/~jrw12/network-semantics.html)
* [The verification of a distributed system By Caitie McCaffrey](http://queue.acm.org/detail.cfm?id=2889274) also [podcast](https://www.infoq.com/articles/podcast-caitie-mccaffrey) on InfoQ.com and [accompanying materials](https://github.com/CaitieM20/TheVerificationOfDistributedSystem) on GitHub and a [slidedeck](https://speakerdeck.com/caitiem20/qcon-newyork-2016-the-verification-of-a-distributed-system)


### Fuzzing
* [Fuzzing Raft for Fun and Publication](https://colin-scott.github.io/blog/2015/10/07/fuzzing-raft-for-fun-and-profit/)
* [DNS parser, meet Go fuzzer](https://blog.cloudflare.com/dns-parser-meet-go-fuzzer/)
* [Fuzz Testing with afl-fuzz (American Fuzzy Lop)](http://spin.atomicobject.com/2015/08/23/fuzz-testing-american-fuzzy-lop/)
* [Randomized testing for Go](https://github.com/dvyukov/go-fuzz) and talk on this tool [GopherCon 2015: Dmitry Vyukov - Go Dynamic Tools](https://www.youtube.com/watch?v=a9xrxRsIbSU)
* [Simple guided fuzzing for libraries using LLVM's new libFuzzer](http://blog.llvm.org/2015/04/fuzz-all-clangs.html)
* [LibFuzzer – a library for coverage-guided fuzz testing](http://llvm.org/docs/LibFuzzer.html)
* [How Heartbleed could've been found](https://blog.hboeck.de/archives/868-How-Heartbleed-couldve-been-found.html) -- example of how fuzzing could be used for finding famous HeartBleed vulnerability
* [Combining AFL and QuickCheck for Directed Fuzzing by Dan Luu](http://danluu.com/testing/)


### Kill-dash-nine
* [Game Day Exercises at Stripe: Learning from kill -9](https://stripe.com/blog/game-day-exercises-at-stripe)
* [Sometimes Kill -9 Isn’t Enough](http://bravenewgeek.com/sometimes-kill-9-isnt-enough/)
* [Comcast tool](https://github.com/tylertreat/Comcast)
* [Slow tool](https://github.com/ModusCreateOrg/slow/)
* [Python API for Linux Traffic Control](https://github.com/praus/shapy)
* [Blockade is a utility for testing network failures and partitions in distributed applications](https://github.com/dcm-oss/blockade)

### Performance and Benchmarking
* [Your Load Generator Is Probably Lying To You](http://highscalability.com/blog/2015/10/5/your-load-generator-is-probably-lying-to-you-take-the-red-pi.html)
* [Everything You Know About Latency Is Wrong](http://bravenewgeek.com/everything-you-know-about-latency-is-wrong/) -- great overview of Gil Tene`s "How NOT to Measure Latency" talk
* ["How NOT to Measure Latency" by Gil Tene](https://www.youtube.com/watch?v=lJ8ydIuPFeU)
* ["Benchmarking: You're Doing It Wrong" by Aysylu Greenberg](https://www.youtube.com/watch?v=XmImGiVuJno)


## Concrete approaches in different distributed systems
### Amazon DynamoDB
* [The Evolution of Testing Methodology at AWS: From Status Quo to Formal Methods with TLA+](http://www.infoq.com/presentations/aws-testing-tla)
* [Use of Formal Methods at Amazon Web Services](http://research.microsoft.com/en-us/um/people/lamport/tla/formal-methods-amazon.pdf)
* [CACM Article "How Amazon Web Services Uses Formal Methods"](http://cacm.acm.org/magazines/2015/4/184701-how-amazon-web-services-uses-formal-methods/fulltext)
* [Experience of software engineers using TLA+, PlusCal and TLC](http://tla2012.loria.fr/contributed/newcombe-slides.pdf)
* [Debugging Designs by Chris Newcombie](http://www.hpts.ws/papers/2011/sessions_2011/Debugging.pdf) there is also a  [source bundle](http://www.hpts.ws/papers/2011/sessions_2011/amazonbundle.tar.gz)

### Netflix 
* [Monkeys in Lab Coats: Applying Failure Testing Research @Netflix](http://www.infoq.com/presentations/failure-test-research-netflix)
* [“Monkeys in Labs Coats”: Applied Failure Testing Research at Netflix](http://www.infoq.com/news/2016/03/failure-testing-netflix)
* [Automated Failure Testing](http://techblog.netflix.com/2016/01/automated-failure-testing.html)
* [Netflix Simian Army](http://techblog.netflix.com/2011/07/netflix-simian-army.html)
* [Failure Injection Testing](http://techblog.netflix.com/2014/10/fit-failure-injection-testing.html)
* [From Chaos to Control - Testing the resiliency of Netflix’s Content Discovery Platform](http://techblog.netflix.com/2015/08/from-chaos-to-control-testing.html)
* [Breaking Bad at Netflix: Building Failure as a Service](http://www.infoq.com/presentations/failure-as-a-service-netflix)
* [GTAC 2014: I Don't Test Often ... But When I Do, I Test in Production](https://www.youtube.com/watch?v=xkP70Zhhix4) -- Netflix different testing strategies
* [Principles of Chaos Engineering](http://www.principlesofchaos.org/)

### Twitter 
* [Diffy: Testing services without writing tests](https://blog.twitter.com/2015/diffy-testing-services-without-writing-tests)
* [How we break things at Twitter: failure testing](https://blog.twitter.com/2015/how-we-break-things-at-twitter-failure-testing)

### Datastax (Cassandra) 
* [Testing Apache Cassandra with Jepsen](http://www.datastax.com/dev/blog/testing-apache-cassandra-with-jepsen)
* [Testing Cassandra Guarantees under Diverse Failure Modes with Jepsen](http://www.slideshare.net/jkni/testing-cassandra-guarantees-under-diverse-failure-modes-with-jepsen-53168992)
* [Testing Cassandra Guarantees under Diverse Failure Modes with Jepsen](http://cassandrasummit-datastax.com/agenda/testing-cassandra-guarantees-under-diverse-failure-modes-with-jepsen/)
* [Jepsen Cassandra Testing on Git](https://github.com/riptano/jepsen)
* [Netflix A STATE OF XEN - CHAOS MONKEY & CASSANDRA](https://vimeopro.com/user35188327/cassandra-summit-2015/video/140949186) from Cassandra Summit 2015

### ScyllaDB
They published series of blog posts on testing ScyllaDB:
* [Scylla testing part 1: Cassandra compatibility testing](http://www.scylladb.com/2016/02/04/cassandra-compatibility-testing/)
* [Scylla testing part 2: Extending Jepsen for testing Scylla](http://www.scylladb.com/2016/02/11/jepsen-testing/)
* [CharybdeFS: a new fault-injecting filesystem for software testing](http://www.scylladb.com/2016/02/16/fault-injection-filesystem-software-testing/)
* [Testing part 4: Distributed tests](http://www.scylladb.com/2016/03/10/dtest-scylla/)
* [Testing part 5: Longevity testing](http://www.scylladb.com/2016/03/15/longevity-testing-scylla/)
* [Fault-injecting filesystem cookbook](http://www.scylladb.com/2016/05/02/fault-injection-filesystem-cookbook/)

### VoltDB 
Series of post on testing at VoltDB:
* [How We Test at VoltDB](https://voltdb.com/blog/how-we-test-voltdb)
* [Testing at VoltDB: SQLCoverage](https://voltdb.com/blog/testing-voltdb-sqlcoverage) 
Describes how they test SQL query functionality using 5 millions queries generated from templates and comparing results against HSQLDB.
* [Testing VoltDB Against PostgreSQL](https://voltdb.com/blog/testing-voltdb-against-postgresql)

Additional resources:
* ["All In With Determinism for Performance and Testing in Distributed Systems" by John Hugg](https://www.youtube.com/watch?v=gJRj3vJL4wE) and a slide deck [Hugg-DeterministicDistributedSystems.pdf](https://github.com/strangeloop/StrangeLoop2015/blob/master/slides/talks/Hugg-DeterministicDistributedSystems.pdf)
* [SelfCheck workload](https://github.com/VoltDB/voltdb/tree/master/tests/test_apps/txnid-selfcheck2)
* [TPC-C implementation](https://github.com/VoltDB/voltdb/tree/master/tests/test_apps/tpcc)

### MemSQL 
* [Running MemSQL’s 107 Node Test Infrastructure on CoreOS](http://blog.memsql.com/running-memsqls-107-node-test-infrastructure-on-coreos/)
* [Practical Techniques to Achieve Quality in Large Software Projects](http://blog.memsql.com/practical-techniques-to-achieve-quality-in-large-software-projects-3/)
* [How to Make a Believable Benchmark](http://blog.memsql.com/how-to-make-a-believable-benchmark/)
* [Building an Infinitely Scalable Testing System](http://blog.memsql.com/building-an-infinitely-scalable-testing-system/) -- description of internal test system PsyDuck

### CockroachDB
* [DIY Jepsen Testing CockroachDB](https://www.cockroachlabs.com/blog/diy-jepsen-testing-cockroachdb/) -- great read about using Jepsen at Cockroach Labs

### Cloudera
* [Quality Assurance at Cloudera: Fault Injection and Elastic Partitioning](http://blog.cloudera.com/blog/2016/04/quality-assurance-at-cloudera-fault-injection-and-elastic-partitioning/) -- Cloudera describes their approach to fault injection testing
 

### FoundationDB 
* ["Testing Distributed Systems w/ Deterministic Simulation" by Will Wilson](https://www.youtube.com/watch?v=4fFDFbi3toc&feature=youtu.be)

### Google
* [Efficient Exploratory Testing of Concurrent Systems](http://www.pdl.cmu.edu/PDL-FTP/associated/CMU-PDL-11-113.pdf) -- They don`t mention it but looks like they describe testing of Google Omega
* [Exploratory Testing Architecture (ETA) ](https://github.com/google/cluster-data/blob/master/ETAExplorationTraces.md)
* [Paxos Made Live - An Engineering Perspective](http://research.google.com/pubs/pub33002.html) has a section on testing
* [10 Years of Crashing Google](https://www.usenix.org/conference/lisa15/conference-program/presentation/krishnan) describes some war stories from Disaster Recovery Testing (DiRT) team at Google

### Microsoft 
* [Uncovering Bugs in Distributed Storage Systems during Testing (not in Production!) ](http://research.microsoft.com/pubs/260939/paper.pdf)
* [Windows Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency](http://www.sigops.org/sosp/sosp11/current/2011-Cascais/11-calder-online.pdf) describes "Pressure Point Testing" approach used for Azure Cloud Storage
* [Inside Azure Search: Chaos Engineering](https://azure.microsoft.com/ru-ru/blog/inside-azure-search-chaos-engineering/)

### Dropbox 
* [Mysteries of Dropbox Property-Based Testing of a Distributed Synchronization Service](http://www.cis.upenn.edu/~bcpierce/papers/mysteriesofdropbox.pdf) -- example of how to use QuickCheck to test synchronisation in Dropbox and similar tools (Google Drive)

### Atomix Copycat 
* [A novel implementation of the Raft consensus algorithm](https://github.com/atomix/copycat)
* [Jepsen tests for Atomix Copycat](https://github.com/atomix/atomix-jepsen)

### Onyx
* [Onyx Straps in For a Jepsening](http://www.onyxplatform.org/jekyll/update/2016/03/15/Onyx-Straps-In-For-A-Jepsening.html)
* [Jepsen test Onyx](https://github.com/onyx-platform/onyx-jepsen)

### LinkedIn 
* [Simoorg Failure inducer framework](https://github.com/linkedin/simoorg) -- Failure inducer implemented in Python
* [A Deep Dive into Simoo](https://engineering.linkedin.com/blog/2016/03/deep-dive-Simoorg-open-source-failure-induction-framework)

### Druid.io 
* [Architecting Distributed Databases for Failure](http://www.infoq.com/presentations/data-integrity-distributed-systems)

### Salesforce 
* [Go Fast and Don't Break Things: Ensuring Quality in the Cloud](http://www.hpts.ws/papers/2011/sessions_2011/HansmaHPTS2011.pdf)

### TimSort 
* [Proving that Android’s, Java’s and Python’s sorting algorithm is broken (and showing how to fix it)](http://envisage-project.eu/proving-android-java-and-python-sorting-algorithm-is-broken-and-how-to-fix-it/)

### SQLite 
* [Finding bugs in SQLite, the easy way](http://lcamtuf.blogspot.ru/2015/04/finding-bugs-in-sqlite-easy-way.html) -- how fuzzing used in testing SQLite database 
* [How SQLite Is Tested](https://www.sqlite.org/testing.html)

### InfluxDB 
* [Jepsen and InfluxDB part 1](http://www.refactorium.com/distributed_systems/Hacking-up-a-testing-environment-for-jepsen-and-influxdb/)
* [Jepsen and InfluxDB part 2](http://www.refactorium.com/distributed_systems/InfluxDB-and-Jepsen-Chapter-II-Where-is-influxdb-on-the-cap-scale/)

## Tools
* [Hermitage: Testing transaction isolation levels](https://github.com/ept/hermitage)
* [RapidCheck - QuickCheck port to C++](https://github.com/emil-e/rapidcheck)
* [Verdi - A framework for formally verifying distributed systems implementations in Coq](https://github.com/uwplse/verdi)
* [Simulating shitty network connections so you can build better systems](https://github.com/tylertreat/comcast)
* [Muxy Simulating real-world distributed system failures](https://github.com/mefellows/muxy)
* [faketime](http://manpages.ubuntu.com/manpages/natty/man1/faketime.1.html)

### QuickCheck 
* [PolyConf 14: Testing the Hard Stuff and Staying Sane / John Hughes](http://www.youtube.com/watch?v=F6LzB6SdFKA&feature=youtu.be)
* [The Joy of Testing](http://www.infoq.com/presentations/The-Joy-of-Testing)
* [John Hughes on InfoQ](http://www.infoq.com/author/John-Hughes)
* [Hansei: Property-based Development of Concurrent Systems](https://speakerdeck.com/jtuple/hansei-property-based-development-of-concurrent-systems)
* [QuickChecking Poolboy for Fun and Profit](http://basho.com/posts/technical/quickchecking-poolboy-for-fun-and-profit/) -- from Basho
* [Combining Fault-Injection with Property-Based Testing](http://www2.hh.se/staff/magnusj/papers/2014_DATE_ES4CPS.pdf)
* [Testing Telecoms Software with Quviq QuickCheck](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.148.6554&rep=rep1&type=pdf)

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

### Traffic Control 
* [Traffic Control](http://www.funtoo.org/Traffic_Control)
