# Even Ether Splitting Among Three Fixed Addresses
This contract forwards any received Ether to three pre-set addresses, splitting it equally. 
We store three payable addresses at deployment and implement a receive() function:
  - Fixed payees: The three addresses are set in the constructor.
  - Automatic split: The receive function is payable and executes on any plain Ether transfer to the
    contract. It splits msg.value into three parts and transfers to each address.
  - Remainder handling: If msg.value isn’t divisible by 3, the remainder is sent to the first address to ensure all funds are distributed.

## Code
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Splitter {
    address payable public addr1;
    address payable public addr2;
    address payable public addr3;

    constructor(address payable _addr1, address payable _addr2, address payable _addr3) {
        addr1 = _addr1;
        addr2 = _addr2;
        addr3 = _addr3;
    }

    // Automatically called when Ether is sent to contract
    receive() external payable {
        uint share = msg.value / 3;
        uint remainder = msg.value - share*3;
        // Distribute shares; any remainder goes to addr1
        addr1.transfer(share + remainder);
        addr2.transfer(share);
        addr3.transfer(share);
    }
}
```



## Deployment

![Screenshot from 2025-05-19 18-06-39](https://github.com/user-attachments/assets/d2f525a0-b382-4319-a2dc-263b7cbf3b19)

![Screenshot from 2025-05-19 18-06-58](https://github.com/user-attachments/assets/e8b0f6cd-1146-4ba3-bb0e-5d0aa7e1e802)

![Screenshot from 2025-05-19 18-07-14](https://github.com/user-attachments/assets/cff2a7c1-2fc8-46ff-b578-d4062645f8b2)

![Screenshot from 2025-05-19 18-07-33](https://github.com/user-attachments/assets/7dc80861-02bd-4e19-9363-870b6d9dee76)



