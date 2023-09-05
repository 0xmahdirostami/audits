# anyone can call mintYieldFee and gain _yieldFeeTotalSupply
## Impact
stole all _yieldFeeTotalSupply from vault
## Proof of Concept
In
```solidity
  function mintYieldFee(uint256 _shares, address _recipient) external {
    _requireVaultCollateralized();
    if (_shares > _yieldFeeTotalSupply) revert YieldFeeGTAvailable(_shares, _yieldFeeTotalSupply);


    _yieldFeeTotalSupply -= _shares;
    _mint(_recipient, _shares);


    emit MintYieldFee(msg.sender, _recipient, _shares);
  }
```
anyone call this function and get all _yieldFeeTotalSupply
## Tools Used
manual
## Recommended Mitigation Steps
remove address _recipient and mint for _yieldFeeRecipient
```diff
-  function mintYieldFee(uint256 _shares, address _recipient) external {
+  function mintYieldFee(uint256 _shares) external { //@audit high anyone can call use _yieldFeeRecipient for recipent instead
     _requireVaultCollateralized();
     if (_shares > _yieldFeeTotalSupply) revert YieldFeeGTAvailable(_shares, _yieldFeeTotalSupply);
 
     _yieldFeeTotalSupply -= _shares;
-    _mint(_recipient, _shares);
+    _mint(_yieldFeeRecipient, _shares);
```
