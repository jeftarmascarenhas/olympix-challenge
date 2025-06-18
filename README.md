# OracleGuard AI

## Olympix Challange
Assignment:
- look through recent Defi exploits (in last 18 months)
- pick the one you find most interesting
- architect a solution for a tool that would've prevented it (bonus points if you have a POC) 

Note: 
- I didn't have time to implement the PoC
- I organize my markdown file using AI
- It took me 3 days to come up with this idea

## Overview
OracleGuard AI is an AI-powered tool designed to detect, analyze, and mitigate oracle manipulation vulnerabilities in DeFi smart contracts.

This solution is inspired by the **UwU Lend exploit (June 2024)**, where a malicious actor manipulated an on-chain price oracle via a flash loan, resulting in a loss of ~$19.5M. The attacker temporarily inflated the price of Curve’s CRV token to borrow assets against the manipulated collateral value.

Oracle manipulation remains one of the most common and devastating attack vectors in DeFi. OracleGuard AI provides developers, auditors, and protocols with an intelligent agent capable of understanding smart contract oracle patterns, simulating attack scenarios, and recommending mitigations.

---

## 🎯 Challenge Description

> Look through recent DeFi exploits (in the last 18 months).  
> Pick one you find most interesting.  
> Architect a solution for a tool that would've prevented it.  
> *(Bonus points if you have a PoC).*  

---

## Why UwU Lend Exploit?

- **Type:** Oracle Manipulation + Flash Loan Attack  
- **Date:** June 2024  
- **Loss:** ~$19.5M  

**Summary:**  
- UwU Lend relied on a DEX pool spot price oracle (Curve CRV).  
- The attacker used a flash loan to inflate the CRV price temporarily.  
- They deposited overpriced CRV as collateral.  
- Borrowed maximum available assets.  
- After exiting, the price normalized, and the protocol was drained.

---

## 🛠️ Solution – OracleGuard AI

OracleGuard AI consists of an AI Agent that performs:

- **Static Analysis:** Detects oracle design patterns.  
- **LLM Reasoning:** Understands whether oracle logic is safe.  
- **Dynamic Attack Simulation:** Models liquidity manipulation, flash loans.  
- **Risk Scoring:** Assigns SAFE / WARNING / CRITICAL based on exposure.  
- **Mitigation Suggestion:** Recommends fixes like TWAP, Chainlink, circuit breakers.

---

## Architecture

The architecture design is fully detailed in [ARCHITECTURE.md](./ARCHITECTURE.md).

---
