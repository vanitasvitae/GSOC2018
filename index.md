# Summer of Code 2018 - OpenPGP for XMPP Instant Messaging in Smack

This is the project page for my Summer of Code project 2018. As you can read in the title, my project is about an implementation of OpenPGP for XMPP (short: OX) in the XMPP client library 
[Smack](https://github.com/igniterealtime/Smack).

OpenPGP for XMPP is specified in [XEP-0373](https://xmpp.org/extensions/xep-0373.html) and [XEP-0374](https://xmpp.org/extensions/xep-0374.html), where 373 specifies general building blocks, while 
the latter describes the usage profile for instant messaging (OX-IM).

## Smack: smack-openpgp

The major part of my GSoC project is an OX:IM implementation for the XMPP client library Smack. This was done as the Smack module *smack-openpgp*, which contains an implementation of XEP-0373 and XEP-0374. It consists of XMPP extension elements and providers, as well as manager classes which handle the OX workflow.

I designed an easy to use API, which gives client developers the oportunity to quickly implement OpenPGP encrypted instant messaging. My implementation is capable of public key exchange over PubSub,
encrypted secret key exchange between the users devices, as well as general encrypted messaging with signature verification. The user also has the option to easily generate fresh OpenPGP keys (RSA, 
ElGamal, EC) through PGPainless.

During the project, I created a bunch of JUnit and Integration tests to ensure correct functionality.

My code has already been [merged](https://github.com/igniterealtime/Smack/pull/254) into Smacks master branch and can be found in the [smack-openpgp](https://github.com/igniterealtime/Smack/tree/master/smack-openpgp) module.

## PGPainless
The second big part of my project is PGPainless.

![PGPainless logo](https://avatars1.githubusercontent.com/u/41373830?s=400&u=55ee07cd4f9d4ba4f27ca90b95304757a7b0f902&v=4  "PGPainless Logo")

[PGPainless](https://pgpainless.org) is my library for OpenPGP. It started as a fork of Jens Neuhalfens [bouncy-gpg](https://github.com/neuhalje/bouncy-gpg), but I quickly decided to start from scratch and write my own library. This quickly grew into a standalone project ([https://pgpainless.org](https://pgpainless.org)), which I will thrive to extend further. As I understand, there is a need for easy to use OpenPGP libraries for Java and Android. In fact, Android compatibility was one of the reasons to start from scratch instead of going with existing implementations.

PGPainless is based around [Bouncycastle](https://www.bouncycastle.org/), but it provides an easy to use API, which allows to execute cryptographic actions without touching any bouncycastle code at all.
The plan is to make pgpainless as easy to use as possible, so that it can be incorporated in other (also non-Smack) projects that want to implement OpenPGP for XMPP (and other purposes as well).

## Demo client

I created a small command line client which demonstrates the capabilities of my OpenPGP API for Smack. It is able to generate user keys, restore existing secret key backups from pubsub, and obviously exchange encrypted messages with other users.

You can find it [here](https://github.com/vanitasvitae/oxclient). Enjoy testing :)

## Contributions to other projects

During my work, I...

* detected a [bug in Bouncycastle](https://github.com/bcgit/bc-java/issues/348) which caused exported keys to have an invalid format by using a wrong checksum in unencrypted keys.
* detected [another bug in Bouncycastle](https://github.com/bcgit/bc-java/issues/381), which caused exported sub-keys to have a wrong package format, causing them to get lost on import.
* created a [small patch](https://github.com/bcgit/bc-java/pull/362) for an inconvenience in Bouncycastle.
* Gave feedback and did some formal work on XEP-0373 and XEP-0374 ([[1]](https://github.com/xsf/xeps/pull/621), [[2]](https://github.com/xsf/xeps/pull/634), [[3]](https://github.com/xsf/xeps/pull/644), [[4]](https://github.com/xsf/xeps/pull/669), [[5]](https://github.com/xsf/xeps/pull/670), [[6]](https://github.com/xsf/xeps/pull/683)).
* Tested my implementation against another experimental OX application and gave feedback.

## Blog Highlights
Throughout the whole GSoC period, I [blogged](https://blogs.fsfe.org/vanitasvitae/category/gsoc-2018/) extensively about my progress.

One of my personal favourites is my posting from [May 17th](https://blogs.fsfe.org/vanitasvitae/2018/05/17/summer-of-code-bug-found/), in which I explained a [bug in Bouncycastle](https://github.com/bcgit/bc-java/issues/348), that I found.

I'm also proud of my posting from [June 11](https://blogs.fsfe.org/vanitasvitae/2018/06/11/summer-of-code-evaluation-and-key-lengths/), in which I investigated OpenPGP message lengths depending on which key types are used.
![Diagram showing different message lengths depending on which algorithm is used](https://blogs.fsfe.org/vanitasvitae/files/2018/06/cipher_lengths1.png  "OpenPGP message lengths")
