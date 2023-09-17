//SPDX-License-Idenifier:MIT
pragma solidity ^0.8.0;

contract VickyPiggyBank {
event Deposit(address indexed sender, uint amount);
event Withdraw(address indexed sender, uint amount);

address public owner;
uint256 public accountBalance;

constructor() {
owner = msg.sender;
}

modifier onlyOwner() {
require(msg.sender == owner, "ONLY THE OWNER CAN CALL THIS FUNCTION");
_;
}
 
function deposit() public payable {
require(msg.value > 0, "MUST DEPOSIT SOME ETHER");
accountBalance += msg.value;
emit Deposit(msg.sender, msg.value);
}


function withdrawMoney(uint256 _amount) public onlyOwner {
require(_amount <= accountBalance, "INSUFFICIENT BALANCE");
accountBalance -= _amount;
payable(msg.sender).transfer(_amount);
emit Withdraw(msg.sender, _amount);
}
function getBalance() public view returns(uint256) {
    return accountBalance;

}
}
