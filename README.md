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
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PingTwo {
    address[] public pingers;
    uint256[] public timestamps;

    event Pinged(address indexed user, uint256 timestamp, uint256 index);

    function ping() external {
        pingers.push(msg.sender);
        timestamps.push(block.timestamp);
        emit Pinged(msg.sender, block.timestamp, pingers.length - 1);
    }

    function getPing(uint256 index) external view returns (address, uint256) {
        require(index < pingers.length, "Invalid index");
        return (pingers[index], timestamps[index]);
    }

    function count() external view returns (uint256) {
        return pingers.length;
    }
}
