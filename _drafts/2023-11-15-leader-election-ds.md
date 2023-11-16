---
layout: post
title: "Summary of Understanding Distributed system by Roberto Vitillo"
date: 2023-11-15 21:03:36 +0030
categories: distributed-system
---

A leader election algorithm needs to guarantee that 
* there is at most one leader at any given time 
* an election eventually completes.

### Raft leader election

Raft leader election algorithm is implemented with a state machine in which a process is one of three states,

* _the follower state_, in which the process recognize another one as leader
* _the candidate state_, in which the process starts a new election proposing itself as a leader
* or _the leader state_, in which the process is the leader.

Election Term: 
* An election term is represented with a logical clock, a numerical counter that can only increase over time. 
* The algorithm guarantees that for any term there is at most one leader.

Leader and Follower:
* follower expects to receive a periodic heartbeat from the leader containing the election term the leader was elected in. 
* If the follower doesn’t receive any heartbeat within a certain time period, a timeout fires and the leader is presumed dead.
* At that point, the follower starts a new election by incrementing the current election term and transitioning to the candidate state.

Vote:
* candidate votes for itself and sends a request to all the processes in the system to vote for it, stamping the request with the current election term.


![Alt text](https://github.com/frhan/frhan.github.io/blob/master/assets/screenshot/uds/uds-4.png?raw=true "a title")






