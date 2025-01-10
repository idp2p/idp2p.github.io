# idp2p

> `Experimental`, inspired by `ipfs`, and `keri`

## Background

See also (related topics):

* [Decentralized Identifiers (DIDs)](https://w3c.github.io/did-core)
* [Key Event Receipt Infrastructure](https://keri.one//)
* [DIDComm](https://didcomm.org/)
* [IPFS](https://ipfs.io/)


## Problem

> `Alice` has a secret message for `Bob`, but she doesn't know who `Bob` is or where he is. 

DIDs and DIDComm solve this by providing decentralized identifiers that include service endpoints and mediator support,
enabling Alice to discover Bob's DID and securely send her message through these endpoints.
This allows communication without needing to know Bob’s personal details or his physical and network location in advance.

KERI (Key Event Receipt Infrastructure) enables a truly decentralized, ledger-independent identity system by managing identities through secure, self-sovereign keys and event-based updates

This ensures that Bob’s identity is secure and independent, free from centralized registries.

However,

- How to notify keri events to subscribers(witness)
- How to deliver or broadcast a message to subscribers(pubsub)
- Bonus: How to utilize by webassembly in identity area 

## Solution(idp2p)

### ID

> What is an identity and its features 

#### Values

> What are the values an identity has

#### WebAssembly

> Why using WebAssembly for KERI

- Deterministic 
- Security and Isolation
- Portable(You don't need to install new software, just download binary and use it)
- Language Agnostic(You can use another language for different versions)
- Multiple Concurrent Versions

### P2P

## idp2p

![w:5-1000](idp2p-diagram.png) 

## Demo