# Simple-Timed-Auction
Simple Timed Auction
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract TimedAuction {
    uint256 public endTime;
    address public highestBidder;
    uint256 public highestBid;

    constructor(uint256 duration) {
        endTime = block.timestamp + duration;
    }

    function bid() public payable {
        require(block.timestamp < endTime, "Ended");
        require(msg.value > highestBid, "Low bid");

        payable(highestBidder).transfer(highestBid);
        highestBid = msg.value;
        highestBidder = msg.sender;
    }
}
