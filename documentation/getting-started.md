---
layout: page
title: Getting Started
---

You will use the [P4 language](http://p4.org) to implement the data plane of
your internet router. Note that there are two versions of the language, P4\_14
and P4\_16. For this course we will use P4\_16. You should familiarize yourself
with the [P4_16 specification](https://p4.org/p4-spec/docs/P4-16-v1.1.0-spec.html).
You should implement the control plane with Python, and use
[P4Runtime](https://p4.org/p4-runtime/) to communicate with the switch.


## Tools

* [P4C](https://github.com/p4lang/p4c) is the reference compiler for the P4
  language.
* [BMV2](https://github.com/p4lang/behavioral-model) is a software switch that
  runs P4 programs compiled with P4C.
* [Mininet](http://mininet.org/overview/) creates a virtual network running
  software switches and real user-space applications.
* [Scapy](https://scapy.readthedocs.io/en/latest/introduction.html) is a Python
  library for crafting and decoding raw packets. It also has utilities for
  sniffing and sending packets.
* [p4app](https://github.com/p4lang/p4app/tree/rc-2.0.0) is a tool for running
  P4 programs on a Mininet topology. It includes all the dependencies for
  compiling, running and testing your programs: P4C, BMV2, Mininet and Scapy.


## How to run p4app on Mac OSX:

* **Install homebrew & cask:**

```
xcode-select --install
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew install caskroom/cask/brew-cask
```


* **Install docker-toolbox:**

```
brew cask install docker-toolbox
```

* **Install git:**

```
brew install git
```

* **Clone p4app github repo:**

```
git clone --branch rc-2.0.0 https://github.com/p4lang/p4app.git
```


* **Make p4app command available:**

```
ln -s &lt;PATH_TO_P4APP_REPO&gt;/p4app/p4app /usr/local/bin/p4app
```

* **Launch docker quickstart terminal:**

```
open -a Docker\ Quickstart\ Terminal -j
```

* **Run program through p4app:**

```
p4app run &lt;PROG_NAME&gt;.p4app/
```
