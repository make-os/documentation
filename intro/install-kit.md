---
id: install-lobe
title: Installation
sidebar_label: Install
description: >-
  Kit is the official reference client for interacting with the MakeOS network
  and blockchain. Depending on your platform, there are several ways to install
  it.
---

# Install

## Homebrew:

For macOS or Linux users, you can get Kit by using the [Homebrew](https://brew.sh/) package manager.

```bash
brew tap make-os/kit 
brew install kit
```

## Pre-built Binaries

For platforms with no support for Homebrew, you can download a pre-built binary from our GitHub [release](https://github.com/make-os/kit/releases) page.

There are binaries for macOS, Windows and Linux systems. Unzip the tarball file, add the `kit` or `kit.exe` executable in your PATH. 

{% hint style="danger" %}
Git is required and must be in your PATH. Git version must be &gt;= v2.11.0. Click [here](https://git-scm.com/downloads) to download and install the latest git release.
{% endhint %}

{% hint style="info" %}
**Add \`kit\` executable to your PATH**

Git interacts with Kit to perform signing and push operations. You must add**`kit`**to your system PATH to allow git to find it.
{% endhint %}

##  Build From Source

If you prefer to build from the official source, you can do this by downloading the source from [GitHub](https://github.com/make-os/lobe). 

You will need to install the following \[dependencies\]\(\#install-dependencies\) to successfully run the commands below.

```bash
# Fetch source using go get
go get github.com/make-os/kit

# Check into Kit's source directory
cd path/to/kit

# Install dependencies and build Kit
make install
```

## Install Dependencies

If you are building from source, you must have the following dependencies installed.

* Go \(go1.14 or later\)
* Git
* GNU Make

