# mahdiRostami's security audits and findings

> Total H&M: 11

## Profiles, Username
- Codehawks: mahdirostami[:link:](https://www.codehawks.com/profile/clk52jmr9000el008w4z3a043)<br>
- Code4rena: mahdirostami[:link:](https://code4rena.com/@mahdirostami)<br>
- Sherlock:  mahdirostami[:link:](https://audits.sherlock.xyz/watson/mahdiRostami)<br>
- Hats.finance: wallet address 

## H&M Finding

- Convergence-Finance(Hats.finance)
> - Revert in the computeRoi function due to lncalculation[:link:](https://github.com/hats-finance/Convergence-Finance---IBO-0x0e410e7af8e70fc5bffcdbfbdf1673ee7b3d0777/issues/47)

- CodeHawks Escrow Contract[:link:](https://www.codehawks.com/contests/cljyfxlc40003jq082s0wemya)(Codehawks)
> - As some tokens balances can be changed over time, arbiter fee must be a percent of the price instead of the fixed value[:link:](https://github.com/Cyfrin/2023-07-escrow/issues/145)

- Stakewise v3(Hats.finance)
> - New Users gain some rewards of old users[:link:](https://github.com/hats-finance/StakeWise-0xd91cd6ed6c9a112fdc112b1a3c66e47697f522cd/issues/98)(but wontfix)

- BeedleFi[:link:](https://www.codehawks.com/contests/clkbo1fa20009jr08nyyf9wbx)(Codehawks)
> - Reentrancy in repay in Lender.sol[:link:](https://github.com/Cyfrin/2023-07-beedle/issues/136)
> - Reentrancy in setPool in Lender.sol[:link:](https://github.com/Cyfrin/2023-07-beedle/issues/130)
> - there is no limit for amount out from uniswap pool[:link:](https://github.com/Cyfrin/2023-07-beedle/issues/73)
> - Reentrancy in seizeLoan in Lender.sol[:link:](https://github.com/Cyfrin/2023-07-beedle/issues/137)

- pooltogether[:link:](https://code4rena.com/contests/2023-07-pooltogether)(Code4rena)
> - Anyone can call mintYieldFee and gain _yieldFeeTotalSupply[:link:](https://github.com/0xmahdirostami/audits/blob/main/Code4rena/anyone%20can%20call%20mintYieldFee%20and%20gain%20_yieldFeeTotalSupply.md)

- 2023-06-real-wagmi[:link:](https://app.sherlock.xyz/audits/contests/88)(Sherlock)
> - Fixed fee in contracting with Uniswap[:link:](https://github.com/0xmahdirostami/audits/blob/main/Sherlock/Fixed%20fee%20in%20contracting%20with%20Uniswap.md)

- superbots[:link:](https://immunefi.com/bounty/superbots/)(Immunefi)
> - Initial depositor can manipulate the price per share value[:link:](https://github.com/0xmahdirostami/audits/blob/main/Immunefi/Initial%20depositor%20can%20manipulate%20the%20price%20per%20share%20value.md)(but closed as has already been reported)

- Asymmetry contest[:link:](https://code4rena.com/reports/2023-03-asymmetry)(Code4rena)
> - Lack of slippage bound[:link:](https://github.com/0xmahdirostami/audits/blob/main/Code4rena/Lack%20of%20slippage%20bound.md)

## Gas&Low Finding

- BeedleFi[:link:](https://www.codehawks.com/contests/clkbo1fa20009jr08nyyf9wbx)(Codehawks)
> - Use better name in sellProfits function[:link:](https://github.com/Cyfrin/2023-07-beedle/issues/128)

- Stablecoin[:link:](https://www.codehawks.com/contests/cljx3b9390009liqwuedkn0m0)(Codehawks)
> - Non-library/interface files should use fixed compiler versions, not floating ones[:link:](https://github.com/Cyfrin/2023-07-foundry-defi-stablecoin/issues/117)
> - <x> += <y> costs more gas than <x> = <x> + <y> for state variables[:link:](https://github.com/Cyfrin/2023-07-foundry-defi-stablecoin/issues/119)

- Asymmetry contest[:link:](https://code4rena.com/reports/2023-03-asymmetry)(Code4rena)

- Basin[:link:](https://code4rena.com/contests/2023-07-basin)(Code4rena)



