# Recovery
* Single Server / Multi-Server
https://dkron.io/usage/recovery/
Check is back online or not ? A fully healthy state has return.

## Single Server Cluster
Restart directly, if failed create a new one.

## Failed Server in Multi Cluster
Easiest option is to bring it back online and have it rejoin the cluster with the same IP address

## Multi Failed Server in Multi Cluster
Normaly would cause data uncommitted loss and imcompleted.

* You simply include just the remaining servers in the raft/peers.json recovery file. The cluster should be able to elect a leader once the remaining servers are all restarted with an identical raft/peers.json configuration.

Any new servers you introduce later can be fresh with totally clean data directories.

* Extremely case. It should be possible to recover with just a single remaining server by starting that single server with itself as the only peer in the raft/peers.json recovery file.


# Manual Recovery
* peer.json

# Backup
* Share Volume With dkron.data
```You must plan a backup strategy for the data directories, you can configure it using the --data-dir parameter, by default ./dkron.data.```

# Memo
## dkron agent --server --bootstrap-expect=X
dkron will wait until the specified number X of servers are available and then bootstraps the cluster. This allows an initial leader to be elected automatically.