# first time start

```
bash-5.0# ./dkron raft list-peers --rpc-addr=172.22.0.2:6868 // if you run on docker instead of localhost, you need add this param
INFO[0000] No valid config found: Applying default values.  error="Config File \"dkron\" Not Found in \"[/etc/dkron /root/.dkron /opt/local/dkron/config]\""
Node         ID           Address          State     Voter
testServer1  testServer1  172.22.0.3:6868  leader    true
testSeed     testSeed     172.22.0.2:6868  follower  true
```

# docker-compose down, then docker-compose up

Keep trying to elect but always failed.
```
testSeed | time="2020-02-06T05:38:14Z" level=info msg="2020/02/06 05:38:14 [WARN] raft: Election timeout reached, restarting election"
testSeed | time="2020-02-06T05:38:14Z" level=info msg="2020/02/06 05:38:14 [INFO] raft: Node at 172.24.0.2:6868 [Candidate] entering Candidate state in term 12"
testSeed | time="2020-02-06T05:38:14Z" level=info msg="2020/02/06 05:38:14 [DEBUG] raft: Votes needed: 2"
testSeed | time="2020-02-06T05:38:14Z" level=info msg="2020/02/06 05:38:14 [DEBUG] raft: Vote granted from testSeed in term 12. Tally: 1"
testSeed | time="2020-02-06T05:38:14Z" level=info msg="2020/02/06 05:38:14 [ERR] raft: Failed to make RequestVote RPC to {Voter testServer1 172.22.0.3:6868}: dial tcp 172.22.0.3:6868: i/o timeout" 172.22.0.2:6868: i/o timeout"
```
So, you can notice that node is 172.24.0.3 this time but keep requesting 172.22.0.x.

### go check dashboard get server ip for this case is 172.24.0.2 but last time is 172.22.0.2
```
bash-5.0# ./dkron raft list-peers --rpc-addr=172.24.0.2:6868
INFO[0000] No valid config found: Applying default values.  error="Config File \"dkron\" Not Found in \"[/etc/dkron /root/.dkron /opt/local/dkron/config]\""
Node       ID           Address          State     Voter
(unknown)  testServer1  172.22.0.3:6868  follower  true
(unknown)  testSeed     172.22.0.2:6868  follower  true
```

### To solve this, each dkron server need a fixed ip