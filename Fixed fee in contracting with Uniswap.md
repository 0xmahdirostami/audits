## Summary
"rebalanceAll" function use "getAmountOut" for checking price slippage but "getAmountOut" use  "underlyingTrustedPools[500].poolAddress" for "tickCumulatives" instead of "underlyingTrustedPools[fee].poolAddress".
## Vulnerability Detail
In  "rebalanceAll" function:
```solidity
       uint256 swappedOut = getAmountOut(params.zeroForOne, amountIn);
        if (amountOut < swappedOut) {
            ErrLib.requirement(
                (swappedOut * maxTwapDeviation) / MAX_WEIGHT_UINT256 >= swappedOut - amountOut,
                ErrLib.ErrorCode.PRICE_SLIPPAGE_CHECK
            );
        }
```
"uint256 swappedOut = getAmountOut(params.zeroForOne, amountIn);" used for **PRICE_SLIPPAGE_CHECK**.
But
```solidity
    function getAmountOut(
        bool zeroForOne,
        uint256 amountIn
    ) public view returns (uint256 swappedOut) {
        uint32[] memory secondsAgo = new uint32[](2);
        secondsAgo[0] = twapDuration;
        secondsAgo[1] = 0;
        (int56[] memory tickCumulatives, ) = IUniswapV3Pool(underlyingTrustedPools[500].poolAddress)
```
getAmountOut is using  "underlyingTrustedPools[500].poolAddress" for "tickCumulatives" which should be "underlyingTrustedPools[fee].poolAddress"
.
## Impact
Slippage for all funds during rebalanceAll
## Code Snippet
affected code :
[https://github.com/sherlock-audit/2023-06-real-wagmi-0xmahdirostami/blob/358ec3e22258ae86185c8279ab7ec754bf039c3e/concentrator/contracts/Multipool.sol#L823](https://github.com/sherlock-audit/2023-06-real-wagmi-0xmahdirostami/blob/358ec3e22258ae86185c8279ab7ec754bf039c3e/concentrator/contracts/Multipool.sol#L823)
## Tool used
Manual Review
## Recommendation
use "underlyingTrustedPools[fee].poolAddress" instead of "underlyingTrustedPools[500].poolAddress".
