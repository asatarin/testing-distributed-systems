# Testing Distributed Systems

## Overview of  testing approaches


### RICON 2014: Ines Sombra, Fastly - Testing in a Distributed World
https://youtu.be/KSdNYi55kjg

Great overview of techniques for testing distributed systems.
Additional materials for this talk could be found in [this Github repo](https://github.com/Randommood/RICON2014)

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
* [The verification of a distributed system By Caitie McCaffrey](http://queue.acm.org/detail.cfm?id=2889274)


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
* [Game Day Exercises at Stripe: Learning from `kill -9`](https://stripe.com/blog/game-day-exercises-at-stripe)
* [Sometimes Kill -9 Isn’t Enough](http://bravenewgeek.com/sometimes-kill-9-isnt-enough/)
* [Comcast tool](https://github.com/tylertreat/Comcast)
* [Slow tool](https://github.com/ModusCreateOrg/slow/)
* [Python API for Linux Traffic Control](https://github.com/praus/shapy)

### Performance and Benchmarking
* [Your Load Generator Is Probably Lying To You](http://highscalability.com/blog/2015/10/5/your-load-generator-is-probably-lying-to-you-take-the-red-pi.html)
* [Everything You Know About Latency Is Wrong](http://bravenewgeek.com/everything-you-know-about-latency-is-wrong/) -- great overview of Gil Tene`s "How NOT to Measure Latency" talk
* ["How NOT to Measure Latency" by Gil Tene](https://www.youtube.com/watch?v=lJ8ydIuPFeU)
* ["Benchmarking: You're Doing It Wrong" by Aysylu Greenberg](https://www.youtube.com/watch?v=XmImGiVuJno)

### etc
* [Simple Testing Can Prevent Most Critical Failures: An Analysis of Production Failures in Distributed Data-Intensive Systems](https://www.usenix.org/conference/osdi14/technical-sessions/presentation/yuan)


## Concrete approaches in different distributed systems
### Amazon DynamoDB
* [The Evolution of Testing Methodology at AWS: From Status Quo to Formal Methods with TLA+](http://www.infoq.com/presentations/aws-testing-tla)
* [Use of Formal Methods at Amazon Web Services](http://research.microsoft.com/en-us/um/people/lamport/tla/formal-methods-amazon.pdf)
* [CACM Article "How Amazon Web Services Uses Formal Methods"](http://cacm.acm.org/magazines/2015/4/184701-how-amazon-web-services-uses-formal-methods/fulltext)
* [Experience of software engineers using TLA+, PlusCal and TLC](http://tla2012.loria.fr/contributed/newcombe-slides.pdf)
* [Debugging Designs by Chris Newcombie](http://www.hpts.ws/papers/2011/sessions_2011/Debugging.pdf) there is also a  [source bundle](http://www.hpts.ws/papers/2011/sessions_2011/amazonbundle.tar.gz)
