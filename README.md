# Blockchain 

Q Create a voting system with multiple candidates. Each address can vote only once.

CODE 
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Voting {
    struct Candidate {
        string name;
        uint voteCount;
    }

    mapping(address => bool) public hasVoted;  // Tracks if an address has voted
    Candidate[] public candidates;  // Array of candidates

    // Add a new candidate
    function addCandidate(string memory _name) public {
        candidates.push(Candidate(_name, 0));
    }

    // Vote for a candidate by index
    function vote(uint candidateIndex) public {
        // Ensure the sender hasn't voted already
        require(!hasVoted[msg.sender], "You have already voted.");
        
        // Ensure the candidate index is valid
        require(candidateIndex < candidates.length, "Invalid candidate index.");
        
        // Ensure there are candidates to vote for
        require(candidates.length > 0, "No candidates available to vote for.");
        
        // Increment the vote count for the selected candidate
        candidates[candidateIndex].voteCount++;
        
        // Mark the sender as having voted
        hasVoted[msg.sender] = true;
    }

    // Get the list of all candidates
    function getCandidates() public view returns (Candidate[] memory) {
        return candidates;
    }
}
```


![image](https://github.com/user-attachments/assets/161a0f74-5992-4532-a580-c62555f2237d)

