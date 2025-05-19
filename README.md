# Smart Contract Auditing Master

## Overview

This repo serves as a comprehensive guide to advanced topics in smart contract auditing, encompassing reverse engineering, vulnerability detection, EVM bytecode manipulation, AI/ML applications, and blockchain forensics. Each topic is detailed in dedicated submodules by providing in-depth resources and practical examples.

## Table of Contents

1. [Reverse Engineering Smart Contracts](#reverse-engineering-smart-contracts)
2. [Finding Critical & High-Severity Vulnerabilities Quickly](#finding-critical--high-severity-vulnerabilities-quickly)
3. [Manipulating EVM Bytecode & Opcode-Level Attacks](#manipulating-evm-bytecode--opcode-level-attacks)
4. [AI & Machine Learning for Smart Contract Auditing](#ai--machine-learning-for-smart-contract-auditing)
5. [Blockchain Forensics & Tracking Stolen Funds](#blockchain-forensics--tracking-stolen-funds)

## Submodules

This master repository integrates several submodules, each focusing on a specific aspect of smart contract auditing:

### Reverse Engineering Smart Contracts

Explore techniques for extracting and decompiling bytecode from deployed contracts, identifying vulnerabilities in obfuscated contracts, and study real-world cases like The DAO Hack.

**Topics Covered:**

- Extracting bytecode from deployed contracts
- Decompiling bytecode to Solidity
- Identifying vulnerabilities in obfuscated contracts
- Case Study: The DAO Hack

**Repository:** [reverse-engineering-smart-contracts](https://github.com/jason-victor1/reverse-engineering-smart-contracts)

### Finding Critical & High-Severity Vulnerabilities Quickly

Learn to detect reentrancy, integer overflows, access control flaws, and utilize advanced mathematical tools like SMT solvers for verifying contract logic.

**Topics Covered:**

- Detecting reentrancy, integer overflows, and access control flaws
- Advanced math (SMT solvers) for verifying contract logic
- Graph theory for multi-contract vulnerabilities
- Statistical outlier detection for flash loan exploits

**Repository:** [Critical-High-Severity-Vulnerabilities](https://github.com/jason-victor1/Critical-High-Severity-Vulnerabilities)

### Manipulating EVM Bytecode & Opcode-Level Attacks

Delve into EVM opcodes, delegatecall hijacks, selfdestruct vulnerabilities, and methods for manually modifying bytecode for attack simulations.

**Topics Covered:**

- Understanding EVM opcodes
- Delegatecall hijacks & selfdestruct vulnerabilities
- Manually modifying bytecode for attack simulations
- Deploying altered contracts on a testnet

**Repository:** [EVM-Bytecode-Opcode-Level-Attacks](https://github.com/jason-victor1/EVM-Bytecode-Opcode-Level-Attacks)

### AI & Machine Learning for Smart Contract Auditing

Discover how AI-powered decompilers can reconstruct Solidity code, build AI models to predict contract vulnerabilities, and automate exploit detection with deep learning.

**Topics Covered:**

- AI-powered decompilers for reconstructing Solidity
- Building an AI model to predict contract vulnerabilities
- Automating exploit detection with deep learning
- Hands-on: Training an ML model for security scanning

**Repository:** [AI-ML-for-Smart-Contract-Auditing](https://github.com/jason-victor1/AI-ML-for-Smart-Contract-Auditing)

### Blockchain Forensics & Tracking Stolen Funds

Examine real-world case studies, utilize tools for fund tracking, monitor transactions in real-time, and learn strategies to prevent money laundering via mixers like Tornado Cash.

**Topics Covered:**

- Real-world case studies (Euler Finance, Ronin Bridge)
- Using Chainalysis alternatives for fund tracking
- Monitoring transactions in real time (Forta, MistTrack)
- Preventing money laundering via Tornado Cash

**Repository:** [blockchain-forensics](https://github.com/jason-victor1/blockchain-forensics)

## 🧠 Advanced Track  
### 📌 [Smart Contract Security & Forensics Deep Dive]([./Smart%20Contract%20Security%20%26%20Forensics%20Deep%20Dive](https://github.com/jason-victor1/Smart-Contract-Auditing-Master/blob/main/Smart%20Contract%20Security%20%26%20Forensics%20Deep%20Dive.md))

This is the **flagship advanced module** of the repo, featuring:

1. ✅ Live reentrancy attack execution and monitoring using Forta  
2. ✅ Step-by-step guide to tracing and recovering stolen funds  
3. ✅ Real-world case study of the $600M Poly Network hack  

> Includes working Solidity contracts, attack scripts, and Forta bot detection logic.

---



