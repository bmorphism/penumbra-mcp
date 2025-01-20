# Penumbra MCP Server Feature Proposals

## Current Functionality
The server provides the following tools:

### Chain Interaction Tools
- `get_validator_set`: Get validator information
- `get_chain_status`: Get chain status
- `get_transaction`: Get transaction details
- `get_dex_state`: Get DEX state
- `get_governance_proposals`: Get governance proposals

### Transaction Building Tools (✓ Implemented)
- `build_transaction`: Create and sign transactions with various actions
- `estimate_fees`: Estimate transaction fees based on action types
- `simulate_transaction`: Simulate transaction execution for validation

## Proposed New Features

### 1. Privacy-Focused Tools

#### `generate_viewing_key`
- Description: Generate new viewing keys for transaction scanning
- Input Schema:
```typescript
{
  seed?: string;  // Optional seed for deterministic generation
}
```

#### `create_shielded_transfer`
- Description: Create private transfer transactions
- Input Schema:
```typescript
{
  amount: string;
  assetId: string;
  recipient: string;
  memo?: string;
}
```

#### `scan_notes`
- Description: Scan for notes visible to a viewing key
- Input Schema:
```typescript
{
  viewingKey: string;
  startHeight?: number;
  endHeight?: number;
}
```

### 2. DEX Enhancement Tools

#### `calculate_swap_output`
- Description: Calculate expected output for a swap
- Input Schema:
```typescript
{
  inputAsset: string;
  outputAsset: string;
  amount: string;
  slippageTolerance?: number;
}
```

#### `get_liquidity_position`
- Description: Get details of a liquidity position
- Input Schema:
```typescript
{
  positionId: string;
}
```

#### `estimate_price_impact`
- Description: Estimate price impact for a trade
- Input Schema:
```typescript
{
  inputAsset: string;
  outputAsset: string;
  amount: string;
}
```

#### `get_historical_prices`
- Description: Get historical price data
- Input Schema:
```typescript
{
  pair: string;
  timeframe: '1h' | '4h' | '1d' | '1w';
  limit?: number;
}
```

### 3. Staking Tools

#### `calculate_rewards`
- Description: Calculate expected staking rewards
- Input Schema:
```typescript
{
  amount: string;
  validatorAddress: string;
  duration?: number;  // In epochs
}
```

#### `get_delegation_info`
- Description: Get detailed delegation information
- Input Schema:
```typescript
{
  delegatorAddress?: string;
  validatorAddress?: string;
}
```

#### `estimate_unbonding_time`
- Description: Estimate time until unbonding completes
- Input Schema:
```typescript
{
  amount: string;
  validatorAddress: string;
}
```

### 4. Analytics Tools

#### `get_network_metrics`
- Description: Get network statistics and health
- Input Schema:
```typescript
{
  metrics: Array<
    | 'tps'
    | 'activeValidators'
    | 'totalStake'
    | 'inflation'
    | 'blockTime'
  >;
}
```

#### `analyze_transaction_privacy`
- Description: Analyze transaction privacy score
- Input Schema:
```typescript
{
  transactionHash: string;
}
```

#### `get_dex_analytics`
- Description: Get DEX volume, TVL, and other metrics
- Input Schema:
```typescript
{
  metrics: Array<
    | 'volume24h'
    | 'tvl'
    | 'fees24h'
    | 'trades24h'
    | 'uniqueTraders24h'
  >;
  pair?: string;
}
```

## Implementation Strategy

1. Core Integration
- Integrate with Penumbra client libraries
- Implement proper error handling
- Add comprehensive logging
- Add metrics collection

2. Privacy Considerations
- Ensure all operations maintain Penumbra's privacy guarantees
- Implement proper key management
- Add privacy score analysis

3. Performance Optimization
- Implement caching for frequently accessed data
- Add batch processing capabilities
- Optimize proof generation

4. Testing
- Add unit tests for all new tools
- Add integration tests with testnet
- Add performance benchmarks

5. Documentation
- Add detailed API documentation
- Add usage examples
- Add privacy considerations guide

## Next Steps

1. Prioritize remaining features based on:
   - User demand
   - Implementation complexity
   - Privacy implications
   - Performance impact

2. Create detailed technical specifications for each tool

3. Implement proof-of-concept for highest priority features

4. Gather community feedback

5. Begin phased implementation
