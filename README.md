# mahdiRostami's security audits and findings
### I have availability for Priave Smart Contract Security Audits (pay-per-vulnerability), and Testing. 
##### Reach out to me on [Twitter](https://twitter.com/0xmahdirostami) OR Rostamimahdi1997@gmail.com.

***
Supported Languages: 
> - Solidity
> - Rust
> - Vyper

# <a name="Private"></a>Private audit, Testing, Development Profile

| Name       | Date          | Language | Site                                    | Company                                   | Action                            | GitHub Link                                                                                     |
| ---------- | ------------- | -------- | --------------------------------------- | ----------------------------------------- | --------------------------------- | ----------------------------------------------------------------------------------------------- |
| Portals    | 2024-March    | Solidity | coming...                               | [Possum lab](https://www.possumlabs.io/)  | Private Audit                     | coming...                                               |
| HLP Adapter| 2024-January  | Solidity | coming...                               | [Possum lab](https://www.possumlabs.io/)  | Development and Testing(foundry)  | [Link](https://github.com/0xmahdirostami/Adapters)      |
| Time Rift  | 2023-December | Solidity | [Link](https://timerift.possumlabs.io/) | [Possum lab](https://www.possumlabs.io/)  | Private Audit                     | [Link](https://github.com/0xmahdirostami/audits/tree/main/Private-audit/Time%20Rift/report.pdf) | 
| HLP Portal | 2023-November | Solidity | [Link](https://portals.possumlabs.io/)  | [Possum lab](https://www.possumlabs.io/)  | Testing(foundry)                  | [Link](https://github.com/PossumLabsCrypto/Portals/blob/main/test/V1/PortalUnit.t.sol)          | 

# <a name="Top"></a>Top public audits

| Audit Contest | Date            | Language | Rank | Results                                                                                                                        | Host         | 
| ------------- | --------------- | -------- | ---- | ------------------------------------------------------------------------------------------------------------------------------ | ------------ |
| Alephzero     |  2024-February  | Ink      | 2st  | [Link](https://app.hats.finance/audit-competitions/alephzeroamm-0x0d88a9ece90994ecb3ba704730819d71c139f60f/leaderboard)        | Hats.Finance |
| Possum        |  2023-November  | Solidity | 1st  | [Link](https://app.hats.finance/audit-competitions/possum-labs-portals-0xed8965d49b8aeca763447d56e6da7f4e0506b2d3/leaderboard) | Hats.Finance |
| Convergence   |  2023-September | Solidity | 2st  | [Link](https://app.hats.finance/audit-competitions/convergence-finance-0x0e410e7af8e70fc5bffcdbfbdf1673ee7b3d0777/leaderboard) | Hats.Finance |

# <a name="Competition"></a>Competition Profile

| Host          | Profile Name  | Link                                                                |  
| ------------- | ------------- | ------------------------------------------------------------------- |
| Hats.Finance  |  mahdirostami | [Link](https://app.hats.finance/profile/mahdirostami)               |
| Codehawks     |  mahdirostami | [Link](https://www.codehawks.com/profile/clk52jmr9000el008w4z3a043) | 
| Code4rena     |  mahdirostami | [Link](https://code4rena.com/@mahdirostami)                         | 
| Sherlock      |  mahdirostami | [Link](https://audits.sherlock.xyz/watson/mahdiRostami)             |

## H&M Findings

> Total H&M in competitions: 27

- 2024-1-The Standard [:link:](https://www.codehawks.com/contests/clql6lvyu0001mnje1xpqcuvl)(Codehawks)
> - High-Unbounded pendingStakes could result in DOS in LiquidationPool
> - Medium-Passing block.timestamp instead of deadline argument in SmartVaultV3::swap.
> - Medium-Fees are hardcoded to 3000 in ExactInputSingleParams

- 2024-01-curves [:link:](https://code4rena.com/audits/2024-01-curves#top)(Code4rena)
> - High-Users Can Exploit Fee Rewards System by Repeatedly Depositing and Withdrawing Curve Tokens [:link:](https://github.com/code-423n4/2024-01-curves-findings/issues/642)
> - High-FeeSplitter:setCurves lacks access control, allowing anyone to change curves [:link:](https://github.com/code-423n4/2024-01-curves-findings/issues/597)
> - High-Potential Denial of Service (DoS) Vulnerability in `_transferFees`, Due to transferring fee to `curvesTokenSubject` and `referralFeeDestination` [:link:](https://github.com/code-423n4/2024-01-curves-findings/issues/527)
> - Medium-User `userFeeOffset` Reset Without Adding to Unclaimed Fee Every Time User Buys or Sells Tokens [:link:](https://github.com/code-423n4/2024-01-curves-findings/issues/630)
> - Medium-Remainder of ETH not returned to user in _buyCurvesToken [:link:](https://github.com/code-423n4/2024-01-curves-findings/issues/589)
> - Medium-Protocol Fee and Referral Fee Stuck in Contract During Sell Operation [:link:](https://github.com/code-423n4/2024-01-curves-findings/issues/525)

- 2023-12-revolutionprotocol [:link:](https://code4rena.com/audits/2023-12-revolution-protocol#top)(Code4rena)
> - Medium-Potential Exploitable Behavior in AuctionHouse::_settleAuction[:link:](https://github.com/code-423n4/2023-12-revolutionprotocol-findings/issues/546)
> - Medium-Potential Dos in AuctionHouse::_settleAuction, due to Not checking RewardSplits::minPurchaseAmount,RewardSplits::maxPurchaseAmount[:link:](https://github.com/code-423n4/2023-12-revolutionprotocol-findings/issues/558)
> - Medium-Unfair Quorum Votes Calculation for Pieces at Creation Time[:link:](https://github.com/code-423n4/2023-12-revolutionprotocol-findings/issues/43)

- 2023-11-kelp-dao-rseth [:link:](https://code4rena.com/contests/2023-11-kelp-dao-rseth#top)(Code4rena)
> - High-Incorrect Share Calculation in depositAsset Function[:link:](https://github.com/code-423n4/2023-11-kelp-findings/issues/98)
> - High-Risk of Share Manipulation in LRTDepositPool Contract[:link:](https://github.com/code-423n4/2023-11-kelp-findings/issues/99)

- 2023-11-Possum Labs (Portals)[:link:](https://app.hats.finance/audit-competitions/possum-labs-portals-0xed8965d49b8aeca763447d56e6da7f4e0506b2d3)(Hats.finance)
> - Medium-Portal Ignores Principal Token and PSM Price Ratio[:link:](https://github.com/hats-finance/Possum-Labs--Portals--0xed8965d49b8aeca763447d56e6da7f4e0506b2d3/issues/49)
> - Medium-Lack of Function for Receiving ETH[:link:](https://github.com/hats-finance/Possum-Labs--Portals--0xed8965d49b8aeca763447d56e6da7f4e0506b2d3/issues/69)

- 2023-10-zksync-findings [:link:](https://code4rena.com/audits/2023-10-zksync-era#top)(Code4rena)
> - Medium-Deposit Limit Check Issue with Bridges in _verifyDepositLimit Function[:link:](https://github.com/code-423n4/2023-12-revolutionprotocol-findings/issues/546)

- 2023-09-venus-prime[:link:](https://code4rena.com/contests/2023-09-venus-prime#top)(Code4rena)
> - High-When minting an "Irrevocable" token, the function fails to delete the stakedAt record for users. This oversight allows users to bypass the staking time requirement after their tokens are burned.[:link:](https://github.com/code-423n4/2023-09-venus-findings/issues/102)

- 2023-09-Convergence-Finance[:link:](https://app.hats.finance/audit-competitions/convergence-finance-ibo-0x0e410e7af8e70fc5bffcdbfbdf1673ee7b3d0777/leaderboard)(Hats.finance)
> - Medium-Revert in the computeRoi function due to ln calculation[:link:](https://github.com/hats-finance/Convergence-Finance---IBO-0x0e410e7af8e70fc5bffcdbfbdf1673ee7b3d0777/issues/47)

- 2023-07-escrow[:link:](https://www.codehawks.com/contests/cljyfxlc40003jq082s0wemya)(Codehawks)
> - Medium-As some tokens balances can be changed over time, arbiter fee must be a percent of the price instead of the fixed value[:link:](https://github.com/Cyfrin/2023-07-escrow/issues/145)

- 2023-07-beedle[:link:](https://www.codehawks.com/contests/clkbo1fa20009jr08nyyf9wbx)(Codehawks)
> - High-Reentrancy in repay in Lender.sol[:link:](https://github.com/Cyfrin/2023-07-beedle/issues/136)
> - High-Reentrancy in setPool in Lender.sol[:link:](https://github.com/Cyfrin/2023-07-beedle/issues/130)
> - High-there is no limit for amount out from uniswap pool[:link:](https://github.com/Cyfrin/2023-07-beedle/issues/73)
> - High-Reentrancy in seizeLoan in Lender.sol[:link:](https://github.com/Cyfrin/2023-07-beedle/issues/137)

- 2023-07-pooltogether[:link:](https://code4rena.com/contests/2023-07-pooltogether)(Code4rena)
> - High-Anyone can call mintYieldFee and gain _yieldFeeTotalSupply[:link:](https://github.com/code-423n4/2023-07-pooltogether-findings/issues/365)

- 2023-06-real-wagmi[:link:](https://app.sherlock.xyz/audits/contests/88)(Sherlock)
> - High-Price slippage in “rebalanceAll” function[:link:](https://github.com/sherlock-audit/2023-06-real-wagmi-judging/issues/22)

- 2023-03-asymmetry[:link:](https://code4rena.com/reports/2023-03-asymmetry)(Code4rena)
> - High-Lack of slippage bound[:link:](https://github.com/code-423n4/2023-03-asymmetry-findings/issues/24)
