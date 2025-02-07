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

However,

- How to resolve the decentralized id
- How to notify keri events to subscribers(witness)
- How to handle uniqueness of identity without witness
- How to send or broadcast a message to subscribers(pubsub)
- How to handle protocol changes and working with multi impl(webassembly)

## Solution(idp2p)

> 

### ID

> KERI implementation with webassembly



#### WebAssembly

> Why using WebAssembly for KERI

- Deterministic 
- Security and Isolation
- Portable(You don't need to install new software, just download binary and use it)
- Language Agnostic(You can use another language for different versions)
- Multiple Concurrent Versions

### P2P

## IdP2P

### Resolve

> Alice wants to connect Bob 

- Alice publishs a `Resolve` message with the topic(Bob's id)
- Bob's delegator or owner publishs a `Provide` with same topic, the Provide message has `provider peers` and `message_id` 
- Alice send a request to one of the provider peer in order to retrieve Bob's identity info
- When the provider sends response, Alice verifies the identity and store it


### Notify Event

> Alice has an keri event and she wants to notify her subscribers

- Whenever an identity event occurs, the identity owner publishs an event with own id topic
- When a subscriber receives the event, it verifies first then store the event

### Notify Message

> Alice wants to send a message to Bob


### Mediator Mechanism

> Alice needs a network agent in order to publishs and receives messages


![w:5-1000](idp2p-diagram.png) 

## Demo