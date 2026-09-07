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
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract KeyTwo {
    address public owner;
    mapping(address => bool) public hasKey;

    event KeyGranted(address indexed user);
    event KeyRevoked(address indexed user);

    constructor() {
        owner = msg.sender;
        hasKey[msg.sender] = true;
    }

    function grantKey(address user) external {
        require(msg.sender == owner, "Not owner");
        hasKey[user] = true;
        emit KeyGranted(user);
    }

    function revokeKey(address user) external {
        require(msg.sender == owner, "Not owner");
        hasKey[user] = false;
        emit KeyRevoked(user);
    }

    function checkKey(address user) external view returns (bool) {
        return hasKey[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract SafeThree {
    address public owner;
    uint256 public total;

    event Deposited(address indexed from, uint256 amount);
    event Withdrawn(uint256 amount);

    constructor() {
        owner = msg.sender;
    }

    function deposit() external payable {
        require(msg.value > 0, "Must send ETH");
        total += msg.value;
        emit Deposited(msg.sender, msg.value);
    }

    function withdraw() external {
        require(msg.sender == owner, "Not owner");
        uint256 amount = address(this).balance;
        total = 0;
        (bool success, ) = owner.call{value: amount}("");
        require(success, "Transfer failed");
        emit Withdrawn(amount);
    }
}
