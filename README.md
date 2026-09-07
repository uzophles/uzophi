// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract BadgeTwo {
    address public owner;
    mapping(address => bool) public hasBadge;

    event BadgeGranted(address indexed user);
    event BadgeRevoked(address indexed user);

    constructor() {
        owner = msg.sender;
        hasBadge[msg.sender] = true;
    }

    function grantBadge(address user) external {
        require(msg.sender == owner, "Not owner");
        hasBadge[user] = true;
        emit BadgeGranted(user);
    }

    function revokeBadge(address user) external {
        require(msg.sender == owner, "Not owner");
        hasBadge[user] = false;
        emit BadgeRevoked(user);
    }

    function checkBadge(address user) external view returns (bool) {
        return hasBadge[user];
    }
}
