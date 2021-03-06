# Cassovary vs. GraphJet

Cassovary has a class [`com.twitter.cassovary.PerformanceBenchmark`](https://github.com/twitter/cassovary/blob/master/cassovary-benchmarks/src/main/scala/com/twitter/cassovary/PerformanceBenchmark.scala) for running performance benchmarks.

The class reads graph data from `cassovary-benchmarks/src/main/resources/graphs/`.

Here's how to run global PageRank on graph data that's stored directly in the repo:

```
$ ./sbt "project cassovary-benchmarks" "run-main com.twitter.cassovary.PerformanceBenchmark -local=facebook -globalpr"
$ ./sbt "project cassovary-benchmarks" "run-main com.twitter.cassovary.PerformanceBenchmark -local=wiki -globalpr"
```

Running Cassovary on the [LiveJournal graph from SNAP](https://snap.stanford.edu/data/soc-LiveJournal1.html) - download the data and put it in the right directory:


```
$ wget http://snap.stanford.edu/data/soc-LiveJournal1.txt.gz
$ gunzip soc-LiveJournal1.txt.gz
$ cp soc-LiveJournal1.txt.gz cassovary-benchmarks/src/main/resources/graphs/
```

Now you can you run the performance benchmark in Cassovary:

```
$ ./sbt "project cassovary-benchmarks" \
  "run-main com.twitter.cassovary.PerformanceBenchmark -local=soc-LiveJournal1 -separator=9 -globalpr"
```

Note that the performance benchmark by default expects the edge list
to be space delimited. The LiveJournal data is tab separated, which is
why we use the `-separator=9` option (tab is decimal 9).

See also McSherry et al.'s ["Scalability! But at what COST?"](https://www.usenix.org/conference/hotos15/workshop-program/presentation/mcsherry) paper and [associated code on GitHub](https://github.com/frankmcsherry/COST).

