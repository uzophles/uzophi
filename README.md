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
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract FlameThree {
    mapping(address => uint256) public flames;
    mapping(address => uint256) public lastFlame;

    event Flamed(address indexed user, uint256 level);

    function flame() external {
        if (block.timestamp <= lastFlame[msg.sender] + 9 minutes) {
            flames[msg.sender] += 1;
        } else {
            flames[msg.sender] = 1;
        }
        lastFlame[msg.sender] = block.timestamp;
        emit Flamed(msg.sender, flames[msg.sender]);
    }

    function getFlames(address user) external view returns (uint256) {
        return flames[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract HitThree {
    address[] public hitters;
    uint256[] public timestamps;

    event Hit(address indexed user, uint256 timestamp, uint256 index);

    function hit() external {
        hitters.push(msg.sender);
        timestamps.push(block.timestamp);
        emit Hit(msg.sender, block.timestamp, hitters.length - 1);
    }

    function getHit(uint256 index) external view returns (address, uint256) {
        require(index < hitters.length, "Invalid index");
        return (hitters[index], timestamps[index]);
    }

    function count() external view returns (uint256) {
        return hitters.length;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract TreasureThree {
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
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract NovaThree {
    mapping(address => uint256) public novas;
    mapping(address => uint256) public lastNova;

    event NovaActivated(address indexed user, uint256 level);

    function activate() external {
        if (block.timestamp <= lastNova[msg.sender] + 11 minutes) {
            novas[msg.sender] += 1;
        } else {
            novas[msg.sender] = 1;
        }
        lastNova[msg.sender] = block.timestamp;
        emit NovaActivated(msg.sender, novas[msg.sender]);
    }

    function getNovas(address user) external view returns (uint256) {
        return novas[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract TraceThree {
    address[] public tracers;
    uint256[] public timestamps;

    event Traced(address indexed user, uint256 timestamp, uint256 index);

    function trace() external {
        tracers.push(msg.sender);
        timestamps.push(block.timestamp);
        emit Traced(msg.sender, block.timestamp, tracers.length - 1);
    }

    function getTrace(uint256 index) external view returns (address, uint256) {
        require(index < tracers.length, "Invalid index");
        return (tracers[index], timestamps[index]);
    }

    function count() external view returns (uint256) {
        return tracers.length;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract BadgeThree {
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

contract VaultThree {
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
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract SparkFour {
    mapping(address => uint256) public sparks;
    mapping(address => uint256) public lastSpark;

    event Sparked(address indexed user, uint256 level);

    function spark() external {
        if (block.timestamp <= lastSpark[msg.sender] + 5 minutes) {
            sparks[msg.sender] += 1;
        } else {
            sparks[msg.sender] = 1;
        }
        lastSpark[msg.sender] = block.timestamp;
        emit Sparked(msg.sender, sparks[msg.sender]);
    }

    function getSparks(address user) external view returns (uint256) {
        return sparks[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract TapFour {
    address[] public tappers;
    uint256[] public timestamps;

    event Tapped(address indexed user, uint256 timestamp, uint256 index);

    function tap() external {
        tappers.push(msg.sender);
        timestamps.push(block.timestamp);
        emit Tapped(msg.sender, block.timestamp, tappers.length - 1);
    }

    function getTap(uint256 index) external view returns (address, uint256) {
        require(index < tappers.length, "Invalid index");
        return (tappers[index], timestamps[index]);
    }

    function count() external view returns (uint256) {
        return tappers.length;
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PermitFour {
    address public owner;
    mapping(address => bool) public hasPermit;

    event PermitGranted(address indexed user);
    event PermitRevoked(address indexed user);

    constructor() {
        owner = msg.sender;
        hasPermit[msg.sender] = true;
    }

    function grantPermit(address user) external {
        require(msg.sender == owner, "Not owner");
        hasPermit[user] = true;
        emit PermitGranted(user);
    }

    function revokePermit(address user) external {
        require(msg.sender == owner, "Not owner");
        hasPermit[user] = false;
        emit PermitRevoked(user);
    }

    function checkPermit(address user) external view returns (bool) {
        return hasPermit[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract LockerFour {
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
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract GlowFour {
    mapping(address => uint256) public glows;
    mapping(address => uint256) public lastGlow;

    event Glowed(address indexed user, uint256 level);

    function glow() external {
        if (block.timestamp <= lastGlow[msg.sender] + 10 minutes) {
            glows[msg.sender] += 1;
        } else {
            glows[msg.sender] = 1;
        }
        lastGlow[msg.sender] = block.timestamp;
        emit Glowed(msg.sender, glows[msg.sender]);
    }

    function getGlows(address user) external view returns (uint256) {
        return glows[user];
    }
}
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract SignalFour {
    address[] public signalers;
    uint256[] public timestamps;

    event Signaled(address indexed user, uint256 timestamp, uint256 index);

    function signal() external {
        signalers.push(msg.sender);
        timestamps.push(block.timestamp);
        emit Signaled(msg.sender, block.timestamp, signalers.length - 1);
    }

    function getSignal(uint256 index) external view returns (address, uint256) {
        require(index < signalers.length, "Invalid index");
        return (signalers[index], timestamps[index]);
    }

    function count() external view returns (uint256) {
        return signalers.length;
    }
}
