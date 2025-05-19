# Simple Auction System
This contract implements an open (English) auction. Bidders call bid() sending Ether; the contract tracks the highest 
bid and allows outbid participants to withdraw their funds. The highest bidder wins at auction end. Important features:
  - Auction parameters: We store beneficiary, auctionEndTime, highestBid, and highestBidder.
  - Bidding: The bid function (payable) requires that the bid is higher than the current highest and that the auction has not ended yet.
  - Refunds: We use a mapping(address => uint) pendingReturns to allow outbid bidders to withdraw their funds.
  - Auction end: A function auctionEnd finalizes the auction after time is up (using block.timestamp in recent Solidity) and sends
    the highest bid to the beneficiary.

## Code
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleAuction {
    address payable public beneficiary;
    uint public auctionEndTime;
    
    address public highestBidder;
    uint public highestBid;
    mapping(address => uint) public pendingReturns; // funds to refund

    bool public ended;

    event HighestBidIncreased(address bidder, uint amount);
    event AuctionEnded(address winner, uint amount);

    constructor(uint biddingTimeSeconds, address payable _beneficiary) {
        beneficiary = _beneficiary;
        auctionEndTime = block.timestamp + biddingTimeSeconds;
    }

    // Place a bid on the auction
    function bid() external payable {
        require(block.timestamp <= auctionEndTime, "Auction already ended");  // time check
        require(msg.value > highestBid, "There already is a higher bid");     // bid check

        if (highestBid != 0) {
            // Refund the previous highest bidder
            pendingReturns[highestBidder] += highestBid;
        }
        highestBidder = msg.sender;
        highestBid = msg.value;
        emit HighestBidIncreased(msg.sender, msg.value);
    }

    // Withdraw a previously overbid amount
    function withdraw() external returns (bool) {
        uint amount = pendingReturns[msg.sender];
        require(amount > 0, "No funds to withdraw");
        pendingReturns[msg.sender] = 0;
        // Send the funds back to the bidder
        (bool success, ) = payable(msg.sender).call{value: amount}("");
        require(success, "Transfer failed");
        return true;
    }

    // End the auction and transfer the highest bid to beneficiary
    function auctionEnd() external {
        require(block.timestamp >= auctionEndTime, "Auction not yet ended");
        require(!ended, "auctionEnd has already been called");
        ended = true;
        emit AuctionEnded(highestBidder, highestBid);
        beneficiary.transfer(highestBid);
    }
}
```

## Deployment

![Screenshot from 2025-05-19 17-50-22](https://github.com/user-attachments/assets/0582d1cf-9366-46fa-911d-bd3eb0fed203)

![Screenshot from 2025-05-19 17-50-49](https://github.com/user-attachments/assets/ec34a501-bf03-4e50-8ca6-f2ba0b59a6d3)

![Screenshot from 2025-05-19 17-51-03](https://github.com/user-attachments/assets/33996e18-167e-47f9-b418-5ac0b5101c09)

![Screenshot from 2025-05-19 17-53-30](https://github.com/user-attachments/assets/759b2bf9-4b52-43cc-8f1d-72c7c1c93d77)





