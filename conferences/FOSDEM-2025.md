---
title: "FOSDEM 2025"
date: 2025-02-01
tags: ["conferences"]
image: "/images/placeholder.png"
---

# FOSDEM 2025

https://www.fosdem.org/2025/schedule/

## Saturday 2025-02-01

### Welcome

* FOSDEM was the 1st IPv6-only non-network large-scale conference
* Quote: _"Send us your anecdotes, e.g. if you met someone here at FOSDEM and got married."_
* https://FOSStodon.org/#FOSDEM
* February 1st is _Global Switch Day,_ from:
  * Twitter to Mastodon
  * Instagram to Pixelfeed
  * WhatsApp to Signal (or Threema!)
  * Facebook to Friendica
  * YouTube to PeerTube
  * TikTok to Loops.video
* Sponsored by Google, Red Hat, ARM, Block, Bloomberg, CNCF, Codethink, Colt, Element, dstny, Eclipse Foundation, Mozilla

### Logo

* Seymour Papert, Jean Piaget (Swiss), Marvin Minskey, Alan Key (Xerox PARC, _"A personal computer for children of all ages",_ 1972); MIT
* Speaker worked with Alan Key
* Turtle, making it physical is important
* Logo
* Smalltalk-80, Squeak open-sourced in 1996 by Alan Key, eToys; try [Squeak.js](https://squeak.js.org/etoys/)
* Scratch is #12 on TIOBE programming languages popularity

This is what got me started - a 100 years ago; Thank You, MIGROS Klubschule St.Gallen.

Believe it or not, but I still very much do and will always remember `maennli`, my very first program.

I think I was 8 years old.

### Creating an Open Knowledge Graph for Climate

* #semanticClimate Turn IPCC and COP climate documents into corpuse of semantic Linked Open Documents
* Driven by weekly public online presentations
* Open Knowledge Foundation #TheTechWeWant
* Mission: Create verifiable computable climate knowledge base
* KISS: No OWL, no Protégé; just RDF triples
* Visualization with NetworkX

<!-- TODO: ORDEM Open Research Dev, Ethics & Mobilization. -->

### Graph Databases after 15 years - where are they headed?

* Linked Data Benchmark Council (LDBC)
* Join Graph DBs, for people who don't like to `JOIN`
* Overfetching is when you grab too much, and filter on the client
* Underfetching is the opposite - but leads to the N+1 Query problem
* The root cause is the impedance mismatch of relational and object models
* 3 categories of Graph Databases
  * "MongoDB"-like (?) solve repeated joins to avoid N+1 query problem
    * OrientDB (2010), acquired by SAP, then abandoned; forked & lives on as ArcadeDB & YouTrackDB
    * Microsoft Cosmos DB (2017), with Gremlin as Query Language (QL), MongoDB API
    * Aeorospike (Gremlin), ... see Graph DBs on DBEngines
  * "Postgres"-like (?) solve recursive joins, with path queries
    * Neo4j
    * Titan / JanusGraph / HugeGraph - Gremlin QL: Apache, mostly maintained by Baidu
    * AWS Neptune
    * Google Cloud Spanner Graph
    * ...
  * "Teradata"-like (?) for Graph BI: Solve many-to-many joins, support Cyclic Queries, Triangle Queries, Acyclic queries
    * Kùzu (2023) with Cypher QL, sucessors of Graphflow & GrainDB
    * TigerGraph (2012) with GSQL
* Both single-node vs distributed & no/optional vs strict schema are orthogonal to above
  * but with schema can be more easily performance optimized
* New QLs
  * SQL/PGQ (SQL:2023) is inspired by Cypher, looks similar
  * GQL
* Chinese backed Graph DBs are leading LDBC benchmarks
* Interest is declining - but vendors are jumping on RAG

### atproto BoF (Bluesky)

* Introduction by Dietrich Ayala of https://webtransitions.org
* https://atptoto.com/guides/applications is a good start
* Self-hosting Personal Data Store (PDS) is now possible
* https://pdsls.dev browser for URIs with `at://` scheme

### 14 Years of systemd, by Lennart Poettering

* Intro: _"Lennart Poettering has the honour of having not one but several Linux distros created NOT to include his software."_ ;-)
* History: sysvinit, Upstart, Babykit, launchd
* UNIX: _"Everything is a file..."_ (but _"my printer is not a file!")_
* Adoption: Fedora 2011, openSUSE & Arch Linux 2012, RHEL & SLES 2014, Ubuntu 2015. _"The world runs on it."_
* People: 6 core maintainers, 60 (!) people with commmit access, >2600 contributors
* What: Suite of ~150 (!) separate binaries
* Footprint: 690K SLOC (wpa_supplicant ~460K, glibc ~1.4M)
* ... 😴
* Goals & Challenges for the Future:
  1. Address Boot & System Integrity
  1. Repivot systemd's IPC system, with more Varlink
  1. Rust. (But lack of dynamic libraries is a blocker.) Zig?
  1. Move image-based OSes into focus (`mkosi`)

### Building Local AI with a full-stack approach (Enzo)

* Survey
  * Q: Who used ChaptGPT and [Gemini](https://gemini.google.com)? A: Everyone.
  * Q: Who [ran an LLM locally](../ml/ollama1.md)? A: Almost everyone.
  * Q: Who training their own LLM? A: A few hands.
* Basics: Model parameters, Quantization
* Running Llama 3 70B fp16 needs...
  * 16x V100
  * 8x 4090
  * 6x A100
  * 4x A100:80gb
* NVIDIA NVLink connects GPUs (at 112.5 GB/s)
* [Jan.ai](https://jan.ai)
* [Ichigo](https://ichigo.homebrew.tld)

### Developing Custom UIs to Explore Graph Databases using Sigma.js

* [RIcardo project](https://ricardo.medialab.sciences-po.fr) from Science Po Paris, dataset of trades between 1830s - 1930s
* Visualization with the Neo4j Browser is useless, because too overwhelming
* Cytoscape.js better for schemas
* D3js better for smaller graphs
* Sigma.js great for rendering larger graphs
* [Let's use it!](https://github.com/jacomyal/2025-fosdem)

**[Coming](https://github.com/enola-dev/enola/tree/main/web/) to (my) [Enola.dev](https://enola.dev) real soon!**

### POSIX Signals in User Space on the Redox Microkernel

Redox, the microkernel-based OS written in Rust, explores _userspaceification_ of POSIX signal handling and IO.

## Sunday 2025-02-02

### Next Generation Internet 2025: where next?

Unclear if NGI EU program will be renewed as-is. Maybe in a different form.

Not a great presentation.

### [We need Disposable Digital Identities for a more secure and resilient digital society](https://fosdem.org/2025/schedule/event/fosdem-2025-6217-we-need-disposable-digital-identities-for-a-more-secure-and-resilient-digital-society/)

Self Sovereign Identity 🆔 with Verifiable Credentials 🪪 is coming to a Wallet near you, EU-wide, and in Switzerland, NEXT YEAR... interesting space? 🤔 

### DevPod

https://devpod.sh had a booth, and a chat with them VS https://www.gitpod.io (they touted their `devcontainer.json` https://containers.dev standard support; although [it seems that GitPod does also support it](https://www.gitpod.io/docs/flex/configuration/devcontainer)). I tried both:

* _GitPod Flex_ (new) is still AWS only, with GCP on waitlist (and personally I don't do AWS, only GCP)
* DevPod [didn't start for me on Fedora](https://github.com/loft-sh/devpod/issues/1410)

I've also explored just directly using [JetBrains Gateway](https://www.jetbrains.com/remote-development/gateway/) on a GCP GCE VM (which allows to choose the IntelliJ version), but I got stuck with SSH not working on Gateway (from a Chromebox). But even if that was fixed, manually need to create, start and remember to shutdown the VM, and manually dealing with ephemeral chaging IPs on VM restarts, as required by this approach, is more cumbersome than DevPod, which handles of this.

Alternatively, one could use [Google Cloud Workstations](https://cloud.google.com/workstations), but that does not support Dev Containers, so one would need to maintain custom workspace set-up scripts (and ituses an older fixed IJ which [I couldn't upgrade](https://issuetracker.google.com/issues/394350437)).

GitHub Codespaces is the simplest, of course; but does not support IntelliJ, anymore.

### NLnet

I've listened in to a BoF of NLnet, and was impressed by the energy there.

### Nostr

I've [spent some time at the Nostr booth](https://njump.me/nevent1qqsdweruuevw4ktqngh9hkekhr8c7tj4gtpz798qt458l8x7ddm435qppemhxue69uhkummn9ekx7mp0qgs0l09hq60h4fwkmvffavu70k9f0z2xd5j45cmm4s0tlpshkpt5q3qrqsqqqqqp574jdf) to better understand what they're up to, and from what I've learned so far, quite like what I've heard!

I'm wondering if there's something to be done with a generic RDF Nostr kind, and how this may relate to Solid. Could Nostr relays be Solid Pods?!

The simplest way to get started being on Nostr seems to be to [install Amethyst](https://www.amethyst.social) (or try another [Nostr client](https://nostr.net/)).

You can follow me by searching for `npub17vyw6y9fht9t6d3ywc3gpujvs7t354qls76thek47f4rqlfjpcmsaqvmsw`.
