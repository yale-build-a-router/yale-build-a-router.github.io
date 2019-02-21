---
layout: page
title: Getting Started Guide
---

## How to run p4app on Mac OSX:

* **Install homebrew & cask:**

    xcode-select --install

    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

    brew install caskroom/cask/brew-cask

* **Install docker-toolbox:**

    brew cask install docker-toolbox

* **Install git:**

    brew install git

* **Clone p4app github repo:**

    git clone --branch rc-2.0.0 https://github.com/p4lang/p4app.git

* **Make p4app command available:**

    ln -s &lt;PATH_TO_P4APP_REPO&gt;/p4app/p4app /usr/local/bin/p4app

* **Launch docker quickstart terminal:**

    open -a Docker\ Quickstart\ Terminal -j

* **Run program through p4app:**

    p4app run &lt;PROG_NAME&gt;.p4app/
