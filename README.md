# mahdiRostami's security audits and findings

> Total H&M: 9

## Profiles, Username
- Codehawks: [mahdirostami](https://www.codehawks.com/profile/clk52jmr9000el008w4z3a043)<br>
- Code4rena: [mahdirostami](https://code4rena.com/@mahdirostami)<br>
- Sherlock:  [mahdirostami](https://audits.sherlock.xyz/watson/mahdiRostami)<br>
- Hats.finance: [mahdirostami](https://app.hats.finance/profile/mahdirostami)

## H&M Finding

- Convergence-Finance(Hats.finance)
> - Revert in the computeRoi function due to lncalculation[:link:](https://github.com/hats-finance/Convergence-Finance---IBO-0x0e410e7af8e70fc5bffcdbfbdf1673ee7b3d0777/issues/47)

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

- 2023-07-beedle[:link:](https://www.codehawks.com/contests/clkbo1fa20009jr08nyyf9wbx)(Codehawks)
> - Use better name in sellProfits function[:link:](https://github.com/Cyfrin/2023-07-beedle/issues/128)

- 2023-07-foundry-defi-stablecoin[:link:](https://www.codehawks.com/contests/cljx3b9390009liqwuedkn0m0)(Codehawks)
> - Non-library/interface files should use fixed compiler versions, not floating ones[:link:](https://github.com/Cyfrin/2023-07-foundry-defi-stablecoin/issues/117)
> - <x> += <y> costs more gas than <x> = <x> + <y> for state variables[:link:](https://github.com/Cyfrin/2023-07-foundry-defi-stablecoin/issues/119)

- 2023-03-asymmetry[:link:](https://code4rena.com/reports/2023-03-asymmetry)(Code4rena)

- 2023-07-basin[:link:](https://code4rena.com/contests/2023-07-basin)(Code4rena)



