---
id: what-is-makeos
title: What Is MakeOS?
sidebar_label: What is MakeOS?
---

# What is MakeOS

**MakeOS** is the designation for a network of computers that work together to allow open-source software developers to create, contribute, distribute, socialize and govern source code without relying on a single, powerful central authority.

MakeOS provides a network and globally accessible storage layer for the git protocol — Allowing anyone to contribute to and access repositories they care about easily, at any time and without needing to go through a single trusted party. No one can prevent MakeOS users from collaborating; MakeOS protocol and client ensure that developers can run their own git remote server or connect to thousands of remote servers without losing their identity and data in the process.

The git technology changed the way developers collaboratively build software today; It allows developers to asynchronously contribute to a shared codebase, with little friction and from anywhere. Fundamentally, git is decentralized; It promotes the replication of repositories across the computers of collaborators allowing users to work offline, with little to no coordination required.

However, it is not very easy for many collaborators working on a shared project to set up and manage their own servers. 

## Supplementary Layers

Git enabled open source developers to build together in ways not seen before. With this success, the software development community grew so much and created layers and tooling with git as a dependence while not respecting the decentralized nature of the git tool. An example of this abnormality is in the storage of git objects. Due to the lack of a network, collaboration and storage protocols, centralized corporations now provide these layers at a cost to users. Users making use of these providers, do not own their data. They cannot move their collaborative data between competing platforms. They can be censored and kicked out at any time.

The MakeOS protocol adds some of the missing layers to give collaborators back their freedom without changing their current workflows or forcing them to learn new behaviours. The protocol provides the following layers:

### Global State Machine Layer

The state machine layer provides a medium for collaborators to store state that relates to a repository. It servers as the source of truth for information about any repository that exists on the network. With it, collaborators can create identities, store and query the state of branches and references. Other layers depend on the state machine to provide high-level services. MakeOS state machine is backed by a blockchain built on top of Tendermint core.

### Network Layer

Many software collaborators cannot run their own server due to the technical or financial cost involved, so they resort to using centralized, free server providers and accept the challenges with these services. The problem could have been resolved if git provided network capabilities that allowed the git client to connect to a vast network, learn about new updates and pull from the network without requiring users to have an always-on git server. MakeOS provides such a network — Anyone can join it, query it and request for git objects. There is no need to have a server that needs to be always on. The protocol supports asynchronous collaboration which allows collaborators to just commit, push and close their computer — fire and forget.

### Storage & Replication Layer

The MakeOS protocol provides an overlay distributed hash table network for storing and providing git objects across the network. Use the impressive [Kademlia DHT](https://github.com/libp2p/go-libp2p-kad-dht) that powers the IPFS and Filecoin network. Every node on the network connects to this DHT to either provide git objects or request using a git object streaming protocol similar to [Bitswap](https://docs.ipfs.io/concepts/bitswap/). The protocol mandates that all objects must be stored by a network participant known as _Host_. A host is responsible for keeping git objects permanently. They are challenged from time-to-time to ensure objects are being stored. They are also incentivized via block inflation to perform this service to the network. The Host is critical to allowing collaborators to contribute asynchronously and to push updates to a repository with confidence, knowing that their updates are publicly accessible to the people that care about them.

### Social Layer

Git does not include a protocol for managing discussions, issues, reviews and pull requests. These are layers that collaborators have come to rely on and a major reason why they are increasingly getting trapped in centralized collaboration platforms — a string vector for platform lock-in. MakeOS protocol makes use of git protocol to create a structure that allows social components to be built right into a repository. MakeOS post protocol can convert git’s branch system into a discussion board, an issue tracker, a merge request or a review. With the Kit client, users can create issues and merge request within a repository and share them by simply pushing to a remote. Since all social data reside in a repository, users can confidently migrate between remote service and tooling providers without the fear of losing anything — This is the way.

### Governance Layer

Developer communities can be fragmented or destroyed when the governance structure is not clearly defined, understood and adhered to. As open source collaboration continues to grow, a well-defined governance structure will increasingly be demanded. Centralized collaboration platform offer tools that enable only the owner of a repository to control all aspect of a project. Contributors have no say; They cannot collectively contribute to the decision-making process and can only do so if the project owner’s leadership style is democratic. Additionally, any governance structure on a centralized platform is an illusion as the platform owners can overrule at any given time. MakeOS allows collaborators to define how they want to govern themselves. The protocol allows ownership to be distributed to thousands of people who can collectively decide how repositories resources are utilized.

### Monetary Layer

On MakeOS, repositories become more; They are no longer just a place for storing source code. They become a sovereign entity, with an identity that is controlled by many people across the world via the governance layer. The repository becomes an unstoppable entity that can own resources that may have a monetary value. It can receive or send out monetary value. It can own digital currencies, receive donations, receive network rewards and will depend on its governance configuration to determine how the resources are managed.

## Why Is MakeOS Important?

We started MakeOS as a reaction to issues we find troubling around the world’s ability to create openly and transparently on centralized platforms. We believe that many also share the same sentiments. Some of them are:

### Centralization

Today, most open source development, collaboration, distribution and coordination are carried out within platforms that are closed. Platforms that are profiting from the success of open source but do not completely share the ideals open source was built on. Platforms that are increasingly introducing features that appear useful but lock-in developers and limit their ability to migrate. Platforms that will sell and push out collaborators at the request of third-party agents. Platforms that have historically been against open source but are now reformed. We have seeded control and the future of open source to entities that are designed to increase shareholders value and will throw us under the bus if asked by a higher authority. We are building tools, services and integrations with entities that become a dangerous point of failure when they go down, leading to complete halt of operations and disruption of workflows. This arrangement is risky for open source.

### Censorship

Code is free speech and should not be censored. But that is an opinion that can only be true if we can express ourselves without a central authority deciding what we can and cannot do. As long as we continue to rely on shareholder-driven entities that are grounded in jurisdictions where third-party authorities can force these platforms to do their will, we cannot expect to be free to create code, share it to whomever we want and socialize around it. The issue of censorship does not only entail our ability to code what we want but also our ability to socialize with communities on these platforms.

### Ownership & Governance

Historically, ownership structure on the internet has typically been defined as one user owning a resource and adding other users as members or admins to help in managing the resource — Most service providers allow only one user to own an account and manage it. This kind of ownership system makes it impossible to truly create shared, community-owned open source services where the community can co-create, co-govern and co-own important software products together. Instead what we have is a system that allows one person to become the authoritative owner and decision-maker of a project and not allowing other collaborators have a say. It is useful for collaborators to collectively own a repository, its content, its users and also its community. Although disagreeing collaborators can create a clone, it is not possible to clone both a project and community on any centralized code hosting platform. Contributors to critical open-source software must have the ability to share ownership to ensure balanced governance, shared interest, performance, continuity and security.

### Sustenance

Open source has grown so much that it is used in almost every organization in the world today — Open is very popular and successful. However, if open source is to continue succeeding we need to talk about sustaining the people contributing to its success. We need to find ways to incentivize continuous contribution of time, energy and intellect to help projects maintain or improve their quality. Developers building the tools, libraries, reporting and fixing bugs and writing documentations need to eat! — We must create a path for them to capture some value and support themselves.

## Target Features

At various stages of release, MakeOS will offer the following features which will enable collaborators conveniently move away from a system that aims to limit their freedom:

* Host your repositories — Create globally accessible, highly available git repositories.
* Merge request management.
* Issue management.
* Gateways — For browsing and querying all repositories.
* Distributed Ownership — allowing many people to truly shared a project.
* Cryptocurrency — for network incentivization and repository finance.
* Repository Accounting — Receive, send and manage funds. 
* Repository Sponsorship.
* Custom governance engine. 
* Actions — Self-hosted CI/CD & Custom blockchain logic execution.
* Release & Dependency Management.
* Task management. 
* Open Source Sustenance — by incentivizing repository dependencies.  

