## Details
- Report ID
- 21695
- Target
- https://bscscan.com/address/0x820950544E1C37479607204E54b239cD164F457b
- Smart Contract
## Description
- Bug Description
A clear and concise description of the bug. Classic issue with vaults. First depositor can deposit small amount o wei then donate to the vault to greatly inflate share ratio. Due to truncation when converting to shares this can be used to steal funds from later depositors.

## Impact
- the initial depositor can inflate share price, other user (next depositor) can lost their asset
- In
```solidity
shares = (amount * totalSupply()) / _poolSize;
```
As _poolSize will become much bigger than, totalSupply(), Another impact of this bug is that Future depositors are forced to the huge value of the asset to deposit(more than the _poolSize) which It is not practically possible for all the users.
This could directly affect the attrition of users towards this system.
## Risk Breakdown
Difficulty to Exploit: Easy

## Recommendation
Uniswap V2 solved this problem by sending the first 1000 LP tokens to the zero address. The same can be done in this case i.e. when totalSupply()== 0, send the first 1000 mint tokens to the zero address to enable share dilution.
As I said before it's a common issue with vaults. some links to read more about this issue: [1](https://solodit.xyz/issues/h-05-underlying-assets-stealing-in-autopxgmx-and-autopxglp-via-share-price-manipulation-code4rena-redacted-cartel-redacted-cartel-contest-git) [2](https://solodit.xyz/issues/h-03-first-depositor-can-break-minting-of-shares-code4rena-caviar-caviar-contest-git) [3](https://solodit.xyz/issues/h-1-attacker-can-manipulate-the-pricepershare-to-profit-from-future-users-deposits-sherlock-mycelium-mycelium-git)

## References
[https://github.com/upbots/superbots_sc/blob/8534e087634c010bdc6a45e23a86de9fe8f46653/contracts/vault_v2.sol#L244-L250](https://github.com/upbots/superbots_sc/blob/8534e087634c010bdc6a45e23a86de9fe8f46653/contracts/vault_v2.sol#L244-L250) [https://github.com/upbots/superbots_sc/blob/8534e087634c010bdc6a45e23a86de9fe8f46653/contracts/vault_v2.sol#L303-L309](https://github.com/upbots/superbots_sc/blob/8534e087634c010bdc6a45e23a86de9fe8f46653/contracts/vault_v2.sol#L303-L309)

## Proof of Concept
An attacker can exploit using these steps

Deposit small amount X wei baseToken or quoteToken to the vault. At this moment, attacker is minted X wei share token.
Transfer large amount of baseToken or quoteToken directly to the vault, such as 1e9 baseToken or 1e9 quoteToken. Since no new share token is minted, X wei share token worths 1e9 baseToken or 1e9 quoteToken.
Normal users who deposit Y (which is more than 1e9) baseToken or quoteToken to vault and will receive a lot less share token because of rounding division.
share = (Y * X ) / 1e9;

In
```solidity
  calculate share and send back xUBXN
  uint256 shares = 0;
  if (totalSupply() == 0) {
      shares = amount;
  } else {
      shares = (amount * totalSupply()) / _poolSize;
  }
  require(shares > 0, "SC");
  _mint(msg.sender, shares);
```
which _poolSize is
```
  uint256 _before = IERC20(vaultParams.quoteToken).balanceOf(
        address(this)
    );
```
OR
```
    uint256 _before = IERC20(vaultParams.baseToken).balanceOf(
          address(this)
      );
```
