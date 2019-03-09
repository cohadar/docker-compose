# zookeeper

## importance of zookeeper
zookeeper cluster is more important than kafka cluster!
if zookeeper cluster is not working or is in split state, kafka will stop working HARD after some time.
With 5 zookeeper nodes, zk cluster can suffer 2 nodes down, if 3 nodes go down it will stop serving.
If those 2 nodes come back up but don't sync with 3 previous nodes, cluster will be in split state.

You can test this with
```
echo stats | zookeeper1.a.local 2181
```

In worst case scenario, you can fix the cluster by shutting down ALL nodes at once and restarting them again.
