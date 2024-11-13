# Seipex Fair Launch Platform

Seipex allows anyone to create and purchase ERC20 tokens on https://seipex.fi using Sei. The platform uses an AMM mechanism to automatically adjust token prices based on purchase volume, ensuring fair price discovery and distribution.

## Contract Address
```
0xe70AAa288F801B208074171be87b804178Ce5d11
```

## Core Functionality

### Token Purchase
```solidity
function buyTokens(address token) external payable
```
Purchase tokens with Sei by sending the desired amount of Sei along with the transaction.
- Automatically calculates token amount based on the current bonding curve
- Price increases with each purchase, following the AMM curve
- Emits a `TokensPurchased` event with purchase details

### Token Sales
```solidity
function sellTokens(address token, uint256 tokenAmount) external
```
Sell tokens back to the platform in exchange for Sei.
- Returns Sei based on the current bonding curve price
- Price decreases with each sale, following the AMM curve
- Emits a `TokensSold` event with sale details

### Price Estimation
```solidity
function estimateBuy(address token, uint256 ethAmount) public view returns (uint256)
```
Calculate expected token amount for a given Sei input.
- Helps users estimate their output before buying

```solidity
function estimateSell(address token, uint256 tokenAmount) public view returns (uint256)
```
Calculate expected Sei return for a given token amount.
- Helps users estimate their output before selling

### Token Information
```solidity
function getTokenMetadata(address token) external view returns (TokenMetadata memory)
```
Retrieve detailed information about a launched token.
- Returns metadata including name, symbol, and supply as well as socials
- Only works for tokens launched through Seipex

```solidity
function getLiquidity(address token) public view returns (uint256 seiReserve, uint256 tokenReserve)
```
Check current liquidity reserves for a token.
- Returns both Sei and token reserves

## Events

### Token Creation
```solidity
event TokenCreated(
    address tokenAddress,
    string name,
    string symbol,
    uint256 totalSupply,
    uint256 initialPurchaseAmount
)
```
Emitted when a new token is launched on the platform.

### Purchase Tracking
```solidity
event TokensPurchased(
    address indexed token,
    address buyer,
    uint256 seiIn,
    uint256 tokensOut,
    uint256 price,
    uint256 timestamp
)
```
Emitted by all token purchases with detailed information.

### Sale Tracking
```solidity
event TokensSold(
    address indexed token,
    address seller,
    uint256 tokensIn,
    uint256 seiOut,
    uint256 price,
    uint256 timestamp
)
```
Emitted by all token sales with detailed information.

### Token Bonding
```solidity
event TokenBonded(
    address indexed token
)
```
Emitted when a token is successfully bonded on DragonSwap.