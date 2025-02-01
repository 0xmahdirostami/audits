---
title: PossumLabs CyberCash Audit Report
author: Mahdi Rostami
date: January 31, 2025
header-includes:
  - \usepackage{titling}
  - \usepackage{graphicx}
---

\begin{titlepage}
    \centering
    \begin{figure}[h]
        \centering
        \includegraphics[width=0.5\textwidth]{logo.pdf} 
    \end{figure}
    \vspace*{2cm}
    {\Huge\bfseries PossumLabs CyberCash Audit Report\par}
    \vspace{1cm}
    {\Large Version 1.0\par}
    \vspace{2cm}
    {\Large\itshape Mahdi Rostami\par}
    \vfill
    {\large \today\par}
\end{titlepage}

\maketitle

<!-- Your report starts here! -->

Prepared by: Mahdi Rostami [[https://x.com/0xmahdirostami]](https://x.com/0xmahdirostami)

# Table of Contents

- [Table of Contents](#table-of-contents)
- [CyberCash Report Security Review](#cybercash-report-security-review)
  - [Disclaimer](#disclaimer)
    - [Impact](#impact)
    - [Actions required by severity level](#actions-required-by-severity-level)
  - [Executive summary](#executive-summary)
    - [Overview](#overview)
    - [Scope](#scope)
    - [Compatibilities](#compatibilities)
    - [Known Issues](#known-issues)
    - [Issues found](#issues-found)
- [Findings](#findings)
  - [Medium Severity](#medium-severity)
    - [\[M-1\] Contract doesn't prevent burn score transfer to migrator and liquidity pool](#m-1-contract-doesnt-prevent-burn-score-transfer-to-migrator-and-liquidity-pool)
  - [Low Severity](#low-severity)
    - [\[L-1\] Contract is not compatible with more than 18 decimal tokens](#l-1-contract-is-not-compatible-with-more-than-18-decimal-tokens)
    - [\[L-2\] Unnecessary increase in total supply of tokens that were never minted](#l-2-unnecessary-increase-in-total-supply-of-tokens-that-were-never-minted)
    - [\[L-3\] Non minted tokens are added to pending mint due to total burn start point](#l-3-non-minted-tokens-are-added-to-pending-mint-due-to-total-burn-start-point)
  - [Info Gas](#info-gas)


# CyberCash Report Security Review

A security review of the [ [CyberCash] ](https://www.possumlabs.io/), [[GitHub]](https://github.com/PossumLabsCrypto/CyberCash) smart contracts was done by [[mahdi rostami]](https://twitter.com/0xmahdirostami) . \
This audit report includes all the vulnerabilities, issues and code improvements found during the security review.

## Disclaimer

"Audits are a time, resource and expertise bound effort where trained experts evaluate smart
contracts using a combination of automated and manual techniques to find as many vulnerabilities
as possible. Audits can show the presence of vulnerabilities **but not their absence**."

\- Secureum

### Impact

- **High**
Issues that lead to the loss of user funds. Such issues include:
	- Direct theft of any user funds, whether at rest or in motion.
	- Long-term freezing of user funds.
	Theft or long term freezing of unclaimed yield or other assets.
	- Protocol insolvency
- **Medium**
  Issues that lead to an economic loss but do not lead to direct loss of on-chain assets. Examples are:
	- Gas griefing attacks (make users overpay for gas)
	- Attacks that make essential functionality of the contracts temporarily unusable or inaccessible.
	- Short-term freezing of user funds.
- **Low**
  Issues where the behavior of the contracts differs from the intended behavior (as described in the docs and by common sense), but no funds are at risk.

### Actions required by severity level

- **High** - client **must** fix the issue.
- **Medium** - client **should** fix the issue.
- **Low** - client **could** fix the issue.

## Executive summary

### Overview

| Project Name |                                               CyberCash                                                |
| :----------: | :---------------------------------------------------------------------------------------------------: |
|  Repository  |                         [[Link]](https://github.com/PossumLabsCrypto/CyberCash)                         |
| Commit Hash  | [[d766a22]](https://github.com/PossumLabsCrypto/CyberCash/e54d093bb7b67173921c844428dd4020dde7b26a) |
|     Docs     |              No Docs             |
|   Methods    |                                             Manual Review                                             |

### Scope

|     File      |
| :-----------: |
| All files in repo |

### Compatibilities

- Solc Version: =0.8.19

### Known Issues

None

### Issues found

|   Severity    | Count |
| :-----------: | :---: |
|     High      |   0   |
|    Medium     |   1   |
|      Low      |   3   |
|    Info/Gas   |   3   |

# Findings
## Medium Severity
### [M-1] Contract doesn't prevent burn score transfer to migrator and liquidity pool

**Description**

The contract does not burn or reward for the migrator and liquidity provider (LP). An attacker could transfer the burn score to these addresses, breaking some functions.

**Impact**

the contract will show a higher balance than the actual balance for those addresses, and if attackers repeat it they gain some tokens which is not accepted.

**Proof of Concept (PoC)**

<details>

```solidity
// Transfer the burnScore from one user to another & verify new reward accrual
function test_TransferBurnScoreToMigrator() public {
    helper_Migrator_setCashAddress();
    helper_Migrator_addTokenMigration();

    uint256 amountSend = 1e21;

    vm.startPrank(treasury);
    // Step 1: Send tokens to Alice, treasury accrues burnScore
    cyberCash.transfer(Alice, amountSend);

    // Step 2: Let rewards accrue
    vm.warp(block.timestamp + oneYear);

    // Step 3: Transfer burnScore to migrator
    cyberCash.transferBurnScore(address(migrator), cyberCash.burnScore(treasury));

    // Step 4: Let rewards accrue & check
    vm.warp(block.timestamp + oneYear);

    uint256 mint = MINT_PER_SECOND * oneYear;

    assertEq(cyberCash.balanceOf(address(migrator)), mint); // migrator earns ~1Bn
    vm.stopPrank();

    uint256 psmAmount = 1e6;
    uint256 migrationOne = 1e6;

    // Treasury sends psm to Alice
    vm.startPrank(treasury);
    IERC20(psm).transfer(Alice, psmAmount);

    // Alice sets approval
    vm.startPrank(Alice);
    IERC20(psm).approve(address(migrator), 1e6);

    // Scenario 1: Alice migrates
    vm.expectRevert("ERC20: transfer amount exceeds balance"); //@audit
    migrator.migrate(psm, migrationOne);
    vm.stopPrank();

    vm.startPrank(treasury);
    // Step 1: Send tokens to Alice, treasury accrues burnScore
    cyberCash.transfer(Alice, amountSend);

    // Step 2: Let rewards accrue
    vm.warp(block.timestamp + oneYear);

    // Step 3: Transfer burnScore to migrator
    cyberCash.transferBurnScore(address(migrator), cyberCash.burnScore(treasury));

    // Step 4: Let rewards accrue & check
    vm.warp(block.timestamp + oneYear);

    mint = MINT_PER_SECOND * oneYear;

    assert(cyberCash.balanceOf(address(migrator)) > 2 * mint); // migrator gains some real balance  //@audit
    vm.stopPrank();

    // Alice sets approval
    vm.startPrank(Alice);
    IERC20(psm).approve(address(migrator), 1e6);

    // Scenario 1: Alice migrates
    migrator.migrate(psm, migrationOne);  //@audit
    vm.stopPrank();
}
```
</details>

As shown, the test reverts because the migrator assumes its balance is more than the real balance. If an attacker transfers the burn score again, the migrator will gain some real balance.

**Mitigation**

Restrict those addresses in `transferBurnScore`.

**Remark**

Fixed. [[commit]](https://github.com/PossumLabsCrypto/CyberCash/commit/6f3ef891a0a7f49cd672a3db539dfd38636baf8b)

## Low Severity

### [L-1] Contract is not compatible with more than 18 decimal tokens

**Description**

Currently, our contract assumes that all approved tokens will have 18 decimals. However, this assumption may be false in the future, potentially leading to issues if tokens with more than 18 decimals are used. 

For tokens with fewer than 18 decimals, owners could set a higher ratio to compensate. For example:

- For a token with 17 decimals, a 1:1 migration could use a ratio of `RATIO_PRECISION * 10`.

However, for tokens with more than 18 decimals, owners have limited flexibility. With RATIO_PRECISION set to 1000, the ratio could range from 1 to 1000. This creates a limitation for owners who want to provide more tokens.

For instance, if a token has 20 decimals and an owner wants to offer a 1:100 ratio, they would need to set the ratio to 0.1, which is not allowed given the current constraints.

**Impact**

Currently, there is little real-world impact, as owners can create separate contracts for unusual cases. However, this approach is suboptimal and may lead to unnecessary complexity.

**Mitigation**

To address this issue, we propose implementing a decimal normalization mechanism. This would allow the contract to handle tokens with varying decimal precisions more effectively, providing greater flexibility and reducing potential conflicts.

**Remark**

Fixed. [[commit]](https://github.com/PossumLabsCrypto/CyberCash/commit/7a04f457a6aecb03f2bb11b36920621666aa1f6b)

### [L-2] Unnecessary increase in total supply of tokens that were never minted

**Description**

Currently, the rewards earned between the deployment time and the first transfer are added to the pending mint. However, these rewards will never be minted, leading to an incorrect increase in the total supply.



**Impact**

The total supply increases despite the fact that these tokens will not be minted.

**Proof of Concept (PoC)**

<details>

```solidity
function test_pendingMint() public {
    vm.warp(block.timestamp + oneYear);
    
    // Transfer tokens
    vm.prank(treasury);
    cyberCash.transfer(Alice, 13e17);
    console.log(cyberCash.pendingMints());
}
```

Logs Before Mitigation:

```
[PASS] test_pendingMint() (gas: 170495)
Logs:
  999999999999999999990144000
```

Logs After Mitigation:
```
[PASS] test_pendingMint() (gas: 175560)
Logs:
  0
```
</details>

**Mitigation**

To address this issue, check for the first call to `burnsAndRewards` and avoid updating the pending mint on the first call:

```solidity
if (first) {
    first = 0;
} else {
    pendingMints = (pendingMints + addedRewards) - rewards;
}
```

**Remark**

Fixed. [[commit]](https://github.com/PossumLabsCrypto/CyberCash/commit/0156751368bd337f660bce598f4e626d87c52484)

### [L-3] Non minted tokens are added to pending mint due to total burn start point

**Description**

Currently, due to an initial total burned value of 1, over time, some rewards are not being minted. Instead, these rewards are added to pending mint and incorrectly increase the total supply.

**Impact**

A wrong increase in total supply occurs as these tokens will not minted as intended.

**Proof of Concept (PoC)**

<details>

```solidity
function test_pendingMint() public {
    vm.warp(block.timestamp + oneYear);

    // Transfer tokens
    vm.prank(treasury);
    cyberCash.transfer(Alice, 13e17);
    console.log(cyberCash.pendingMints());
}
```

Logs Before Mitigation:
```
[PASS] test_pendingMint() (gas: 194180)
Logs:
  153846153847
```

Logs After Mitigation:
```
[PASS] test_pendingMint() (gas: 215290)
Logs:
  1
```
</details>

**Mitigation**

To address this issue, check for the first call to `burnsAndRewards` and decrease the total burned value by 1 for that first call:

```solidity
if (first) {
    if (burnedFromTx > 0) {
         totalBurned += burnedFromTx - 1;
         first = 0;
   }
} else {
    totalBurned += burnedFromTx;
}
```

**Remark**

Fixed. [[commit]](https://github.com/PossumLabsCrypto/CyberCash/commit/0156751368bd337f660bce598f4e626d87c52484)

## Info Gas

- Boolean equality is not required

If x is a boolean, there is no need to do if(x == true) or if(x == false). Just use if(x) and if(!x) respectively.

Instances:
s
```solidity
	        if (allowedTokens[_token] == true) revert IsAllowed();
```

Fixed. [[commit]](https://github.com/PossumLabsCrypto/CyberCash/commit/fa2fbb7d67d4f86e77871b93ab7ff5bfc6ca4450)

- No mechanism to withdraw allowed tokens from Migrator.sol

All allowed tokens will be locked in the migration contract, as there is currently no function to withdraw them. This poses an issue since the owner may want to either withdraw or burn these tokens.

Acknowledged.

- Limitation on adding additional migrators and special addresses

The contract owner currently lacks the ability to add new migrators for unconventional tokens in the future. Additionally, there is no option to include special addresses, such as farm contracts, that do not require a burn score.

Acknowledged.
