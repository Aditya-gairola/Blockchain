# Owner-Only Access with Modifiers
A common pattern is to restrict some functions so that only the contract deployer (owner) can 
execute them. We demonstrate this with a simple contract using a modifier:
  - Owner variable: Store owner = msg.sender in the constructor.
  - Modifier: Define modifier onlyOwner { require(msg.sender == owner, "Not owner"); _; }.
  - Protected function: Any function declared with onlyOwner can only be called by the owner

## Code
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract OwnerRestricted {
    address public owner;

    constructor() {
        owner = msg.sender;  // deployer becomes the owner
    }

    // Modifier that restricts access to the owner address
    modifier onlyOwner() {
        require(msg.sender == owner, "Caller is not owner");
        _;
    }

    // Example of a restricted function
    function privilegedAction() public onlyOwner {
        // Code here can only be executed by the contract owner
    }
}
```
## Deployment

![Screenshot from 2025-05-19 17-06-14](https://github.com/user-attachments/assets/199ca322-4ded-4139-9445-daf9d113b885)

 ![Screenshot from 2025-05-19 17-06-29](https://github.com/user-attachments/assets/d120f3a0-d078-4c8f-9741-9f2452f60d3f)

 ![Screenshot from 2025-05-19 17-06-56](https://github.com/user-attachments/assets/4faff8bb-bcb4-49b4-b6f9-47b676bcd402)

