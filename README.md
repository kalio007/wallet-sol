# wallet-sol
this task is a continuation on my solidity journey.
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.13;
// this contracts acts as a wallet, only the owner can send eth out but can recieve eth from any address
contract EtherWallet {
    address payable public owner; // this 

    constructor() {
        owner = payable(msg.sender);//the keyword "payable"ensures the adress is allowed to receive eth
    }

    receive() external payable {} // the "receieve" keyword ensures the contract can accept eth from other addresses

    function withdraw(uint _amount) external {
         require(msg.sender == owner, "only owner can withdraw");// the "require" key word ensures only the owner of the wallet can call the withdraw function.
        payable(msg.sender).transfer(_amount);
        // the fuction helps the owner withdraw an amount of the ether.
    }

    function getBalance() external view returns (uint) {//the "view" keyword helps saves gas as it only reads a blockchain and not transcat.
        return address(this).balance;
        //this function gets the balance of the eth in the address.
    }
}
