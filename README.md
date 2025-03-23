# AirdropX Distribution Smart Contract

## Overview
This smart contract enables the decentralized distribution of tokens via an airdrop mechanism. It supports recipient eligibility verification, claim tracking, tiered distribution, emergency withdrawals, and reclaiming unclaimed tokens after a set period. Additionally, it includes pause/resume functionality for security and governance.

## Features
- **Recipient Eligibility**: Only pre-approved addresses can claim airdrop tokens.
- **One-Time Claims**: Prevents double claiming by tracking recipients.
- **Tiered Distribution**: Allows for different claim amounts based on recipient tiers.
- **Reclaim Mechanism**: Unclaimed tokens are burned after a defined period.
- **Emergency Withdrawals**: Admin can withdraw funds after a timelock delay.
- **Pause/Resume Functionality**: Airdrop can be paused and resumed by the contract owner.
- **Event Logging**: Tracks key contract activities for transparency.

## Constants
| Constant | Description |
|----------|-------------|
| `CONTRACT-OWNER` | The administrator of the contract. |
| `TIMELOCK-DELAY` | 24-hour delay (144 blocks) for emergency withdrawals. |
| `reclaim-period-length` | Number of blocks before unclaimed tokens can be reclaimed. |
| `airdrop-amount-per-recipient` | Default token amount per recipient. |

## Errors
| Error Code | Description |
|------------|-------------|
| `u100` | Caller is not the contract owner. |
| `u101` | Recipient has already claimed the airdrop. |
| `u102` | Recipient is not eligible for the airdrop. |
| `u103` | Insufficient token balance for distribution. |
| `u104` | Airdrop is not active. |
| `u105` | Invalid token amount specified. |
| `u106` | Reclaim period has not ended. |
| `u107` | Invalid recipient address. |
| `u108` | Invalid reclaim period specified. |

## Contract Functions

### 1. **Admin Functions**
#### `add-eligible-recipient(recipient principal) -> (ok true)`
Adds a recipient to the eligibility list.

#### `remove-eligible-recipient(recipient principal) -> (ok true)`
Removes a recipient from the eligibility list.

#### `bulk-add-eligible-recipients(recipients list) -> (ok true)`
Adds multiple recipients at once.

#### `update-airdrop-amount(new-amount uint) -> (ok new-amount)`
Updates the default airdrop amount.

#### `update-reclaim-period(new-period uint) -> (ok new-period)`
Changes the number of blocks before unclaimed tokens are reclaimed.

### 2. **Claiming Functions**
#### `claim-airdrop-tokens() -> (ok claim-amount)`
Allows an eligible recipient to claim their airdrop tokens.

#### `claim-tiered-airdrop(tier-level uint) -> (ok claim-amount)`
Allows recipients to claim tokens based on their assigned tier.

### 3. **Emergency & Reclaim Functions**
#### `initiate-emergency-withdrawal() -> (ok timelock)`
Begins the emergency withdrawal process with a 24-hour timelock.

#### `execute-emergency-withdrawal(recipient principal) -> (ok balance)`
Executes emergency withdrawal of all contract funds to a specified address.

#### `reclaim-unclaimed-tokens() -> (ok unclaimed-amount)`
Burns any tokens not claimed after the reclaim period.

### 4. **Pause & Resume Functions**
#### `pause-airdrop() -> (ok true)`
Pauses the airdrop.

#### `resume-airdrop() -> (ok true)`
Resumes the airdrop after a pause.

### 5. **Read-Only Queries**
#### `get-airdrop-active-status() -> bool`
Returns whether the airdrop is currently active.

#### `get-tier-multiplier(tier-level uint) -> uint`
Fetches the multiplier associated with a specific tier.

#### `is-recipient-eligible(recipient principal) -> bool`
Checks if a recipient is eligible.

#### `has-recipient-claimed-airdrop(recipient principal) -> bool`
Returns whether a recipient has already claimed their airdrop.

#### `get-total-tokens-distributed() -> uint`
Returns the total number of tokens distributed so far.

#### `get-reclaim-period() -> uint`
Returns the current reclaim period setting.

#### `get-event(event-id uint) -> (optional event-data)`
Fetches event logs by event ID.

## Deployment & Initialization
The contract mints an initial supply of tokens and assigns them to the contract owner. Ensure the contract has enough tokens before enabling the airdrop.

## Future Enhancements
- Multi-chain support for cross-network airdrops.
- Staking-based eligibility verification.
- Custom NFT rewards for airdrop participants.
