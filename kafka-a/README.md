# Kafka

Remember that zookeeper cluster is more important than kafka cluster!
Zookeeper absolutely MUST work, it is recommended to have 5 node zk cluster!

To save costs you can run multiple kafka cluster with same zk cluster using a zk prefix:
```
zookeeper.connect=zookeeper1.a.local:2181,zookeeper2.a.local:2182,zookeeper3.a.local:2183,zookeeper4.a.local:2184,zookeeper5.a.local:2185/kafka/a
```

The most important kafka setting is:
```
default.replication.factor=2
```

it should be 2 or 3!!!
Number of nodes should be >= replication factor

Producers will work ok until they have at least 1 node with a partition replica that can be elected a leader,
same for consumers. Leader election configs are very important, as well consumer offset configs.
if topic *"__consumer_offsets"* has no broker leader for a specific partition.

Number of nodes is irrelevant for availability, number of replicas is all that matters!!!

It is probably best to have main "input" cluster with 3 nodes and replication 3,
and several downstream "namespace" clusters for derived topics with 2 nodes and replication 2.
