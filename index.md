# Summer of Code 2018 - OpenPGP for XMPP Instant Messaging in Smack

This is the project page for my Summer of Code project 2018. As you can read in the title, my project is about an implementation of OpenPGP for XMPP (short: OX) in the XMPP client library 
[Smack](https://github.com/igniterealtime/Smack).

OpenPGP for XMPP is specified in [XEP-0373](https://xmpp.org/extensions/xep-0373.html) and [XEP-0374](https://xmpp.org/extensions/xep-0374.html), where 373 specifies general building blocks, while 
the latter describes the usage profile for instant messaging (OX-IM).

## Smack-openpgp and PGPainless

The code for my OX implementation is currently split in two projects:

* smack-openpgp contains the OX and OX:IM implementation for Smack. It consists of extension elements and providers, as well as manager classes which handle the OX workflow.
I designed an easy to use API, which gives client developers the oportunity to quickly implement OpenPGP encrypted instant messaging. My implementation is capable of public key exchange over PubSub,
encrypted secret key exchange between the users devices, as well as general encrypted messaging with signature verification. The user also has the option to easily generate fresh OpenPGP keys (RSA, 
ElGamal, EC).
* [PGPainless](https://pgpainless.org) is my library for OpenPGP. It started as a fork of [bouncy-gpg](https://github.com/neuhalje/bouncy-gpg), but I quickly decided to start from scratch and write 
my own library. The result is my API for OpenPGP which internally uses [Bouncycastle](https://www.bouncycastle.org/). 
The plan is to make pgpainless as easy to use as possible, so that it can be incorporated in other (also non-Smack) projects that want to implement OpenPGP for XMPP (and other purposes as well).

## Code

You can find the code I'm working on in the following repositories:

* [Smack](https://github.com/igniterealtime/Smack): The code has been [merged](https://github.com/igniterealtime/Smack/pull/254) into Smacks master branch and can be found in the 
[smack-openpgp](https://github.com/igniterealtime/Smack/tree/master/smack-openpgp) module.
* [PGPainless](https://github.com/pgpainless/pgpainless)

## Demo client

I created a small command line client which demonstrates the capabilities of my OpenPGP API for Smack.
You can find it [here](https://github.com/vanitasvitae/oxclient). Enjoy testing :)

## Miscellaneous

During my work, I...

* made myself familiar with the [OpenPGP Specification](https://tools.ietf.org/html/rfc4880)
* detected a [bug in Bouncycastle](https://github.com/bcgit/bc-java/issues/348) which caused exported keys to have an invalid format by using a wrong checksum in unencrypted keys.
* detected [another bug in Bouncycastle](https://github.com/bcgit/bc-java/issues/381), which caused exported sub-keys to have a wrong package format, causing them to get lost on import.
* created a [small patch](https://github.com/bcgit/bc-java/pull/362) for an inconvenience in Bouncycastle.
* Did some formal work on XEP-0373 and XEP-0374 
([[1]](https://github.com/xsf/xeps/pull/621), 
[[2]](https://github.com/xsf/xeps/pull/634), 
[[3]](https://github.com/xsf/xeps/pull/644), 
[[4]](https://github.com/xsf/xeps/pull/669), 
[[5]](https://github.com/xsf/xeps/pull/670), 
[[6]](https://github.com/xsf/xeps/pull/683)).
* extensively [blogged](https://blogs.fsfe.org/vanitasvitae/category/gsoc-2018/) about my progress.
