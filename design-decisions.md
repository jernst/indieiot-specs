# Design Decisions

If you wonder why we made certain design decisions and not others,
please read on:

## Q: DNS-SD advertisements? Really?

Sounds a bit surprising, but why not?

* DNS advertisement are very efficient: a message often fits into a single
  network packet,and -- unless the payload is encrypted -- message traffic
  is independent of the number of listeners to the message.

* There is no overhead in negotiating a connection, or keeping a
  connection alive. If we used an HTTP POST, for example, TCP and then HTTP
  connection setup takes much longer, and has to be repeated one for each
  listener to the message.

* It's very straighforward to implement for solar or battery-powered devices that
  only communicate when they have sufficient energy: the devices comes alive,
  connects to the network, emits the packet, and goes back to sleep. Keeping
  TCP connections alive, for example, would take much more power.

* It's easy to develop with: mDNS browsers are commonly available, and
  they can be an excellent tool to follow along what's happening on the
  network and what values are currently emitted by a Thing.

## Q: Why are using using digital signatures and not HMACs for authenticity?

HMACs, or any other Message Authentication Code, require the sender and
the receiver of a message to have access to the same secret. Digital
signatures use a publicly shared key in combination with a secret,
never-shared private key. Only the public key is required to verify
a signature.

If we used HMACs, we would also have to come up with a method to securely
share the shared secrets, which would make the protocol much more complex.
Also, messages signed with digital signatures cannot be repudiated as
no other party has access to the private key.

## Q: Why all that JSON metadata?

We want to reduce the need for manual configuration as much as possible.
For example, if a display Thing can discover that a Thing on the network
is of type Button, and has two states called On and Off, the display
Thing can automatically show a digital representation of a switch; it
requires no configuration.

Over time, we expect that the metadata in the system will become ever
richer, as we come across more use cases in which more types of information
would be useful to have discoverable.
