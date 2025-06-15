---
title: TopCut Audit Report
author: 0xmahdirostami
date: June 7, 2025
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
    {\Huge\bfseries TopCut Audit Report\par}
    \vspace{1cm}
    {\Large Version 1.0\par}
    \vspace{2cm}
    {\Large\itshape Mahdi Rostami\par}
    \vfill
    {\large \today\par}
\end{titlepage}

\maketitle

<!-- Your report starts here! -->

Prepared by: Mahdi Rostami [[Twitter]](https://x.com/0xmahdirostami)

# Table of Contents

- [Table of Contents](#table-of-contents)
- [TopCut Security Review](#topcut-security-review)
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
    - [\[M-1\] Incorrect Affiliate Points Redemption Logic Causes Reward Dilutio](#m-1-incorrect-affiliate-points-redemption-logic-causes-reward-dilutio)
    - [\[M-2\] Excessive Maximum Cohort Size May Cause Out-of-Gas Errors](#m-2-excessive-maximum-cohort-size-may-cause-out-of-gas-errors)
    - [\[M-3\] Missing Sequencer Uptime Check When Using Chainlink Oracle on L2](#m-3-missing-sequencer-uptime-check-when-using-chainlink-oracle-on-l2)
    - [\[M-4\] Incomplete Chainlink Oracle Data Validation Allows Stale or Invalid Prices](#m-4-incomplete-chainlink-oracle-data-validation-allows-stale-or-invalid-prices)
  - [Low Severity](#low-severity)
    - [\[L-1\] Inefficient Initial Settlement Timing](#l-1-inefficient-initial-settlement-timing)
    - [\[L-2\] Inefficient Claim Handling Prevents Partial Withdrawals](#l-2-inefficient-claim-handling-prevents-partial-withdrawals)
    - [\[L-3\] Missing Cohort ID Input in castPrediction Can Lead to Incorrect Cohort Assignment](#l-3-missing-cohort-id-input-in-castprediction-can-lead-to-incorrect-cohort-assignment)
    - [\[L-4\] Insufficient Keeper Incentives for Small/Empty Cohort Settlement](#l-4-insufficient-keeper-incentives-for-smallempty-cohort-settlement)
  - [Info](#info)


# TopCut Security Review

A security review of the [ Possum-labs ](https://www.possumlabs.io/), [TopCut](https://github.com/PossumLabsCrypto/TopCut) smart contracts was done by [mahdi rostami](https://twitter.com/0xmahdirostami) . \
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

| Project Name |                                                TopCut                                                |
| :----------: | :--------------------------------------------------------------------------------------------------: |
|  Repository  |                          [Link](https://github.com/PossumLabsCrypto/TopCut)                          |
| Commit Hash  | [ce88e7](https://github.com/PossumLabsCrypto/TopCut/commit/ce88e78ebd782fc88399f9122a4e66febadf7f9d) |
|     Docs     |                                               No docs                                                |
|   Methods    |                                            Manual Review                                             |

### Scope

|  File  |
| :----: |
| TopCut |

### Compatibilities

- Solc Version: 0.8.19
- Chain(s) to deploy contract to: Arbitrum

### Known Issues

None

### Issues found

|   Severity    | Count |
| :-----------: | :---: |
|     High      |   0   |
|    Medium     |   4   |
|      Low      |   4   |
| Informational |   6   |

# Findings
## Medium Severity
### [M-1] Incorrect Affiliate Points Redemption Logic Causes Reward Dilutio

**Description:** In the claimAffiliateReward function, the contract incorrectly adds affiliatePoints[_refID] (the total accumulated points) to totalRedeemedAP instead of _pointsRedeemed (the number of points being redeemed in the current transaction). This causes totalRedeemedAP to increase much faster than intended, leading to reward dilution for subsequent users or for users redeeming rewards in multiple transactions. As a result, the economic model of the affiliate rewards system is compromised.

**Location:** [link](https://github.com/PossumLabsCrypto/TopCut/blob/ce88e78ebd782fc88399f9122a4e66febadf7f9d/src/TopCutVault.sol#L192-L193)

**Code:**
```solidity
    totalRedeemedAP = (totalRedeemedAP + affiliatePoints[_refID] < MAX_AP_REDEEMED)
        ? totalRedeemedAP + affiliatePoints[_refID]
```

**Mitigation:**  Update the logic to increment totalRedeemedAP by the actual number of points being redeemed in the current transaction:
```solidity
    totalRedeemedAP = (totalRedeemedAP + _pointsRedeemed < MAX_AP_REDEEMED)
        ? totalRedeemedAP + _pointsRedeemed
```
**Remark:**

Fixed. [commit](https://github.com/PossumLabsCrypto/TopCut/commit/16353f490b970e5b602c1212f4ec6a6a84e4307e)


### [M-2] Excessive Maximum Cohort Size May Cause Out-of-Gas Errors

**Description:** The current _maxCohortSize is set to 3300, which can lead to significant gas consumption. For example, a test with 3300 participants used at least 22,493,443 gas. Given that the Arbitrum block gas limit is 30,000,000, this could cause transactions to fail due to out-of-gas errors in production.
The impact is high as both cohort users will lose money.

**Location:** [link](https://github.com/PossumLabsCrypto/TopCut/blob/ce88e78ebd782fc88399f9122a4e66febadf7f9d/src/TopCutMarket.sol#L47)

**Code:**
```solidity
        if (_maxCohortSize < 330 || _maxCohortSize > 3300) revert InvalidConstructor();
```

**Mitigation:** Reduce the maximum allowed cohort size to ensure gas usage stays within safe limits.

**Remark:**
Fixed. [commit](https://github.com/PossumLabsCrypto/TopCut/commit/24dfe1a6b56d0059b73a976d96b626b84e40b83a)

### [M-3] Missing Sequencer Uptime Check When Using Chainlink Oracle on L2

**Description:** Using Chainlink on L2 chains like Arbitrum requires checking the sequencer's status to prevent stale or manipulated prices during sequencer downtime. Without this check, malicious actors could exploit periods when the sequencer is down, as oracle prices may appear fresh but are not reliable.

**Location:** [link](https://github.com/PossumLabsCrypto/TopCut/blob/ce88e78ebd782fc88399f9122a4e66febadf7f9d/src/TopCutMarket.sol#L176-L183)

**Code:**
```solidity
    ///@dev Get the settlement price and timestamp from the oracle
    (, int256 price,, uint256 updatedAt,) = ORACLE.latestRoundData();


    ///@dev Ensure that the oracle price was updated after or at the settlement time
    if (updatedAt < settlementTime) revert StaleOraclePrice();


    ///@dev Sanity check to filter out a bad oracle feed (0 or negative)
    if (price < 1) revert BrokenOraclePrice();
```

**Mitigation:** Follow Chainlink's recommended approach link for L2 sequencer feeds to ensure the sequencer is up and a grace period has passed before using oracle data.

**Remark:**
Fixed. [commit](https://github.com/PossumLabsCrypto/TopCut/commit/3e725ef1579a89813c7ab854c1abf9c941f85c24) & [commit](https://github.com/PossumLabsCrypto/TopCut/commit/0c8c0b8b36b608f593ab457422e0848d45d7f2c7)

### [M-4] Incomplete Chainlink Oracle Data Validation Allows Stale or Invalid Prices 

**Description:** The contract's current validation of Chainlink oracle data is insufficient. It only checks if updatedAt is greater than or equal to settlementTime and that price is positive. However, this approach does not ensure that the oracle data is fresh or finalized. Specifically, it does not verify that answeredInRound matches roundId, nor does it check if updatedAt is recent relative to block.timestamp. As a result, stale or incomplete price data could be processed, potentially leading to incorrect settlements or vulnerabilities.

**Location:** [link](https://github.com/PossumLabsCrypto/TopCut/blob/ce88e78ebd782fc88399f9122a4e66febadf7f9d/src/TopCutMarket.sol#L176-L183)

**Code:**
```solidity
        ///@dev Get the settlement price and timestamp from the oracle
        (, int256 price,, uint256 updatedAt,) = ORACLE.latestRoundData();


        ///@dev Ensure that the oracle price was updated after or at the settlement time
        if (updatedAt < settlementTime) revert StaleOraclePrice();


        ///@dev Sanity check to filter out a bad oracle feed (0 or negative)
        if (price < 1) revert BrokenOraclePrice();
```

**Mitigation:** 
```solidity
function getSecurePrice() external view returns (int256) {
    (
        uint80 roundId,
        int256 price,
        uint256 startedAt,
        uint256 updatedAt,
        uint80 answeredInRound
    ) = priceFeed.latestRoundData();
    
    // Check for stale data
    require(answeredInRound >= roundId, "Stale price data");
    
    // Check for round completion
    require(updatedAt != 0, "Round not complete");
    
    // Check for price freshness (e.g., within last 3600 seconds)
    require(block.timestamp - updatedAt <= STALENESS_THRESHOLD, "Price too old");
    
    if (updatedAt < settlementTime) revert StaleOraclePrice();

    // Check for valid price
    require(price > 0, "Invalid price");
    
    return price;
```

**Remark:**
Fixed. [commit](https://github.com/PossumLabsCrypto/TopCut/commit/3e725ef1579a89813c7ab854c1abf9c941f85c24) & [commit](https://github.com/PossumLabsCrypto/TopCut/commit/0c8c0b8b36b608f593ab457422e0848d45d7f2c7)

## Low Severity

### [L-1] Inefficient Initial Settlement Timing

**Description:** In the first round, nextSettlement is set to a value greater than _tradeDuration * 2. This causes the settlement for the first cohort to occur at least at block.timestamp + _tradeDuration * 2 + _tradeDuration, introducing unnecessary delay.

**Location:** [link](https://github.com/PossumLabsCrypto/TopCut/blob/ce88e78ebd782fc88399f9122a4e66febadf7f9d/src/TopCutMarket.sol#L57)

**Code:**
```solidity
        if (_firstSettlementTime < block.timestamp + _tradeDuration * 2) revert InvalidConstructor();
```

**Mitigation:** Check _firstSettlementTime to be >= block.timestamp + _tradeDuration.

**Remark:**
Fixed. [commit](https://github.com/PossumLabsCrypto/TopCut/commit/76614152111f2805fee566b4003af4012fcd0763) 

### [L-2] Inefficient Claim Handling Prevents Partial Withdrawals

**Description:** The claim function attempts to transfer the entire claimable amount for a user in a single transaction. If the contract's balance is insufficient to cover the full amount, the transaction reverts, preventing the user from withdrawing any portion of their claim. This approach is inefficient, especially for users with large claim amounts who may prefer to withdraw available funds incrementally.

**Location:** [link](https://github.com/PossumLabsCrypto/TopCut/blob/ce88e78ebd782fc88399f9122a4e66febadf7f9d/src/TopCutMarket.sol#L275)

**Code:**
```solidity
    uint256 amount = claimAmounts[user];
```

**Mitigation:** Allow users to specify the amount they wish to claim, enabling partial withdrawals when the contract balance cannot cover the full claim.

**Remark:**
Acknowledged.

### [L-3] Missing Cohort ID Input in castPrediction Can Lead to Incorrect Cohort Assignment

**Description:** We found that castPrediction does not take a cohortId as an input. As a result, if a transaction is delayed by the frontend or for other reasons, the prediction may be cast into an unexpected cohort.

**Location:** [link](https://github.com/PossumLabsCrypto/TopCut/blob/ce88e78ebd782fc88399f9122a4e66febadf7f9d/src/TopCutMarket.sol#L114)

**Mitigation:** Require the cohort ID as an input to castPrediction and validate it to ensure predictions are assigned to the intended cohort.

**Remark:**
Fixed. [commit](https://github.com/PossumLabsCrypto/TopCut/commit/e482bba960b2d2031d91afdf2ef086640a61b869)  

### [L-4] Insufficient Keeper Incentives for Small/Empty Cohort Settlement

**Description:** Currently, keepers receive rewards proportional to cohort size (_cohortSize * TRADE_SIZE * SHARE_KEEPER), creating a disincentive to process small or empty cohorts. This leads to timing issues as these cohorts may be neglected, potentially disrupting the protocol's expected settlement schedule and causing operational delays.

**Location:** [link](https://github.com/PossumLabsCrypto/TopCut/blob/ce88e78ebd782fc88399f9122a4e66febadf7f9d/src/TopCutMarket.sol#L259-L264)

**Code:**
```solidity
        // INTERACTIONS
        ///@dev Compensate the keeper based on the number of traders in the Cohort
        uint256 keeperReward = (_cohortSize * TRADE_SIZE * SHARE_KEEPER) / SHARE_PRECISION;


        (bool sent,) = payable(msg.sender).call{value: keeperReward}("");
        if (!sent) revert FailedToSendKeeperReward();
```

**Mitigation:** Implement a minimum base reward for keepers regardless of cohort size to ensure all cohorts are processed in a timely manner,
Replace the direct transfer mechanism with a claimable reward system to handle cases where contract funds are insufficient.

**Remark:**
Fixed. [commit](https://github.com/PossumLabsCrypto/TopCut/commit/c857ae969755bc9a04a1a004c49cf84cd125d376)  

## Info
1. The error `FailedToSkimSurplus();` is declared but not used in `TopCutMarket`.
2. In `castPrediction()`, it's preferable to compare `msg.value` with the immutable `TRADE_SIZE` and proceed using `TRADE_SIZE` instead of introducing a new `tradeSize` variable.
3. The variables `vaultReward` and `frontendReward` can be declared as `immutable` and calculated in the constructor for improved efficiency and clarity.
4. The comparison of `currentMaxValue` in `settleCohort` currently favors later users over the first user. To ensure the later user with the maximum value is selected, update the comparison from `diff > currentMaxValue` to `diff >= currentMaxValue`:

```diff
-    if (diff > currentMaxValue) {
+    if (diff >= currentMaxValue) {
    currentMaxValue = diff;
    currentMaxIndex = i;
    }
```
5. The error `FailedToSendNativeToken();` is declared but not used in `TopCutNFT`.
6. The `activeCohortID` variable is currently private, preventing users from viewing which cohort they are casting into; make it `public` to improve transparency.

**Remark:**
Fixed. [commit](https://github.com/PossumLabsCrypto/TopCut/commit/181500933ba66deef62c3d2a463ebe30ff03bbd8) & [commit](https://github.com/PossumLabsCrypto/TopCut/commit/6abcaff0be9f6e9a6cbd6d44e21dd699bcafcff4)