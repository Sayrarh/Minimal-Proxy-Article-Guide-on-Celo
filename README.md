# Multi-Sig Wallet Minimal Proxy on Celo and its Application in Smart Contracts

---

## Introduction

This article provides a comprehensive guide on building a Multi-signature Wallet Minimal Proxy on Celo Blockchain. In addition to providing a detailed explanation of the technical process involved in deploying the smart contract, I will also demonstrate how to interact with it. Multisig contracts are an essential tool for decentralized decision-making and governance, enabling multiple parties to authorize transactions on the blockchain.
<br/>
With the help of this article, you can follow the step-by-step instructions provided to create and utilize your own Multisig Wallet Minimal Proxy Contract on the Celo Blockchain. Whether you're a seasoned blockchain developer or a curious beginner, this article is sure to leave you feeling confident and empowered to leverage the power of Multisig contracts on the Celo network.

## Table of Contents

- [Multi-Sig Wallet Minimal Proxy on Celo and its Application in Smart Contracts](#multi-sig-wallet-minimal-proxy-on-celo-and-its-application-in-smart-contracts)
  - [Introduction](#introduction)
  - [Table of Contents](#table-of-contents)
  - [Objective](#objective)
  - [Prerequisites](#prerequisites)
  - [Requirements](#requirements)
  - [Factory Contracts](#factory-contracts)
    - [Types of Factory Contract Pattern](#types-of-factory-contract-pattern)
    - [Cloned Factory Contract using Minimal Proxy](<#cloned-factory-contract-using-minimal-proxy-contract)
  - [Multi-Sig Wallet](#multi-sig-wallet)
    - [Benefits of using a Multi-sig Wallet](#benefits-of-using-a-multi-sig-wallet)
  - [Tutorial](#tutorial)
    - [STEP 1 - Set up Hardhat Environment](#step-1---setup-hardhat-environment)
    - [STEP 2 - Create your Smart contracts](#step-2---create-your-smart-contracts)
      - [Multisig Wallet Contract Explained](#multisig-wallet-contract-explained)
      - [Minimal Proxy Contract Explained](#minimal-proxy-contract-explained)
    - [STEP 3 - Deploying the contracts](#step-3---deploying-the-contracts)
    - [STEP 4 - Interacting with the deployed contracts](#step-4---interacting-with-the-deployed-contracts)
    - [STEP 5 - ](#step5)
    - [Conclusion](#conclusion)

## Objective

Upon completion of this article, you'll possess the knowledge and skills needed to proficiently create and interact with your own Multi-Sig Minimal Proxy on the Celo blockchain. You'll gain a deep understanding of the technical aspects required to deploy the smart contract and navigate its functions seamlessly. By the end of it all, you'll be equipped to confidently utilize Multisig contracts on the Celo network, regardless of your level of expertise.

## Prerequisites

- Familiarity with the Solidity programming language: You should have a good grasp of Solidity, the primary programming language used to write smart contracts on the Ethereum and Celo blockchains.

- Basic familiarity with command line tools: You should be comfortable using command line tools such as the Terminal or Command Prompt to run commands and scripts.

- Good understanding of using Hardhat, a development environment set up for writing, testing, and deploying smart contracts on the Celo blockchain.

## Requirements

- A text editor: For this tutorial, we will make use of Visual Studio Code, so ensure you have VS Code setup on your PC: VSCode is a popular integrated development environment (IDE) for building software.
- You will need to have node.js installed on your system, with version V10. or higher.
- npm (node package manager) used for installing and managing dependencies.

## Multisig Wallet

A Multisig wallet is a type of cryptocurrency wallet that requires multiple signatures (or approvals) from different users or addresses to authorize a transaction. The purpose of a multisig wallet is to provide an extra layer of security and protection against unauthorized transactions, as multiple parties are required to sign off on any transactions.

### Benefits of using a Multi-sig Wallet

1. **Enhanced security**: With multiple signatures required to authorize a transaction, a multisig wallet provides increased security and protection against theft or unauthorized access.

2. **Shared control**: A multisig wallet allows multiple parties to have shared control over funds, which can be useful for organizations or groups that require collective decision-making.

3. **Reduced risk of human error**: Multisig wallets can reduce the risk of human error, as multiple parties are required to approve transactions, which can help prevent mistakes or fraudulent activity.

4. **Customizable authorization**: Multisig wallets can be customized to require a specific number of signatures, which can be useful for different use cases and scenarios.

## Factory Contract

A factory contract is a smart contract designed to produce and deploy other smart contracts. In other words, it acts as a template or a blueprint for the creation of new smart contracts. Factory contracts can be used to automate the process of smart contract creation, reducing the time and resources required to develop and deploy new contracts.

### Types of Factory Contract Patterns

The two factory contract patterns are:

1. **Simple Factory Pattern**: This pattern deploys multiple instances of other contracts without any optimization to save gas on each deployment. This pattern is useful when there are no specific optimization requirements for the smart contracts being deployed.

2. **Cloned Factory Pattern**: This pattern deploys multiple instances of other contracts with emphasis on optimization to save gas on each deployment. This pattern is useful when there is a need to optimize the gas costs associated with deploying smart contracts, which can result in significant cost savings.
   <br/>

Both patterns can be used to create and deploy multiple instances of smart contracts, but the Cloned Factory Pattern is specifically designed to optimize the gas costs associated with deployment. The choice of which pattern to use will depend on the specific requirements of the project, such as the need for gas optimization or the complexity of the smart contracts being deployed.

### Cloned Factory Contract using Minimal Proxy

The Clone Factory Contract is a reference implementation of the [EIP-1167](https://eips.ethereum.org/EIPS/eip-1167) standard, which is an Ethereum Improvement Proposal for creating **Minimal proxy contracts**. The Clone Factory Contract is designed to optimize the gas costs associated with deploying new instances of smart contracts by using a minimal proxy contract that points to a master contract. When a new instance is needed, the minimal proxy contract is cloned and the address of the new contract is updated to point to the new instance. This approach reduces the gas costs associated with deploying new instances because only the minimal proxy contract needs to be deployed once, and subsequent instances can be created by simply cloning the minimal proxy contract and updating the contract address.
<br/>

In this tutorial, we will be making use of the Cloned factory pattern.

## Tutorial

### STEP 1 - Set up Hardhat Environment

To begin setting up the Hardhat environment for your smart contract implementation, you will first need to create a new folder on your system. You can do this by using the ‘mkdir’ command in your terminal followed by the desired name of your folder. For example:

```
mkdir multisig-wallet
```

Once you have created the folder, you can initialize a new npm project inside it by running the following command:

```
npm init -y
```

This will create a “package.json” file in your project folder with default settings. Next, navigate to your project folder using the ‘cd’ command, like so:

```
cd multisig-wallet
```

Finally, open your project folder in VScode by running this command in your terminal:

```
code .
```

This will open up your project folder in Visual Studio Code, where you can start setting up your Hardhat environment and writing your smart contract code.
<br/>

Run the following command to initialize the Hardhat environment and create some default configuration files and folders required for building and testing smart contracts.

```
npm install hardhat --save-dev
npx hardhat
```

We will be using a typescript project for this tutorial, so click on “Create a typescript project” and enter this and other prompt options.

### STEP 2 - Create your Smart Contracts

In the root directory of your project, you'll find a folder called "contracts". To create a new TypeScript file, simply navigate to this folder and add your new files.
<br/>

For this tutorial, we'll be ceating a Multisignature Wallet Minimal Proxy Contract. To create this contracts, we'll need to generate three files:

- Multisig Wallet contract,
- Minimal Proxy contract, and
- Interface of the Multisig Wallet contract.

#### Multisig Wallet Contract Explained

This link to the Multisig wallet contract code is attached here.
<br/>

The multisignature wallet requires multiple owners to approve transactions before they can be executed. The contract includes the following components:

- There are state variables that are used to keep track of the state of the contract. These variables include the maximum number of owners allowed, the number of approvals required for a transaction to be executed, the address of the factory that created the contract, an array of valid owners, an array of all transactions, an array of successful transaction IDs, and the ID of the next transaction to be created.
- The contract has a constructor that takes an array of valid owners and a quorum (the number of approvals required for a transaction to be executed).
- The contract has several functions that can be called by anyone who is a valid owner of the contract. These functions include requestTransaction, and approveTransaction.
- The requestTransaction function allows an owner to create a new transaction by specifying the recipient and amount. The function returns the ID of the newly created transaction.
- The approveTransaction function allows an owner to approve a transaction by specifying the ID of the transaction. The function checks that the transaction has not already been approved and that the ID is valid.
  <br/>

If the number of approvals for the transaction meets the required quorum, the function executes the transaction and adds the transaction ID to the list of successful transaction IDs.

- getTxnsCount function returns the number of transactions that have been created.
- getAllowners function returns an array of all valid owners of the contract.
- getAlltxnDetails function returns the details of a specific transaction by ID.
- getAlltxnsInfo function returns an array of all transactions that have been created.
- allSuccessfulTxnIDs function returns an array of all successful transaction IDs.
- The contract includes a receive function that allows the contract to receive Ether, which is emitted as a Deposit event.
- The contract also includes some mappings. These mappings include \_transactions (which maps transaction IDs to transaction details), hasApprovedtxn (which maps transaction IDs to the approval status of each owner), and isOwner (which maps addresses to a boolean indicating whether or not the address is a valid owner).

#### Minimal Proxy Contract Explained

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.4;
import "./IMultisigWallet.sol";

contract MinimalProxy {
  event ContractCreated(address indexed newMultisig, uint256 position);

  mapping(uint256 => address) cloneAddresses;
  uint256 public contractIndex = 1;

  address[] allClonedMultiSigContractAddresses;

  function createClone(
    address _implementationContract,
    address[] memory validSigners,
    uint8 _quorum
  ) external returns (address) {
    // convert the address to 20 bytes
    bytes20 implementationContractInBytes = bytes20(_implementationContract);

    //address to assign cloned proxy
    address proxy;

    // as stated earlier, the minimal proxy has this bytecode
    // <3d602d80600a3d3981f3363d3d373d3d3d363d73><address of implementation contract><5af43d82803e903d91602b57fd5bf3>

    // <3d602d80600a3d3981f3> == creation code which copy runtime code into memory and deploy it

    // <363d3d373d3d3d363d73> <address of implementation contract> <5af43d82803e903d91602b57fd5bf3> == runtime code that makes a delegatecall to the implentation contract

    assembly {
      /*
            reads the 32 bytes of memory starting at pointer stored in 0x40
            In solidity, the 0x40 slot in memory is special: it contains the "free memory pointer"
            which points to the end of the currently allocated memory.
            */
      let clone := mload(0x40)
      // store 32 bytes to memory starting at "clone"
      mstore(
        clone,
        0x3d602d80600a3d3981f3363d3d373d3d3d363d73000000000000000000000000
      )

      /*
              |              20 bytes                |
            0x3d602d80600a3d3981f3363d3d373d3d3d363d73000000000000000000000000
                                                      ^
                                                      pointer
            */
      // store 32 bytes to memory starting at "clone" + 20 bytes
      // 0x14 = 20
      mstore(add(clone, 0x14), implementationContractInBytes)

      /*
              |               20 bytes               |                 20 bytes              |
            0x3d602d80600a3d3981f3363d3d373d3d3d363d73bebebebebebebebebebebebebebebebebebebebe
                                                                                              ^
                                                                                              pointer
            */
      // store 32 bytes to memory starting at "clone" + 40 bytes
      // 0x28 = 40
      mstore(
        add(clone, 0x28),
        0x5af43d82803e903d91602b57fd5bf30000000000000000000000000000000000
      )

      /*
            |                 20 bytes                  |          20 bytes          |           15 bytes          |
            0x3d602d80600a3d3981f3363d3d373d3d3d363d73b<implementationContractInBytes>5af43d82803e903d91602b57fd5bf3 == 45 bytes in total
            */

      // create a new contract
      // send 0 Ether
      // code starts at pointer stored in "clone"
      // code size == 0x37 (55 bytes)
      proxy := create(0, clone, 0x37)
    }
    IMultisigWallet(proxy).initialize(validSigners, _quorum);

    cloneAddresses[contractIndex] = proxy;
    allClonedMultiSigContractAddresses.push(proxy);

    contractIndex = contractIndex + 1;

    emit ContractCreated(proxy, allClonedMultiSigContractAddresses.length);
    return proxy;
  }

  // Check if an address is a clone of a particular contract address
  function isClone(
    address _implementationContract,
    address query
  ) external view returns (bool result) {
    bytes20 implementationContractInBytes = bytes20(_implementationContract);
    assembly {
      let clone := mload(0x40)
      mstore(
        clone,
        0x363d3d373d3d3d363d7300000000000000000000000000000000000000000000
      )
      mstore(add(clone, 0xa), implementationContractInBytes)
      mstore(
        add(clone, 0x1e),
        0x5af43d82803e903d91602b57fd5bf30000000000000000000000000000000000
      )

      let other := add(clone, 0x40)
      extcodecopy(query, other, 0, 0x2d)
      result := and(
        eq(mload(clone), mload(other)),
        eq(mload(add(clone, 0xd)), mload(add(other, 0xd)))
      )
    }
  }

  function getAllCreatedAddresses() external view returns (address[] memory) {
    return allClonedMultiSigContractAddresses;
  }

  function getCloneAddress(uint256 _index) external view returns (address) {
    return cloneAddresses[_index];
  }

  function getCurrentIndex() external view returns (uint256) {
    return allClonedMultiSigContractAddresses.length;
  }
}
```

The contract contains a createClone() function that deploys new instances of the multisig wallet contract by creating a minimal proxy contract. The deployed minimal proxy contract is a lightweight contract that points to the actual implementation contract.

**Pictorial Representation of the contract flow**
![Minimal Proxy Clone Representation](Images/mclone.png)

The implementation contract's(Multisig Wallet) address is passed as a parameter to the createClone() function, along with an array of valid signers and a quorum number. The function then creates the minimal proxy using the implementation contract's address and assigns it to a variable named proxy.
<br/>
The initialize() function of the implementation contract is then called through the IMultisigWallet(proxy).initialize(validSigners, \_quorum) line, passing the valid signers and quorum as arguments.
<br/>
The created proxy contract's address is then stored in the cloneAddresses mapping, and the index of the contract is stored in allClonedMultiSigContractAddresses.
<br/>
There are also view functions defined in the contract to retrieve information about the created contracts. getCloneAddress() takes an index and returns the corresponding clone address, getCurrentIndex() returns the number of created contracts, and isClone() checks if a given address is a clone of the implementation contract.
<br/>
The contract uses assembly code to create the minimal proxy contract. The bytecode for the minimal proxy contract is created by concatenating the initialization code and runtime code, with the implementation contract address inserted in the appropriate location in the bytecode.
