## Introduction
This is a simple utility to identify the cassandra tables on a node that are currently receiving the largest number of reads and writes. Finding out what tables are currently receiving reads and and writes can be challenging. Particularly if you have 50 or more application tables.

Typically, the only real option is to record read/write metrics for every table on a node via JMX. This tool leverages 'nodetool cfstats' output to generate a report of the top N tables receiving reads and writes on a particular node.
This output can then be used to investigate individual partitions using 'nodetool toppartitions'


## Instructions
Clone the repo and copy to the node you want to examine
```
git clone https://github.com/gregory-smith/requesthunter.git
```

Execute the wrapper script

```
./requesthunter
```

By default 'requesthunter.sh' will call 'nodetool cfstats' every two minutes and leverage 'cfstats-diff' to generate the Top 5 tables for reads and writes during that period.

Sample output

```
./requesthunter
Mon Oct  2 13:55:14 UTC 2017
dse_perf.node_slow_log  reads: 50
OpsCenter.events  reads: 32
OpsCenter.rollups60  reads: 30
OpsCenter.events_timeline  reads: 2
system.local  reads: 1
OpsCenter.rollups60  writes: 1359
OpsCenter.rollup_state  writes: 1176
OpsCenter.rollups300  writes: 112
system.size_estimates  writes: 20
system.sstable_activity  writes: 17
```
