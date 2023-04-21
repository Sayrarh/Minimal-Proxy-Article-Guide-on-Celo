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
    - [Cloned Factory Contract(Minimal Proxy Contract)](<#cloned-factory-contract(minimal-proxy-contract)>)
  - [Multi-Sig Wallet](#multi-sig-wallet)
    - [Benefits of using a Multi-sig Wallet](#benefits-of-using-a-multi-sig-wallet)
  - [Tutorial](#tutorial)
    - [STEP 1 - Set up Hardhat Environment](#step-1---setup-hardhat-environment)
    - [STEP 2 - Create your Minimal Proxy Contract](#step-2---create-your-minimal-proxy-contract)
    - [STEP 3 - Simple bank contract with Withdraw defect](#step-3---simple-bank-contract-with-withdraw-defect)
    - [STEP 4 - Interacting with our deployed Contract](#step-4---interacting-with-our-deployed-contract)
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

## Multisig-Wallet

A multisig wallet is a type of cryptocurrency wallet that requires multiple signatures (or approvals) from different users or addresses to authorize a transaction. The purpose of a multisig wallet is to provide an extra layer of security and protection against unauthorized transactions, as multiple parties are required to sign off on any transactions.

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

### Cloned Factory Contract(Minimal Proxy Contract)

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

For this tutorial, we'll be ceating a Multisignature Wallet Minimal Proxy Contract. To create this contracts, we'll need to generate three files: one for the Multisig contract, one for the Minimal Proxy, and one for the interface of the Multisig contract.
