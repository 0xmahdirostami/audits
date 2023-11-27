# mahdiRostami's security audits and findings
#### I have availability for smart contract security audits and testing. Reach out to me on [Twitter](https://twitter.com/0xmahdirostami).
- [Private audit and testing Profile](#Private)
- [Competition Profile](#Competition)

# <a name="Private"></a>Private audit and testing
- [Possum lab](https://www.possumlabs.io/) - Testing and last review before deployment after audit competition in Hats.Finance 
# <a name="Competition"></a>Competition
- Hats.Finance: [mahdirostami](https://app.hats.finance/profile/mahdirostami)<br>
- Codehawks: [mahdirostami](https://www.codehawks.com/profile/clk52jmr9000el008w4z3a043)<br>
- Code4rena: [mahdirostami](https://code4rena.com/@mahdirostami)<br>
- Sherlock:  [mahdirostami](https://audits.sherlock.xyz/watson/mahdiRostami)<br>
## H&M Findings
> Total H&M in competitions: 14

- 2023-11-kelp-dao-rseth [:link:](https://code4rena.com/contests/2023-11-kelp-dao-rseth#top)(Code4rena)
> - High-Incorrect Share Calculation in depositAsset Function[:link:](https://github.com/code-423n4/2023-11-kelp-findings/issues/98)
> - High-Risk of Share Manipulation in LRTDepositPool Contract[:link:](https://github.com/code-423n4/2023-11-kelp-findings/issues/99)

- Possum Labs (Portals)[:link:](https://app.hats.finance/audit-competitions/possum-labs-portals-0xed8965d49b8aeca763447d56e6da7f4e0506b2d3)(Hats.finance)
> - Medium-Portal Ignores Principal Token and PSM Price Ratio[:link:](https://github.com/hats-finance/Possum-Labs--Portals--0xed8965d49b8aeca763447d56e6da7f4e0506b2d3/issues/49)
> - Medium-Lack of Function for Receiving ETH[:link:](https://github.com/hats-finance/Possum-Labs--Portals--0xed8965d49b8aeca763447d56e6da7f4e0506b2d3/issues/69)

- 2023-09-venus-prime[:link:](https://code4rena.com/contests/2023-09-venus-prime#top)(Code4rena)
> - High-When minting an "Irrevocable" token, the function fails to delete the stakedAt record for users. This oversight allows users to bypass the staking time requirement after their tokens are burned.[:link:](https://github.com/code-423n4/2023-09-venus-findings/issues/102)

- Convergence-Finance[:link:](https://app.hats.finance/audit-competitions/convergence-finance-ibo-0x0e410e7af8e70fc5bffcdbfbdf1673ee7b3d0777/leaderboard)(Hats.finance)
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
