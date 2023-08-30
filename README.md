# mahdiRostami's security audits and findings
## 1.Codehawks
[Profile](https://www.codehawks.com/profile/clk52jmr9000el008w4z3a043)

**1.1 H&M Finding:**

- [BeedleFi](https://www.codehawks.com/contests/clkbo1fa20009jr08nyyf9wbx)

> - Reentrancy in repay in Lender.sol
> - Reentrancy in setPool in Lender.sol
> - there is no limit for amount out from uniswap pool
> -  Reentrancy in seizeLoan in Lender.sol

**1.2 Gas&Low Finding:**

- [BeedleFi](https://www.codehawks.com/contests/clkbo1fa20009jr08nyyf9wbx)

> - Use better name in sellProfits function


- [Stablecoin](https://www.codehawks.com/contests/cljx3b9390009liqwuedkn0m0)

> - Non-library/interface files should use fixed compiler versions, not floating ones
> - <x> += <y> costs more gas than <x> = <x> + <y> for state variables

## 2.Code4rena
[Profile](https://code4rena.com/@mahdirostami)

**2.1 H&M Finding:**

- [pooltogether](https://code4rena.com/contests/2023-07-pooltogether)

> - Anyone can call mintYieldFee and gain _yieldFeeTotalSupply

- [Asymmetry contest](https://code4rena.com/reports/2023-03-asymmetry)

> - Lack of slippage bound

**2.2 Gas&Low Finding:**

- [Asymmetry contest](https://code4rena.com/reports/2023-03-asymmetry)

- [Basin](https://code4rena.com/contests/2023-07-basin) 


## 3.Immunefi

**3.1 H&M Finding:**

- [superbots](https://immunefi.com/bounty/superbots/)

> - Initial depositor can manipulate the price per share value(but closed as has already been reported)

## 4.Hats.finance

**4.1 H&M Finding:**

- Stakewise v3

> - [Initial depositor can manipulate the price per share value](https://github.com/hats-finance/StakeWise-0xd91cd6ed6c9a112fdc112b1a3c66e47697f522cd/issues/98)(but wontfix)
