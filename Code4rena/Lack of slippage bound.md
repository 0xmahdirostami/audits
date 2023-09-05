## Unbounded slippage
```
https://github.com/code-423n4/2023-03-asymmetry/blob/44b5cd94ebedc187a08884a7f685e950e987261c/contracts/SafEth/SafEth.sol#L202-L208
```
## Impact
setting high slippage may cause loss in asset value.
## Proof of Concept
There is no upper bound for setting slippage in SafEth.sol and derivatives.
```
function setMaxSlippage(
        uint _derivativeIndex,
        uint _slippage
    ) external onlyOwner {
        derivatives[_derivativeIndex].setMaxSlippage(_slippage);
        emit SetMaxSlippage(_derivativeIndex, _slippage);
    }
```
## Tools Used
Manual review
## Recommended Mitigation Steps
Create an upper bound in SafEth.sol or derivatives, Then check _slippage for being under upper bound.

```
-    function setMaxSlippage(
-        uint _derivativeIndex,
-        uint _slippage
-    ) external onlyOwner {
-        derivatives[_derivativeIndex].setMaxSlippage(_slippage);
-        emit SetMaxSlippage(_derivativeIndex, _slippage);
-    }
+    uint256 public maxSlippageUpperBound = (5 * 10 ** 16); // 5%
+    function setMaxSlippage(
+    uint _derivativeIndex,
+    uint _slippage
+  ) external onlyOwner {
+    require(_slippage < maxSlippageUpperBound);
+    derivatives[_derivativeIndex].setMaxSlippage(_slippage);
+    emit SetMaxSlippage(_derivativeIndex, _slippage);
+  }
```
