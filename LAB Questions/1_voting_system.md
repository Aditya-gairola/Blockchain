# Voting System with Multiple Candidates
We create a contract where multiple candidates (identified by name) compete for votes. We use a mapping(address => bool) to ensure each address votes at most once
, and a mapping(uint => Candidate) (or array) to track vote counts. The vote function checks with require that the voter hasn’t voted yet and that the candidate exists. Key points:
  - Structs and mappings: We define a Candidate struct and map uint IDs to Candidate. We also map each voter address to bool hasVoted.
  - One-vote enforcement: Before accepting a vote, we use require(!hasVoted[msg.sender], "Already voted"); to block repeat votes.
  - Vote counting: When a vote is cast, we increment the candidate’s voteCount and mark the voter as having voted.

 ## Code
 ```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract VotingSystem {
    struct Candidate {
        string name;
        uint voteCount;
    }

    mapping(uint => Candidate) public candidates;  // candidate ID to Candidate
    uint public candidatesCount;
    mapping(address => bool) public hasVoted;     // track if an address has voted

    // Set up the candidates in the constructor
    constructor(string[] memory candidateNames) {
        // Initialize candidates with given names
        for (uint i = 0; i < candidateNames.length; i++) {
            candidates[i] = Candidate(candidateNames[i], 0);
        }
        candidatesCount = candidateNames.length;
    }

    // Allow an address to vote for a candidate by ID (only once)
    function vote(uint candidateId) public {
        require(!hasVoted[msg.sender], "Address has already voted");  // only one vote per address
        require(candidateId < candidatesCount, "Invalid candidate ID");
        hasVoted[msg.sender] = true;
        candidates[candidateId].voteCount++;
    }

    // View function to get details of a candidate by ID
    function getCandidate(uint candidateId) public view returns (string memory name, uint votes) {
        require(candidateId < candidatesCount, "Invalid candidate ID");
        Candidate storage c = candidates[candidateId];
        return (c.name, c.voteCount);
    }
}
```
## Deloyment 
### Connecting to wallet

![Screenshot from 2025-05-19 15-43-56](https://github.com/user-attachments/assets/6ff86904-5fe8-430b-a955-c7e5291e7800)

### Deploying

 ![Screenshot from 2025-05-19 15-46-21](https://github.com/user-attachments/assets/5d94c454-b168-4264-9a11-d1c35bb324d7)

 ![Screenshot from 2025-05-19 15-46-35](https://github.com/user-attachments/assets/5e6f9b3f-0779-4d72-8b7e-82ffcd49f17f)





