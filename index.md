---
layout: default
---

# Time and Location

**Term:** Spring 2019

**Lectures:** 
   * Wednesday 1:30pm – 3:15pm, Friday 3:30pm – 5:15pm
   * 110-101 in the Main Quad

# Overview

Students will work in teams of two to build  a fully functioning Internet router. Students will design the control plane in Python on a linux host and will design the data plane in the new P4 language on a software switch switch. For the midterm milestone, teams must demonstrate that their routers can interoperate with the other teams by building a small topology utilizing everyone's router.

# Teams

The class will be broken down into teams of two students. One teammate will be responsible for the P4 data-plane implementation and the other teammate will be responsible for the Python control-plane. We leave it up to each team to decide how to they would like to divide up the workload amongst themselves. However, we highly encourge close collaboration and consulation so that each member is intimiately familiar with both aspects of the router implementation.

# Class Router Interoperation

Routers by nature work cooperatively in large complex environments. In fact, much of the complexity in router design and implementation is inter-operating with routers developed by different teams based on varying assumptions of standard protocol specifications. Inter-operation is such a critical feature of network infrastructure development that it is one of the major focuses of this course. For the midterm milestone, teams must demonstrate interoperability of thier router will all other teams' routers. The students are responsible for initiating communication between groups, coming up with a cooperative integration plan and ensuring that your routers inter-operate with all other routers in the class. It is our goal that every finished router will be able to route traffic cooperatively on a large shared topology.

We have reserved a portion of the total class points to allocate based on participation during inter-operation. This means that we expect all the students to be pro-active from the start about planning and communicating a solid inter-operation strategy between teams during development. It is a good idea to collectively map out a strategy early on in the quarter and have incremental goals that can tested piece-wise. You may meet during designated course hours (since not all lectures are held), use the class email, or meet during class hours.

# Documentation and Deliverables

This is a project based course. There is no midterm or final exam. There is a set of deliverables specified on the [course schedule]({{ site.baseurl }}/schedule). These deliverables are meant to function as milestones for the two main tasks of the quarter: (1) building an internet router, (2) your advanced features project. We will be using github extensively throughout the course. Each team will fork the starter code from a github repository and will add the instructors as collaborators on their forks. Teams will "submit" their deliverables by adding a tag to a specific commit, this will allow instructors to evaluate their work easily and efficiently, and it's also good code development practice.

In addition to the deliverables specified in the course schedule, teams are also asked to maintain a design document as a README file in their project directory. This document is the instructors' window into the team's design, so it is important to keep it up to date and organized. The design document may contain diagrams, pseudocode, flow charts, or whatever else might be helpful to explain the key design decisions to the instructors. Every Friday, starting *TBD*, instructors will review each teams design document to ensure that they are on track and making progress. A portion of the total points is reserved for these documentation checks.

Each team will give a 15 min presentation / demonstration at the end of the course explaining their advanced features project.


