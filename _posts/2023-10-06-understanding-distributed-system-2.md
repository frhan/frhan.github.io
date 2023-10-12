---
layout: post
title: "Understanding Distributed system ch:6-11 by Roberto Vitillo"
date: 2023-10-07 21:03:36 +0530
categories: distributed-system
---

# Chapter 6 : System models
A _system model_ encodes assumptions about the behavior of nodes, communication links, and timing;

Let’s start by introducing some models for communication links:
* The _fair-loss_ link model assumes that messages may be lost and duplicated.
* The _reliable link_ model assumes that a message is delivered
  exactly once, without loss or duplication.
* The _authenticated reliable_ link model makes the same assumptions as the reliable link, but additionally assumes that the
  receiver can authenticate the message’s sender.

the different types of node failures we expect to happen:
* The _arbitrary-fault_ model assumes that a node can deviate from its algorithm in arbitrary ways, leading to crashes or unexpected behavior due to bugs or malicious activity. The arbitrary fault model is also referred to as the “Byzantine” model for historical reasons.
* The _crash-recovery_ model assumes that a node does not deviate from its algorithm, but can crash and restart at any time, losing its in-memory state.
* The crash-stop model assumes that a node doesn’t deviate from its algorithm, but if it crashes it never comes back online.