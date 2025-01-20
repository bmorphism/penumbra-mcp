# Penumbra MCP Server

A Model Context Protocol server for interacting with the Penumbra blockchain. This server provides tools for chain interaction, transaction building, and more.

## Installation

1. Prerequisites:
   - Node.js >= 18.0.0
   - npm

2. Clone and install dependencies:
```bash
git clone <repository-url>
cd penumbra-mcp
npm install
```

3. Build the server:
```bash
npm run build
```

4. Configure environment variables (optional):
```bash
# Node connection
PENUMBRA_NODE_URL=http://localhost:8080  # Default
PENUMBRA_REQUEST_TIMEOUT=10000           # Default: 10s
PENUMBRA_REQUEST_RETRIES=3               # Default

# Chain configuration
PENUMBRA_NETWORK=testnet                 # Default
PENUMBRA_CHAIN_ID=penumbra-testnet      # Default
PENUMBRA_BLOCK_TIME=6000                 # Default: 6s
PENUMBRA_EPOCH_DURATION=100              # Default: blocks

# DEX configuration
PENUMBRA_DEX_BATCH_INTERVAL=60000        # Default: 60s
PENUMBRA_DEX_MIN_LIQUIDITY=1000          # Default
PENUMBRA_DEX_MAX_PRICE_IMPACT=0.05       # Default: 5%

# Governance configuration
PENUMBRA_GOVERNANCE_VOTING_PERIOD=604800000  # Default: 7 days
PENUMBRA_GOVERNANCE_MIN_DEPOSIT=10000        # Default
```

5. Run the server:
```bash
npm start
```

## Available Tools

### Chain Interaction Tools

#### get_validator_set
Get current validator set information.
```typescript
// Input: {}
// Output: { validators: Array<{
//   address: string;
//   votingPower: string;
//   commission: string;
//   status: string;
// }> }
```

#### get_chain_status
Get current chain status including block height and chain ID.
```typescript
// Input: {}
// Output: {
//   height: string;
//   chainId: string;
//   timestamp: string;
//   blockHash: string;
// }
```

#### get_transaction
Get details of a specific transaction.
```typescript
// Input: { hash: string }
// Output: {
//   hash: string;
//   status: string;
//   height: string;
//   timestamp: string;
//   gasUsed: string;
//   fee: string;
// }
```

#### get_dex_state
Get current DEX state including latest batch auction results.
```typescript
// Input: {}
// Output: {
//   currentBatchNumber: string;
//   lastBatchTimestamp: string;
//   batchInterval: number;
//   minLiquidityAmount: string;
//   maxPriceImpact: number;
//   activePairs: Array<{
//     baseAsset: string;
//     quoteAsset: string;
//     lastPrice: string;
//     volume24h: string;
//   }>;
// }
```

#### get_governance_proposals
Get active governance proposals.
```typescript
// Input: { status?: 'active' | 'completed' | 'all' }
// Output: {
//   proposals: Array<{
//     id: string;
//     title: string;
//     status: string;
//     votingEndTime: string;
//     minDeposit: string;
//     yesVotes: string;
//     noVotes: string;
//   }>;
// }
```

### Transaction Building Tools

#### build_transaction
Create and sign transactions with various actions.
```typescript
// Input: {
//   actions: Array<{
//     type: 'spend' | 'output' | 'swap' | 'delegate' | 'undelegate';
//     params: object;  // Action-specific parameters
//   }>;
//   memo?: string;
//   expiryHeight?: number;
// }
// Output: {
//   hash: string;
//   actions: Array<object>;
//   memo: string;
//   expiryHeight: number;
//   signature: string;
//   timestamp: string;
// }
```

#### estimate_fees
Estimate transaction fees based on action types.
```typescript
// Input: {
//   actions: Array<{
//     type: string;
//     params: object;
//   }>;
// }
// Output: {
//   estimatedFee: string;
//   breakdown: {
//     baseFee: string;
//     actionFees: Array<{
//       type: string;
//       fee: string;
//     }>;
//   };
// }
```

#### simulate_transaction
Simulate transaction execution for validation.
```typescript
// Input: {
//   transaction: string;  // Serialized transaction
// }
// Output: {
//   success: boolean;
//   gasUsed: string;
//   logs: Array<{
//     type: string;
//     timestamp: string;
//     details: string;
//   }>;
//   effects: {
//     stateChanges: Array<any>;
//     events: Array<any>;
//   };
// }
```

## Development

1. Build in watch mode:
```bash
npm run build -- --watch
```

2. Run tests:
```bash
npm test
```

## Future Features

See [FEATURE_PROPOSALS.md](./FEATURE_PROPOSALS.md) for upcoming features and implementation plans.
