---
layout: post
title: "Understanding Distributed system by Roberto Vitillo"
date: 2023-07-17 21:03:36 +0530
categories: distributed-system
---

This post is the summary of the book called `Understanding Distributed system` by Roberto Vitillo.

#### Chapter 1: Introduction

<p>Fundamental  challenges of distributed system </p>

* Communication
* Coordination
* Scalability
* Resiliency
* Operations

<b>Coordination</b>: <p>It's a very hard challenge to coordinate multiple nodes into a single coherent in the presence of failures.
                     </p> 

<b>Resiliency</b>: <p>System availability is defined as the amount of time the application can server request divided by the duration of the period measured.
Availability often describe with nines. Three nines are typically considered acceptable, and anything above four is considered highly available.
                    </p>

### Chapter 2: Reliable links

#### 2.1 Reliability
* TCP partitions a byte stream into discrete packets called segments.

#### 2.2 Connection lifecycle
* The opening state, in which the connection is being created.
* The established state, in which the connection is open and data is being transferred. 
* The closing state, in which the connection is being closed.

TCP uses a three-way handshake to create a new connection:
1. The sender picks a random sequence number x and sends a SYN segment to the receiver.
2. The receiver increments x, chooses a random sequence num ber y and sends back a SYN/ACK segment.
3. The sender increments both sequence numbers and replies with an ACK segment and the first bytes of application data.


![Alt text](https://github.com/frhan/frhan.github.io/blob/master/assets/screenshot/uds/uds-1.png "a title")

