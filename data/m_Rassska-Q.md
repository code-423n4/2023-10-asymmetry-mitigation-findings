# Lines of code

https://github.com/asymmetryfinance/afeth/blob/main/contracts/AfEth.sol#L289-L291


# Vulnerability details


* In the following [PR](https://github.com/asymmetryfinance/afeth/pull/167/commits/e24bb9bffa66cda4289f5ecb0e33ccaac490cfcb), upon requesting withdrawal, `votiumWithdrawAmount` is being passed to determine the time, which is completely how it's supposed to be. However, the function `AfEth.withdrawTime()`, which is exposed to a public access doesn't account it.


## Mitigation
* Instead of sending an `afEth` amount into `AbstractStrategy(vEthAddress).withdrawTime(_amount)`, it should compute the amount of vAfEth corresponding to a specified amount of `afEth` and determine the time based on that.
  
## Recommended Steps:
* Short term:
  * Send afETH from `afEth.requestWithdraw()` to `afEth.withdrawTime()` and inside of `afEth.withdrawTime()` compute `votiumWithdrawAmount` which has to be sent to determine the actual withdrawal time.


## Assessed type

Context