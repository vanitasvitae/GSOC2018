# Summer of Code 2018 - OpenPGP for XMPP Instant Messaging in Smack

This is the project page for my Summer of Code project 2018. As you can read in the title, my project is about an implementation of OpenPGP for XMPP (short: OX) in the XMPP client library Smack.

OpenPGP for XMPP is specified in XEP-0373 and XEP-0374, where 373 specifies general building blocks, while the latter describes the usage profile for instant messaging (OX-IM).

## smack-openpgp, smack-openpgp-bouncycastle and pgpainless

The code for my OX implementation is currently split in two modules:
* smack-openpgp contains classes which are independend from the OpenPGP backend. It consists of extension elements and providers, as well as manager classes which handle the OX workflow. It also 
defines a set of interfaces, which can be implemented by backend implementations like smack-openpgp-bouncycastle.
* smack-openpgp-bouncycastle on the other hand contains implementations of interfaces from smack-openpgp, as well as bindings to pgpainless. Its main purpose is to provide the cryptographic 
functionality which is missing from smack-openpgp. Ideally there would be multiple of such backend implementations available at some point (out of scope for GSoC).
* [pgpainless](https://github.com/vanitasvitae/pgpainless) is my fork of [bouncy-gpg](https://github.com/neuhalje/bouncy-gpg). It is my API for OpenPGP which internally uses 
[BouncyCastle](https://www.bouncycastle.org/). The plan is to make pgpainless as easy to use as possible, so that it can be incorporated in other (also non-Smack) projects that want to implement
OpenPGP for XMPP.

## Code

You can find the code I'm working on in the following repositories:

* [Smack](https://github.com/igniterealtime/Smack): Progress can be found in the openpgp branch 
in my [fork](https://github.com/vanitasvitae/Smack/tree/openpgp).
* [pgpainless](https://github.com/vanitasvitae/pgpainless): In order to implement OpenPGP 
functionality for Smack, I forked the project 
[bouncy-gpg](https://github.com/neuhalje/bouncy-gpg) and made some modifications.

## Demo client

I created a small command line client which demonstrates the capabilities of my OpenPGP API for Smack.
You can find it [here](https://github.com/vanitasvitae/oxclient). Enjoy testing :)
