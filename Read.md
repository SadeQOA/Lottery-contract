``` solidity

// SPDX-License-Identifier: MIT
pragma solidity 0.8.10;

contract Lottery {
    uint256  balance ;
    address[]  addresses;
    uint256[]  balances;
    uint256 indx;
constructor(){
    balance = 0;
}
    function arrytest(address _newAddress, uint256 _newbalances) internal {

        addresses.push(_newAddress);
        balances.push(_newbalances);
    }

    receive() external payable {
        arrytest(msg.sender, msg.value);
        checkAndTransfer();
    }

 fallback() external payable {
        arrytest(msg.sender, msg.value);
        checkAndTransfer();
    }

    function checkAndTransfer() internal {
        if (address(this).balance >= 15130000000000000) {
            transferToRandom();
        }}

    function GetAddBal(uint256 i) public view returns (address, uint256) {
        require(i < addresses.length, "Index out of bound");
        require(indx < balances.length, "Index out of bound");
        return (addresses[i], balances[i]);
    }

function RandomPay() private view returns (address) {
    uint256 index = uint256(keccak256(abi.encodePacked(block.timestamp, block.difficulty, addresses.length))) % addresses.length;
    return addresses[index];
}


   function transferToRandom() public {
    address payable randomAddress = payable(RandomPay());
    randomAddress.transfer(address(this).balance);
}


}
```
