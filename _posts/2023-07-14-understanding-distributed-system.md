---
layout: post
title: "Understanding Distributed system by Roberto Vitillo"
date: 2023-07-17 21:03:36 +0530
categories: distributed-system
---

This post is the summary of the book called `Understanding Distributed system` by Roberto Vitillo.

## Chapter 1: Introduction

<p>Fundamental  challenges of distributed system </p>

* Communication
* Coordination
* Scalability
* Resiliency
* Operations

<b>Coordination</b>: It's a very hard challenge to coordinate multiple nodes into a single coherent in the presence of failures.

<b>Resiliency</b>: System availability is defined as the amount of time the application can server request divided by the duration of the period measured.
Availability often describe with nines. Three nines are typically considered acceptable, and anything above four is considered highly available.

## Chapter 2: Reliable links

### 2.1 Reliability
* TCP partitions a byte stream into discrete packets called segments.

### 2.2 Connection lifecycle
* The opening state, in which the connection is being created.
* The established state, in which the connection is open and data is being transferred. 
* The closing state, in which the connection is being closed.

TCP uses a three-way handshake to create a new connection:
1. The sender picks a random sequence number x and sends a SYN segment to the receiver.
2. The receiver increments x, chooses a random sequence num ber y and sends back a SYN/ACK segment.
3. The sender increments both sequence numbers and replies with an ACK segment and the first bytes of application data.

![Alt text](https://github.com/frhan/frhan.github.io/blob/master/assets/screenshot/uds/uds-1.png?raw=true "a title")

### 2.3 FLow Control
* Flow control is a backoff mechanism implemented to prevent the sender from overwhelming the receiver.
* The sender, if it’s respecting the protocol, avoids sending more data that can fit in the receiver’s buffer.
* TCP is rate-limiting on a connection level.

### 2.4 Congestion control
* When a new connection is established, the size of the congestion window is set to a system default. Then, for every segment acknowledged, the window increases its size exponentially until reaching an upper limit.
* When the sender detects a missed acknowledgment through a timeout, a mechanism called congestion avoidance kicks in, and the congestion window size is reduced.

### 2.5 Custom protocols
TCP’s reliability and stability come at the price of lower bandwidth
and higher latencies than the underlying network is actually capable of delivering.

* Unlike TCP, UDP does not expose the abstraction of a byte
  stream to its clients. Clients can only send discrete packets,
  called datagrams, with a limited size.
* UDP doesn’t implement flow and congestion control either.

## Chapter 3: Secure links

### 3.1 Encryption

Encryption guarantees that the data transmitted between a client and a server is obfuscated and can only be read by the communicating processes.

### 3.2 Authentication
* TLS implements authentication using digital signatures based on asymmetric cryptography.
* One of the most common mistakes when using TLS is letting a certificate expire
* Automation to monitor and auto-renew certificates close to expiration is well worth the investment.

### 3.3 Integrity

* TLS verifies the integrity of the data by calculating a message digest. A secure hash function
  is used to create a message authentication code(HMAC).
* The TLS HMAC protects against data corruption as well, not just tampering.
* While TCP does use a checksum to protect against data corruption, it’s not 100% reliable.

### 3.4 Handshake
![Alt text](https://github.com/frhan/frhan.github.io/blob/master/assets/screenshot/uds/uds-2.png?raw=true "a title")

