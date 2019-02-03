# Overview

## The Problem

In a nutshell: we believe the Internet of Things could be much more useful
if sensors, actuators, displays and other IoT "Things" could simply (and
securely) talk to each other on the local WiFi network. Without requiring
much configuration, without going through some vendor's cloud, and certainly
without invading the user's privacy. And open for anybody to connect to.

Read more about [the problem](problem.md) we want to solve.

## The Architecture

There are three basic ideas:

1. Things on the local WiFi network publish new information (such a sensor values)
   through DNS Service Discovery broadcast messages. Things also listen to this
   type of message from other Things, and potentially take action based on what
   they hear.

2. Things can find out more about other Things, and interact with them based
   on metadata that each Thing publishes on the local network via HTTP.

3. Each Thing has its own a public/private key pair. The public key is published
   to the network, and the private key is kept secret. Outgoing messages
   are signed with the private key, and potentially encrypted with the
   intended recipient's public key.

This is simple, has low latency, takes very little network bandwidth or energy,
requires minimal setup, and provides confidentiality and authenticity where
needed.

Read more about [the architecture](architecture.md) and why we think these
basic ideas are good ones.

## Example Use Cases

* A touchscreen Thing tracks the comings and goings of Things on the local
  network, and enables the user to interact with each Thing
* A button Thing, and a door lock Thing collaborate to allow the resident
  to open the front door without concerns that a hostile Thing does this
  without permission.

## The specs

* [Secure Decentralized Ambient Synchronization](sdas/index.md)
* [Keys](keys/index.md)
* [Thing Metadata](metadata/index.md)

Note: these are early drafts, in the spirit of "release early and release often".
and we are well aware that important pieces have not been defined yet
(example: secure provisioning).

## Credits

The core ideas come from:

* Peter Hoddie's [Decentralized Ambient Synchronization](http://blog.moddable.com/blog/das/),
  which proposes to use mDNS to publish IoT data with little latency or overhead.
* Johannes Ernst's [Light-Weight Digital Identity (LID)](https://en.wikipedia.org/wiki/Light-Weight_Identity),
  which used GPG key pairs behind URLs for human-to-machine and machine-to-machine internet identity.
* [Mozilla's Web of Things](https://github.com/mozilla-iot/wot) specification, which
  has Things publishe rich metadata about themselves via HTTP.
