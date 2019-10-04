---
layout: page
title: Building an Internet Router
---

One of the main goals of this course is to design and build a fully functioning internet router. This document is meant to serve as a high level overview of approach that we will take to do this.

# Tools

We will use P4 to implement the data-plane portion of the router. P4 abstracts away many of the low level details required for hardware development. One of the goals is for it to be usable by P4 developers with no prior HDL design experience.

The control-plane will be written in Python on top of the [Scapy](https://scapy.readthedocs.io/en/latest/) packet processing library. Scapy is a very flexible packet generator, sniffer, parser, and editor; and it is quite easy to use, making developers more productive.

# Approach

* Complete [Getting Started]({{ site.baseurl }}/deliverables/getting-started) deliverable to get everything that you will need set up.

* Review the protocols:
  * [PWOSPF]({{ site.baseurl }}/documentation/pwospf/)
    * IP - understand how a router makes a decision about forwarding an IP packet based on its routing table
    * ARP
    * ICMP
       
* Learn how to use P4 and Mininet:

    * [P4 Mininet exercises]({{ site.baseurl }}/deliverables/p4-mininet)

* Review the basic requirements for the data-plane and control-plane (see below).
* Develop an interoperability plan early! As a class, you will want to decide on a concrete plan to make sure that everyone's router will end up interoperable. We strongly suggest that the teams work together to do incremental tests of their implementations against each other. For example, after implementing the PWOSPF HELLO protocol, ensure that inter-team routers can successfully perform neighbor discovery before going on to develop the link state updates. Testing components individually provides a much saner debugging environment than a fully built system.

* Integrate your data-plane and control-plane implementations. Make sure to run some tests on your own design before attempting to build a multi-router topology. See the hints below for some example tests.
* Interoperate with otherstudents! As a class, you will need to prove to the instructor that all of your routers are in fact interoperable.
* Celebrate!


# Data-Plane Basic Requirements

* Provide a routing table that can store IP address/prefix pairs with their associated port and next-hop IP address.
* Use the routing table to perform a longest prefix match on destination IP addresses and return the appropriate egress port and next-hop address (or 0.0.0.0 for a directly attached destination). 
    * NOTE: We will use a ternary match table for the routing table because LPM tables are not fully supported by SDNet yet.
* Provide an ARP table that can store at least 64 entries. This will accept an IP address as a search key and will return the associated MAC address (if found). This table is modified by the software, which runs its own ARP protocol.
* Provide a “local IP address table”. This will accept an IP address as a search key and will return a signal that indicates whether the correspond address was found. This table is used to identify IP addresses that should be forwarded to the CPU.
* Decode incoming IP packets and perform the operations required by a router. These include (but are not limited to):
    * verify that the existing checksum and TTL are valid
    * look up the next-hop port and IP address in the route table
    * look up the MAC address of the next-hop in the ARP table
    * set the src MAC address based on the port the packet is departing from
    * decrement TTL
    * calculate a new IP checksum
    * transmit the new packet via the appropriate egress port
    * local IP packets (destined for the router) should be sent to the software
    * PWOSPF packets should be sent to the software
    * packets for which no matching entry is found in the routing table should be sent to the software
    * any packets that the hardware cannot deal with should be forwarded to the CPU. (e.g. not Version 4 IP)
* Provide counters for the following:
    * IP packets
    * ARP packets
    * Packets forwarded to the control-plane

# Control-Plane Basic Requirements

* Sending ARP requests
* Updating entries in the hardware ARP cache
* Timing out entries in the hardware ARP cache
* Queuing packets pending ARP replies
* Responding to ICMP echo requests
* Generating ICMP host unreachable packets
* Handling corrupted or otherwise incorrect IP packets
* Building the forwarding table via a dynamic routing protocol (PWOSPF)
* Support static routing table entries in addition to the routes computed by PWOSPF
* Handling all packets addressed directly to the router

# You Decide

* Responding to ARP requests is actually fairly straight forward to express in P4. You can decide whether you want to implement ARP responding in the control-plane or the data-plane.


# Hints and Tips

* Are you handling PWOSPF HELLO packets correctly in the data-plane? What IP address are they sent to?
* Be sure to make use of the CLI tool to add/remove/inspect table entries and read/write counters
* Possible initial tests:
    * Is your router forwarding correctly with statically configured table entries?
    * Can you ping each of the routers interfaces?
    * Is the router responding to ARP requests?
    * Be careful if you are trying to ping one interface from the other. Unless you are careful, linux will force the traffic to use the loopback interface rather than sending packets out onto the wire. [It is possible](https://serverfault.com/questions/127636/force-local-ip-traffic-to-an-external-interface) to do this, but it'll be easier (and less confusing) if you can arrange a time with a neighboring group to use their NIC. Then you can do small tests like sending pings through the router, traceroute to and through the router, send iperf flows through the router, and so on.
