### Selective Disclosure Trie

> Inspired by Merkle Patricia Trie

#### Problem

As the saying goes, "Great deceivers do not lie", in other words, small deceivers try to deceive people by lying. While the truth may reveal a part of reality, it does not always provide a complete picture of the whole.

To illustrate this problem, consider the following analogy:

> Alice:  Bob, just tell me the truth. Do you swear that you love me?

> Bob:  I swear, I love you.


> Eve: Bob, just tell me the truth. Do you swear that you love me?

> Bob: I swear, I love you.

To avoid this situation, Alice would need to ask Bob to "prove that she is the only one in his heart". However, Bob would not want to completely open up his heart, because the fact that Alice is in his heart only concerns Alice, and furthermore, who his friend is doesn't concern Alice at all. As a result, Bob would need to prove that the love compartment in his heart belongs only to Alice.

In the digital world, let's propose a solution for this analogy related to privacy and proof of uniqueness.

#### Solution

The SDT is a solution proposal that expresses personal information with a data structure called a trie, similar to a Merkle tree. SDT provides two key features; selective disclosure and proof of non-existence.

SDT creates a root proof similar to a `Merkle Tree` but its branches have keys like `Merkle Patricia Trie`. A branch node's proof is obtained from the proofs of its child nodes. As an example, the proof of the following tree is a summary of the ordered JSON data consisting of the `personal` and `addresses` proofs. The proof of a leaf node is the hash of salt and value. Consider the following information:


```json
{
   "personal": {
     "name": "Adem",
     "surname": "Çağlın"
   }
   "addresses": {
     "work": {
        "city": "A City",
        "zipcode": 123456
      }
   }
}
```

The pseudocode for generating proofs from this information is as follows:

```javascript 
root_proof = hash({ "addresses": "<proof>", "personal": "<proof>" })

personal_proof = hash({ "name": "<proof>", "surname": "<proof>" })

name_proof = hash({ "value": "Adem", "salt": "0x.." })

// Not: hash method is sha-256 and byte encoding is hexadecimal

``` 

This proof, similar to a Merkle root, represents a summary of all information, thus ensuring data integrity. So how is selective disclosure possible? For example, consider a verifier who only needs the person's name. SDT expresses this query using a GraphQL-like query structure:

```graphql
{
  personal {
    name
  }
}
```

This query produces a result that reveals only the person's name, but also provides proofs for `surname` and `addresses`:


```json 
{                                                                 
  "addresses": "0x.."                                                   
  "personal": {                                                  
      "name": { "value": "Adem", "salt": "0x.." },                                                                                
      "surname": "0x.."
   }                                       
}
```
Now, let's discuss how proof of non-existence is achieved. Suppose a verifier wants to see the person's phone number.

```graphql
{
  phones {
    cell
  }
}
```
In this case, the owner can prove that they don't have a phone number as follows:

```json 
{                                                                 
  "addresses": "0x.."                                                   
  "personal": "0x.."                                     
}
```

You can visit the following links to get more details:

Playground: https://tudnme.csb.app/

Rust implementation: https://github.com/idp2p/sdt

