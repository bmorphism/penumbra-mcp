# Penumbra MCP Server

An MCP server providing tools for interacting with the Penumbra blockchain. This server enables privacy-preserving interactions with Penumbra's core features including transaction queries, validator set information, DEX state, and governance proposals.

<a href="https://glama.ai/mcp/servers/21fa1hhrxw"><img width="380" height="200" src="https://glama.ai/mcp/servers/21fa1hhrxw/badge" alt="Penumbra Server MCP server" /></a>

## Features

### Current Tools

- `get_validator_set`: Get the current validator set information
- `get_chain_status`: Get current chain status including block height and chain ID
- `get_transaction`: Get details of a specific transaction
- `get_dex_state`: Get current DEX state including latest batch auction results
- `get_governance_proposals`: Get active governance proposals

### Planned Features

- Transaction submission
- Private staking operations
- DEX trading (sealed-bid batch auctions)
- Private governance voting
- Liquidity position management

## Installation

You can install the package via npm:

```bash
npm install @timeheater/penumbra-mcp
```

Or using yarn:

```bash
yarn add @timeheater/penumbra-mcp
```

## Setup

### Local Development from Source

1. Install dependencies:
```bash
npm install
```

2. Build the server:
```bash
npm run build
```

3. Run in development mode:
```bash
npm run watch
```

### Claude Desktop Integration

To integrate with Claude desktop, add the following configuration to your Claude desktop settings file (`~/Library/Application Support/Claude/claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "penumbra-mcp": {
      "command": "node",
      "args": ["/Users/barton/infinity-topos/penumbra-mcp/build/index.js"],
      "env": {
        "PENUMBRA_NODE_URL": "https://rpc.penumbra.zone",
        "PENUMBRA_NETWORK": "mainnet",
        "PENUMBRA_CHAIN_ID": "penumbra-1",
        "PENUMBRA_REQUEST_TIMEOUT": "30000",
        "PENUMBRA_REQUEST_RETRIES": "5",
        "PENUMBRA_BLOCK_TIME": "6000",
        "PENUMBRA_EPOCH_DURATION": "100",
        "PENUMBRA_DEX_BATCH_INTERVAL": "60000",
        "PENUMBRA_DEX_MIN_LIQUIDITY": "1000",
        "PENUMBRA_DEX_MAX_PRICE_IMPACT": "0.05",
        "PENUMBRA_GOVERNANCE_VOTING_PERIOD": "1209600000",
        "PENUMBRA_GOVERNANCE_MIN_DEPOSIT": "100000"
      }
    }
  }
}
```

Replace `/path/to/penumbra-mcp` with the actual path where you've installed the server.

### Using the MCP Server

Once configured, you can interact with Penumbra through Claude using the following tools:

1. Query validator set:
```
Tell Claude: "Show me the current Penumbra validator set"
```

2. Check chain status:
```
Tell Claude: "What's the current status of the Penumbra chain?"
```

3. Get transaction details:
```
Tell Claude: "Look up Penumbra transaction [HASH]"
```

4. View DEX state:
```
Tell Claude: "Show me the current Penumbra DEX state"
```

5. List governance proposals:
```
Tell Claude: "List active Penumbra governance proposals"
```

## Development

- `npm run watch`: Watch mode for development
- `npm run inspector`: Run MCP inspector for testing
- `npm test`: Run test suite

## Environment Variables

### Node Configuration
- `PENUMBRA_NODE_URL`: URL of the Penumbra node (default: https://rpc.penumbra.zone)
- `PENUMBRA_REQUEST_TIMEOUT`: HTTP request timeout in milliseconds (default: 30000)
- `PENUMBRA_REQUEST_RETRIES`: Number of request retries (default: 5)

### Chain Configuration
- `PENUMBRA_NETWORK`: Network to connect to (default: mainnet)
- `PENUMBRA_CHAIN_ID`: Chain ID (default: penumbra-1)
- `PENUMBRA_BLOCK_TIME`: Block time in milliseconds (default: 6000)
- `PENUMBRA_EPOCH_DURATION`: Number of blocks per epoch (default: 100)

### DEX Configuration
- `PENUMBRA_DEX_BATCH_INTERVAL`: Batch auction interval in milliseconds (default: 60000)
- `PENUMBRA_DEX_MIN_LIQUIDITY`: Minimum liquidity amount (default: 1000)
- `PENUMBRA_DEX_MAX_PRICE_IMPACT`: Maximum price impact as decimal (default: 0.05)

### Governance Configuration
- `PENUMBRA_GOVERNANCE_VOTING_PERIOD`: Voting period duration in milliseconds (default: 1209600000 - 14 days)
- `PENUMBRA_GOVERNANCE_MIN_DEPOSIT`: Minimum proposal deposit amount (default: 100000)

## Architecture

The server is built using TypeScript and implements the Model Context Protocol (MCP) for standardized tool interfaces. It currently provides mock implementations for core functionality, with plans to integrate directly with Penumbra's client libraries and node API endpoints.

### Privacy Considerations

All interactions respect Penumbra's privacy-preserving design:
- Shielded transactions
- Private staking operations
- Sealed-bid batch auctions
- Anonymous governance voting

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

ISC
