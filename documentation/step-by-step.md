---
layout: page
title: PWOSPF Step-by-Step Specification
---

## Requirements

* Maintain a view of the topology;
* Broadcast HELLO packets to maintain a list of neighbours;
* On change, flood the view of the network;
* Run Djikstra to compute the shortest path.

## 1) Define a topology

<img src="{{ site.baseurl }}/images/tp2.jpg" style="width: 600px;"/>

* 2 switches
* 2 hosts
* 2 controllers (same as hosts)

## 2) Send basic traffic

* Send traffic by hand, without PWOSPF;
* Need to install forwarding rule in dataplane (through mininet);
* ping H1 to H2.

## 3) Controller

* Controller program to install rules;
* Controllers are threads in mininet;
* 1 controller per switch;
* To statically install a forwarding rule, use switch.addRule.

## 4) Compute rules instead of hard code them

* Data structure for topology (matrix, ...)
* Compute nearest neighbours;
* Stub out parsing, sending, receiving of PWOSPF;
* Run Djikstra on topology;
* Install rules.

## 5) Send packets (HELLO) ==> Who are our neighbours?

* Define packet format with Scapy;
* To send, use sendp();
* To receive, sniff on interface (provided by mininet);
* Data plane code to handle broadcast or Controller sends 1 packet per interface;
    * Step 1: control plane sends to everyone;
    * Step 2: broadcast in the data plane.  
* Parse packet and populate topology.

## 6) Timeouts

* Generate HELLOs at Timeouts;
* Handle Timeouts ==> link down.

## 7) LSU packets

* Build the graph, running Djikstra;
* Flood to everyone;
* Drop if it is your own;
* Parse responses;
* Build topology.

