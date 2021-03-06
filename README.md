# RationalCrowdsale

A crowdsale contract that can be deployed as-is.

The price of the token is based on its availability: When only 50% of baseAvailability tokens are on the contract, the price will double. At 25% it will quadruple, and so on.

## Flatten

```
./solidityFlattener.pl --mainsol=RationaldCrowdsale.sol
```

## Deployment

You need to provide 3 constructor parameters when deploying the contract:

```solidity
/**
* @param _token The address of the token to be sold
* @param _baseRate How many tokens for 1 ether? The `currentRate()` function will return lower values as tokens are being sold.
* @param _baseAvailability The amount of tokens that should be considered "100%" availability.
*/
constructor(IERC20 _token, uint256 _baseRate, uint256 _baseAvailability) public {
```

### Example

Assume an ERC20 contract at `0x123` with `decimals = 6`, and you want to sell 5000 tokens with a base rate of 20 tokens per ether. You would construct the contract with `token = 0x123`, `baseRate = 20 * 10 ** 6` and `baseAvailability = 5000 * 10 ** 6`.

After deployment, transfer the `baseAvailability` amount of tokens to the contract to make them available for sale.

