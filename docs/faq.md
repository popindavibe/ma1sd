# Frequently Asked Questions
### This is all very complicated and I'm getting confused with all the words, concepts and diagrams - Help!
Matrix is still a very young protocol and there are a whole lot of rough edges.  
Identity in Matrix is one of the most difficult topic, mainly as it has not received much love in the past years.

We have tried our best to put together documentation that requires almost no knowledge of Matrix inner workings to get a
first basic setup running which relies on you reading the documentation in the right order:
- [The Concepts](concepts.md) in few words.
- [Getting Started](getting-started.md) step-by-step to a minimal working install.
- [Identity stores](stores/README.md) you wish to fetch data from.
- [Features](features) you are interested in that will use your Identity store(s) data.

**IMPORTANT**: Be aware that ma1sd tries to fit within the current protocol and existing products and basic understanding
of the Matrix protocol is required for some advanced features.

If all fails, come over to [the project room](https://matrix.to/#/#ma1sd:ru-matrix.org) and we'll do our best to get you
started and answer questions you might have.

### What kind of setup is ma1sd really designed for?
ma1sd is primarily designed for setups that:
- [Care for their privacy](https://github.com/kamax-matrix/ma1sd/wiki/ma1sd-and-your-privacy)
- Have their own [domains](https://en.wikipedia.org/wiki/Domain_name)
- Use those domains for their email addresses and all other services
- Already have an [Identity store](stores/README.md), typically [LDAP-based](stores/ldap.md).

If you meet all the conditions, then you are the prime use case we designed ma1sd for. 

If you meet some of the conditions, but not all, ma1sd will still be a good fit for you but you won't fully enjoy all its
features.

### Do I need to use ma1sd if I run a Homeserver?
No, but it is strongly recommended, even if you don't use any Identity store or integration.

In its default configuration, ma1sd uses other federated public servers when performing queries.  
It can also [be configured](features/identity.md#lookups) to use the central matrix.org servers, giving you access to at
least the same information as if you were not running it.

So ma1sd is like your gatekeeper and guardian angel. It does not change what you already know, just adds some nice
simple features on top of it.

### I'm not sure I understand what an "Identity server" is supposed to be or do...
The current Identity service API is more a placeholder, as the Matrix devs did not have time so far to really work on
what they want to do with that part of the ecosystem. Therefore, "Identity" is currently a misleading word and concept.
Given the scope of the current Identity Service API, it would be best called "Invitation service".

Because the current scope is so limited and no integration is done with the Homeserver, there was a big lack of features
for groups/corporations/organisation. This is where ma1sd comes in.

ma1sd implements the Identity Service API and also a set of features which are expected by regular users, truly living
up to its "Identity server" name.

### Can I migrate my existing account on another Matrix server with ma1sd?
No.

Accounts cannot currently migrate/move from one server to another.  
See a [brief explanation document](concepts.md) about Matrix and ma1sd concepts and vocabulary.

### I already use the synapse LDAP3 auth provider. Why should I care about ma1sd?
The [synapse LDAP3 auth provider](https://github.com/matrix-org/matrix-synapse-ldap3) is not longer maintained despite
saying so and only handles on specific flow: validate credentials at login.

It does not:
- Auto-provision user profiles
- Integrate with Identity management
- Integrate with Directory searches
- Integrate with Profile data

ma1sd is a replacement and enhancement of it, offering coherent results in all areas, which the LDAP3 auth provider
does not.

### Sydent is the official Identity server implementation of the Matrix team. Why not use that?
You can, but [sydent](https://github.com/matrix-org/sydent):
- [should not be used and/or self-hosted](https://github.com/matrix-org/sydent/issues/22)
- is not meant to be linked to a specific Homeserver / domain
- cannot handle federation or proxy lookups, effectively isolating your users from the rest of the network
- forces you to duplicate all your identity data, so people can be found by 3PIDs
- forces users to enter all their emails and phone numbers manually in their profile

So really, you should go with ma1sd.

### Will I loose access to the central Matrix.org/Vector.im Identity data if I use ma1sd?
No.

In its default configuration, ma1sd does not talk to the central Identity server matrix.org to avoid leaking your private
data and those of people you might know.

[You can configure it](features/identity.md#lookups) to talk to the central Identity servers if you wish.

### So ma1sd is just a big hack! I don't want to use non-official features!
ma1sd primary concerns are your privacy and to always be compatible with the Matrix ecosystem and the Identity service API.  
Whenever the API will be updated and/or enhanced, ma1sd will follow, remaining 100% compatible with the ecosystem.

### Should I use ma1sd if I don't host my own Homeserver?
No.

It is possible, but it is not supported and the scope of features will be extremely limited.
Please consider hosting your own Homeserver and using ma1sd alongside it.
