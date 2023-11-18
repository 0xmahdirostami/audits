# mahdiRostami's security audits and findings

> Total H&M: 12

## Profiles, Username
- Codehawks: [mahdirostami](https://www.codehawks.com/profile/clk52jmr9000el008w4z3a043)<br>
- Code4rena: [mahdirostami](https://code4rena.com/@mahdirostami)<br>
- Sherlock:  [mahdirostami](https://audits.sherlock.xyz/watson/mahdiRostami)<br>
- Hats.finance: [mahdirostami](https://app.hats.finance/profile/mahdirostami)

## H&M Finding

- 2023-11-kelp-dao-rseth [:link:](https://code4rena.com/contests/2023-11-kelp-dao-rseth#top)(Code4rena)
> - Incorrect Share Calculation in depositAsset Function[:link:](https://github.com/code-423n4/2023-11-kelp-findings/issues/98)
> - Risk of Share Manipulation in LRTDepositPool Contract[:link:](https://github.com/code-423n4/2023-11-kelp-findings/issues/99)

- 2023-09-venus-prime[:link:](https://code4rena.com/contests/2023-09-venus-prime#top)(Code4rena)
> - When minting an "Irrevocable" token, the function fails to delete the stakedAt record for users. This oversight allows users to bypass the staking time requirement after their tokens are burned.[:link:](https://github.com/code-423n4/2023-09-venus-findings/issues/102)

- Convergence-Finance[:link:](https://app.hats.finance/audit-competitions/convergence-finance-ibo-0x0e410e7af8e70fc5bffcdbfbdf1673ee7b3d0777/leaderboard)(Hats.finance)
> - Revert in the computeRoi function due to ln calculation[:link:](https://github.com/hats-finance/Convergence-Finance---IBO-0x0e410e7af8e70fc5bffcdbfbdf1673ee7b3d0777/issues/47)

- 2023-07-escrow[:link:](https://www.codehawks.com/contests/cljyfxlc40003jq082s0wemya)(Codehawks)
> - As some tokens balances can be changed over time, arbiter fee must be a percent of the price instead of the fixed value[:link:](https://github.com/Cyfrin/2023-07-escrow/issues/145)

- 2023-07-beedle[:link:](https://www.codehawks.com/contests/clkbo1fa20009jr08nyyf9wbx)(Codehawks)
> - Reentrancy in repay in Lender.sol[:link:](https://github.com/Cyfrin/2023-07-beedle/issues/136)
> - Reentrancy in setPool in Lender.sol[:link:](https://github.com/Cyfrin/2023-07-beedle/issues/130)
> - there is no limit for amount out from uniswap pool[:link:](https://github.com/Cyfrin/2023-07-beedle/issues/73)
> - Reentrancy in seizeLoan in Lender.sol[:link:](https://github.com/Cyfrin/2023-07-beedle/issues/137)

- 2023-07-pooltogether[:link:](https://code4rena.com/contests/2023-07-pooltogether)(Code4rena)
> - Anyone can call mintYieldFee and gain _yieldFeeTotalSupply[:link:](https://github.com/code-423n4/2023-07-pooltogether-findings/issues/365)

- 2023-06-real-wagmi[:link:](https://app.sherlock.xyz/audits/contests/88)(Sherlock)
> - Price slippage in “rebalanceAll” function[:link:](https://github.com/sherlock-audit/2023-06-real-wagmi-judging/issues/22)

- 2023-03-asymmetry[:link:](https://code4rena.com/reports/2023-03-asymmetry)(Code4rena)
> - Lack of slippage bound[:link:](https://github.com/code-423n4/2023-03-asymmetry-findings/issues/24)

## Gas&Low Finding

- DittoETH[:link:](https://www.codehawks.com/contests/clm871gl00001mp081mzjdlwc)(Codehawks)
> - there's a missing unstaking strategy for "RETH." This absence of a clear plan for token burning can impact the overall functionality and management of the token.
[:link:](https://www.codehawks.com/submissions/clm871gl00001mp081mzjdlwc/405)

- 2023-07-beedle[:link:](https://www.codehawks.com/contests/clkbo1fa20009jr08nyyf9wbx)(Codehawks)
> - Use better name in sellProfits function[:link:](https://github.com/Cyfrin/2023-07-beedle/issues/128)

- 2023-07-foundry-defi-stablecoin[:link:](https://www.codehawks.com/contests/cljx3b9390009liqwuedkn0m0)(Codehawks)
> - Non-library/interface files should use fixed compiler versions, not floating ones[:link:](https://github.com/Cyfrin/2023-07-foundry-defi-stablecoin/issues/117)
> - <x> += <y> costs more gas than <x> = <x> + <y> for state variables[:link:](https://github.com/Cyfrin/2023-07-foundry-defi-stablecoin/issues/119)

- 2023-03-asymmetry[:link:](https://code4rena.com/reports/2023-03-asymmetry)(Code4rena)

- 2023-07-basin[:link:](https://code4rena.com/contests/2023-07-basin)(Code4rena)



