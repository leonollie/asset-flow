# AssetFlow Dynamic Wealth Orchestrator

[![License: ISC](https://img.shields.io/badge/License-ISC-blue.svg)](https://opensource.org/licenses/ISC)
[![Clarity Version](https://img.shields.io/badge/Clarity-v3-green.svg)](https://docs.stacks.co/clarity)
[![Stacks](https://img.shields.io/badge/Stacks-Compatible-orange.svg)](https://stacks.co)

> Next-generation decentralized asset allocation engine with intelligent rebalancing capabilities

AssetFlow revolutionizes portfolio management through autonomous asset allocation, real-time rebalancing mechanisms, and comprehensive risk management. This protocol empowers users to create sophisticated investment strategies with automated execution, multi-asset diversification, and granular control over allocation parameters. Built for institutional-grade performance with retail accessibility.

## 🌟 Features

### Core Functionality

- **Dynamic Portfolio Creation**: Create custom portfolios with up to 10 different assets
- **Intelligent Rebalancing**: Automated portfolio rebalancing based on target allocations
- **Real-time Asset Management**: Live tracking of portfolio performance and allocation drift
- **Granular Control**: Precise percentage-based asset allocation (basis points precision)
- **Multi-user Support**: Individual portfolio ownership and management per user

### Advanced Capabilities

- **Risk Management**: Built-in validation and safety checks for all operations
- **Protocol Fees**: Configurable fee structure (default: 25 basis points)
- **Time-based Rebalancing**: Intelligent timing mechanisms for optimal rebalancing
- **Comprehensive Analytics**: Portfolio value tracking and performance metrics

## 🏗️ Architecture

### Smart Contract Structure

```text
AssetFlow Contract
├── Error Constants (10 error codes)
├── Protocol Variables (Owner, counter, fees)
├── Data Structures
│   ├── Portfolios Map (Core metadata)
│   ├── PortfolioAssets Map (Asset allocations)
│   └── UserPortfolios Map (User ownership)
├── Read-Only Functions (Data access layer)
├── Private Functions (Internal logic)
└── Public Functions (External interface)
```

### Key Data Structures

#### Portfolio Structure

```clarity
{
  owner: principal,
  created-at: uint,
  last-rebalanced: uint,
  total-value: uint,
  active: bool,
  token-count: uint,
}
```

#### Asset Allocation Structure

```clarity
{
  target-percentage: uint,
  current-amount: uint,
  token-address: principal,
}
```

## 🚀 Getting Started

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) v2.0+
- [Node.js](https://nodejs.org/) v18+
- [Stacks CLI](https://docs.stacks.co/stacks-cli/installation) (optional)

### Installation

1. **Clone the repository**

   ```bash
   git clone <repository-url>
   cd asset-flow
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Run tests**

   ```bash
   npm test
   ```

4. **Format contracts**

   ```bash
   clarinet fmt --in-place
   ```

### Deployment

#### Development Network

```bash
clarinet integrate
```

#### Testnet Deployment

```bash
clarinet deployments generate --testnet
clarinet deployments apply --testnet
```

#### Mainnet Deployment

```bash
clarinet deployments generate --mainnet
clarinet deployments apply --mainnet
```

## 📖 Usage

### Creating a Portfolio

```clarity
;; Create a balanced portfolio with two assets
(contract-call? .asset-flow create-portfolio
  (list 'ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.token-a
        'ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM.token-b)
  (list u5000 u5000)) ;; 50% each
```

### Rebalancing a Portfolio

```clarity
;; Rebalance portfolio ID 1
(contract-call? .asset-flow rebalance-portfolio u1)
```

### Updating Asset Allocation

```clarity
;; Update token 0 allocation to 60%
(contract-call? .asset-flow update-portfolio-allocation u1 u0 u6000)
```

### Reading Portfolio Data

```clarity
;; Get portfolio information
(contract-call? .asset-flow get-portfolio u1)

;; Get user's portfolios
(contract-call? .asset-flow get-user-portfolios 'ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM)

;; Calculate rebalance requirements
(contract-call? .asset-flow calculate-rebalance-amounts u1)
```

## 🧪 Testing

The project includes comprehensive test coverage using Vitest and Clarinet SDK.

### Run Tests

```bash
# Run all tests
npm test

# Run tests with coverage
npm run test:report

# Watch mode for development
npm run test:watch
```

### Test Structure

- Unit tests for all public functions
- Integration tests for complex workflows
- Edge case validation
- Error handling verification

## 🔒 Security

### Validation Mechanisms

- **Authorization Checks**: All state-changing functions verify ownership
- **Input Validation**: Comprehensive parameter validation
- **Bounds Checking**: Safe arithmetic operations with overflow protection
- **State Consistency**: Atomic operations to maintain data integrity

### Error Handling

The contract implements 10 specific error codes:

- `ERR-NOT-AUTHORIZED` (u100): Unauthorized access attempt
- `ERR-INVALID-PORTFOLIO` (u101): Portfolio does not exist or inactive
- `ERR-INSUFFICIENT-BALANCE` (u102): Insufficient funds for operation
- `ERR-INVALID-TOKEN` (u103): Invalid or unsupported token
- `ERR-REBALANCE-FAILED` (u104): Rebalancing operation failed
- `ERR-PORTFOLIO-EXISTS` (u105): Portfolio already exists
- `ERR-INVALID-PERCENTAGE` (u106): Invalid percentage allocation
- `ERR-MAX-TOKENS-EXCEEDED` (u107): Too many tokens in portfolio
- `ERR-LENGTH-MISMATCH` (u108): Array length mismatch
- `ERR-INVALID-TOKEN-ID` (u110): Invalid token identifier

## ⚙️ Configuration

### Protocol Parameters

- **Maximum Tokens**: 10 per portfolio
- **Basis Points**: 10,000 (100% = 10,000 basis points)
- **Protocol Fee**: 25 basis points (0.25%)
- **Rebalance Cycle**: 144 blocks (~24 hours)
- **Max Portfolios per User**: 20

### Environment Settings

Configuration files are available for different networks:

- `settings/Devnet.toml`
- `settings/Testnet.toml`
- `settings/Mainnet.toml`

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines

- Follow Clarity best practices
- Maintain test coverage above 90%
- Include comprehensive documentation
- Use clear, descriptive commit messages

## 📋 Roadmap

### Phase 1: Core Features ✅

- [x] Portfolio creation and management
- [x] Basic rebalancing functionality
- [x] Multi-asset support
- [x] User ownership system

### Phase 2: Advanced Features 🚧

- [ ] Automated rebalancing triggers
- [ ] Performance analytics dashboard
- [ ] Fee distribution mechanisms
- [ ] Governance token integration

### Phase 3: Ecosystem Integration 📋

- [ ] DEX integration for automatic trading
- [ ] Oracle price feeds
- [ ] Cross-chain asset support
- [ ] Mobile application interface

## 📄 License

This project is licensed under the ISC License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

- **Documentation**: [Stacks Documentation](https://docs.stacks.co)
- **Discord**: [Stacks Discord](https://discord.gg/stacks)
- **Issues**: Please use the GitHub issue tracker for bug reports and feature requests

---
**AssetFlow: Where traditional finance meets decentralized innovation**
