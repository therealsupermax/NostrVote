
# NIP-X: Decentralized Voting
## Motivation
The current voting systems often suffer from issues such as centralization, lack of transparency, and susceptibility to manipulation. By leveraging the decentralized nature of the Nostr protocol, we can create a voting system that is secure, transparent, and resistant to censorship. This proposal outlines a protocol for conducting decentralized elections using Nostr, enabling users to cast votes in a verifiable manner while maintaining their privacy. [Max] we can now vote from our phones, securely 


## Specification

1. Key Concepts
Public/Private Key Pair: Each voter generates a unique public/private key pair. The public key serves as the voter's identity, while the private key is used to sign votes.

Vote Object: A vote is represented as a JSON object containing the following fields:
[election_id]: A unique identifier for the election.
[candidate]: The public key of the candidate or option being voted for.
[timestamp]: The time the vote was cast.
[signature]: The cryptographic signature of the vote, created using the voter's private key.

2. Vote Casting
To cast a vote, a voter must perform the following steps:

a) Generate Key Pair: If not already done, the voter generates a public/private key pair.
b) Create Vote Object: The voter creates a vote object with the necessary fields.
c) Sign Vote: The voter signs the vote object using their private key.
d) Broadcast Vote: The signed vote object is sent to one or more Nostr relays for distribution.

3. Vote Structure
A vote object must adhere to the following JSON structure:

// json
```
{
  "election_id": "string",
  "candidate": "string",
  "timestamp": "integer",
  "signature": "string"
}
```


4. Broadcasting Votes
Votes are broadcasted to Nostr relays using the standard Nostr message format.
Each relay must accept vote objects and propagate them to other connected relays.

6. Vote Verification
To verify a vote, any participant can:
• Retrieve the vote object from the relay.
• Check the signature against the voter's public key to ensure authenticity.
• Confirm that the vote was cast within the election period.

7. Vote Counting
Votes can be counted by any participant in the network. The counting process involves:

• Collecting all vote objects for a specific election_id.
• Aggregating the votes for each candidate.
• Publishing the results on the Nostr network for transparency.

7. Security Considerations
• Anonymity: The protocol ensures that votes are anonymous while allowing for verification of eligibility.
• Double Voting Prevention: Each vote must include a unique election_id and timestamp to prevent double voting.
• Relay Trust: While the protocol is decentralized, users should be aware of the trustworthiness of the relays they connect to.


## Examples
• Example Vote Object
A sample vote object might look like this:

// json
```
{
  "election_id": "election_2023",
  "candidate": "candidate_public_key_here",
  "timestamp": 1633036800,
  "signature": "abcdef1234567890..."
}
```



• Broadcasting a Vote
A voter would broadcast their vote to a Nostr relay as follows:

// python
```
import websocket
import json

vote = {
    "election_id": "election_2023",
    "candidate": "candidate_public_key_here",
    "timestamp": 1633036800,
    "signature": "abcdef1234567890..."
}

ws = websocket.WebSocket()
ws.connect("wss://your_nostr_relay_url")
ws.send(json.dumps(vote))
ws.close()
```




This NIP proposes a decentralized voting protocol using the Nostr framework, enabling secure, transparent, and verifiable elections. By leveraging public/private key cryptography and the decentralized nature of Nostr, we can enhance the integrity of the voting process and empower users to participate in democratic decision-making.

Code
Below is link to simple web app example code, viewable in any browser
[here]([https://](https://github.com/therealsupermax/NostrVote/blob/main/voting_app.html))

