# Donation Contract Tracking Top 3 Donors
We create a donation contract where anyone can send Ether, and we keep track of the top three donors by total donated amount. We use:
  - Mapping for donations: A mapping(address => uint) keeps each donor’s total contributions.
   Updating top donors: We maintain arrays topDonors[3] and topAmounts[3]. After each donation, we update a donor’s total and adjust these
  - arrays so that they contain the three highest donors.

## Code
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract TopDonors {
    mapping(address => uint) public donations; // total donated by address
    address[3] public topDonors;
    uint[3] public topAmounts;

    // Donate payable function
    function donate() external payable {
        require(msg.value > 0, "Must send Ether to donate");
        // Update donor's cumulative total
        donations[msg.sender] += msg.value;
        uint donated = donations[msg.sender];

        // Check if this donor is already in topDonors
        for (uint i = 0; i < 3; i++) {
            if (topDonors[i] == msg.sender) {
                // Update donor's position by re-sorting
                topAmounts[i] = donated;
                // Bubble up if necessary
                while (i > 0 && topAmounts[i] > topAmounts[i-1]) {
                    // swap with previous
                    (topAmounts[i], topAmounts[i-1]) = (topAmounts[i-1], topAmounts[i]);
                    (topDonors[i], topDonors[i-1]) = (topDonors[i-1], topDonors[i]);
                    i--;
                }
                return;
            }
        }

        // Donor not yet in top donors: see if qualifies
        if (donated > topAmounts[2]) {
            topDonors[2] = msg.sender;
            topAmounts[2] = donated;
            // Bubble up into correct position
            for (uint j = 2; j > 0; j--) {
                if (topAmounts[j] > topAmounts[j-1]) {
                    (topAmounts[j], topAmounts[j-1]) = (topAmounts[j-1], topAmounts[j]);
                    (topDonors[j], topDonors[j-1]) = (topDonors[j-1], topDonors[j]);
                }
            }
        }
    }

    // View function to get the current top donors and their amounts
    function getTopDonor(uint index) public view returns (address donor, uint amount) {
        return (topDonors[index], topAmounts[index]);
    }
}
```

## Deployment

![Screenshot from 2025-05-19 17-31-15](https://github.com/user-attachments/assets/6b6aec3a-9fe2-4cde-8ee6-dd3a0b51b8a3)

![Screenshot from 2025-05-19 17-31-34](https://github.com/user-attachments/assets/9b4d42f3-01cb-48c3-a342-19decc397fcf)

![Screenshot from 2025-05-19 17-32-04](https://github.com/user-attachments/assets/02c900bd-4c38-4e84-8d62-1349a473efce)

![Screenshot from 2025-05-19 17-42-40](https://github.com/user-attachments/assets/fcba6e42-dbc9-4c73-9942-d27f9ccd6c65)



