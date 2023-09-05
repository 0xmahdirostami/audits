# mahdiRostami's security audits and findings

> Total H&M: 9 Highs

## Profiles, Username
- Codehawks: [mahdirostami](https://www.codehawks.com/profile/clk52jmr9000el008w4z3a043)<br>
- Code4rena: [mahdirostami](https://code4rena.com/@mahdirostami)<br>
- Sherlock:   mahdirostami<be>

## H&M Finding
- Stakewise v3(Hats.finance)
> - [New Users gain some rewards of old users](https://github.com/hats-finance/StakeWise-0xd91cd6ed6c9a112fdc112b1a3c66e47697f522cd/issues/98)(but wontfix)

- [BeedleFi](https://www.codehawks.com/contests/clkbo1fa20009jr08nyyf9wbx)(Codehawks)
> - [Reentrancy in repay in Lender.sol](https://github.com/Cyfrin/2023-07-beedle/issues/136)
> - [Reentrancy in setPool in Lender.sol](https://github.com/Cyfrin/2023-07-beedle/issues/130)
> - [there is no limit for amount out from uniswap pool](https://github.com/Cyfrin/2023-07-beedle/issues/73)
> - [Reentrancy in seizeLoan in Lender.sol](https://github.com/Cyfrin/2023-07-beedle/issues/137)

- [pooltogether](https://code4rena.com/contests/2023-07-pooltogether)(Code4rena)
> - Anyone can call mintYieldFee and gain _yieldFeeTotalSupply

- [2023-06-real-wagmi](https://app.sherlock.xyz/audits/contests/88)(Sherlock)
> - [Fixed fee in contracting with Uniswap](https://github.com/0xmahdirostami/audits/blob/main/Sherlock/Fixed%20fee%20in%20contracting%20with%20Uniswap.md)

- [superbots](https://immunefi.com/bounty/superbots/)(Immunefi)
> - [Initial depositor can manipulate the price per share value](https://github.com/0xmahdirostami/audits/blob/main/Immunefi/Initial%20depositor%20can%20manipulate%20the%20price%20per%20share%20value.md)(but closed as has already been reported)

- [Asymmetry contest](https://code4rena.com/reports/2023-03-asymmetry)(Code4rena)
> - Lack of slippage bound

## Gas&Low Finding

- [BeedleFi](https://www.codehawks.com/contests/clkbo1fa20009jr08nyyf9wbx)(Codehawks)
> - [Use better name in sellProfits function](https://github.com/Cyfrin/2023-07-beedle/issues/128)

- [Stablecoin](https://www.codehawks.com/contests/cljx3b9390009liqwuedkn0m0)(Codehawks)
> - [Non-library/interface files should use fixed compiler versions, not floating ones](https://github.com/Cyfrin/2023-07-foundry-defi-stablecoin/issues/117)
> - [<x> += <y> costs more gas than <x> = <x> + <y> for state variables](https://github.com/Cyfrin/2023-07-foundry-defi-stablecoin/issues/119)

- [Asymmetry contest](https://code4rena.com/reports/2023-03-asymmetry)(Code4rena)

- [Basin](https://code4rena.com/contests/2023-07-basin)(Code4rena)



