---
id: intro
title: Mass Payout
sidebar_position: 0
slug: /
---

# Mass Payout

Manage large-scale payment distributions for tokenized securities with automated batch processing and scheduling capabilities.

## Overview

Mass Payout is a comprehensive payment distribution system designed for tokenized securities. It enables issuers to efficiently distribute dividends, coupon payments, and other recurring obligations to large numbers of token holders on the Hedera network.

### Key Features

* **Batch Payment Processing**: Efficiently distribute payments to thousands of token holders
* **Asset Import**: Automatically sync token holders and balances from ATS tokens
* **Multiple Distribution Types**: Support for dividends, coupon payments, and custom distributions
* **Scheduled Payouts**: Set up recurring distributions with cron-like scheduling
* **Real-time Tracking**: Monitor payout status and transaction history
* **Failure Recovery**: Automatic retry mechanism for failed payments
* **REST API**: Complete backend API for integration

## Architecture

Mass Payout consists of four main components working together:

```mermaid
graph TB
    subgraph "Frontend (React)"
        UI[Admin Panel]
        UI_Assets[Asset Management]
        UI_Dist[Distribution UI]
    end

    subgraph "Backend (NestJS)"
        API[REST API]
        UC[Use Cases]
        DS[Domain Services]
        Repos[Repositories]
        Cron[Scheduled Jobs]
        Listener[Event Listener]
    end

    subgraph "SDK Layer"
        SDK[Mass Payout SDK]
        Adapters[Transaction Adapters]
        Queries[Query Adapters]
    end

    subgraph "Smart Contracts"
        LCC[LifeCycle CashFlow]
        ATS_Contract[ATS Token Contract]
    end

    subgraph "Infrastructure"
        DB[(PostgreSQL)]
        Mirror[Mirror Node]
        HTS[Hedera Network]
    end

    UI --> API
    API --> UC
    UC --> DS
    DS --> Repos
    DS --> SDK
    Repos --> DB
    SDK --> Adapters
    SDK --> Queries
    Adapters --> LCC
    Queries --> Mirror
    LCC --> HTS
    Listener --> Mirror
    Listener --> DB
    Cron --> DS
    LCC -.Import.-> ATS_Contract

    style UI fill:#e1f5ff
    style API fill:#fff4e1
    style SDK fill:#ffe1f5
    style LCC fill:#e1ffe1
    style DB fill:#f3e5f5
```

Mass Payout consists of four main components:

### Smart Contracts

The **LifeCycle Cash Flow** contract manages all on-chain operations:

* **Distribution Execution**: Batch transfer payments to multiple recipients
* **Bond Cash-Out**: Handle bond maturity redemptions
* **Snapshot Management**: Capture holder balances at specific points in time
* **Role-Based Access**: Granular permissions for different operations
* **Upgradeable**: Proxy pattern for contract upgrades

[Learn more about contracts →](developer-guides/contracts/index.md)

### SDK

TypeScript SDK for blockchain interactions:

* **Command/Query Pattern**: Separation of write and read operations
* **Transaction Adapters**: Support for DFNS, RPC, and other signers
* **Value Objects**: Type-safe representation of blockchain entities
* **Mirror Node Integration**: Query historical data and events

[Learn more about SDK integration →](developer-guides/sdk-integration.md)

### Backend (NestJS)

Domain-driven backend API with PostgreSQL:

* **Domain Services**: Business logic for asset import, payout execution, and synchronization
* **Event-Driven Sync**: Automatic blockchain event polling and processing
* **Use Cases**: 22 use cases covering all operations
* **Repositories**: TypeORM for data persistence
* **Scheduled Jobs**: Cron-based automatic payout execution

[Learn more about backend →](developer-guides/backend/index.md)

### Frontend (React)

Admin panel for managing distributions:

* **Asset Management**: Import assets and view holder information
* **Distribution Creation**: Configure and execute payouts
* **Real-time Monitoring**: Track payout status and history
* **Chakra UI**: Modern, accessible component library
* **React Query**: Efficient data fetching and caching

![Mass Payout Web Interface](../../.gitbook/assets/mp-web.png)

[Try the web app →](getting-started/quick-start.md)

## Use Cases

#### 💵 Dividend Distributions

Distribute earnings to equity token holders

* Import equity tokens from ATS
* Calculate amounts per share
* Execute batch payments
* Track history and reporting

[Learn more](user-guides/creating-distributions/)

#### 📅 Coupon Payments

Automate periodic bond interest payments

* Import bond tokens from ATS
* Schedule periodic payments
* Auto-execute on schedule
* Handle proration

[Learn more](user-guides/scheduled-payouts/)

#### 🔄 Recurring Distributions

Set up automated recurring payouts

* Cron-based schedules
* Auto snapshot capturing
* Automatic retry on failure
* Email notifications

[Learn more](user-guides/scheduled-payouts/)

#### 📊 Large-Scale Payouts

Process payments to thousands of holders

* Efficient batch processing
* Pagination support
* Real-time progress tracking
* Detailed transaction logs

[Learn more](user-guides/managing-payouts/)

## Integration with ATS

Mass Payout is designed to work seamlessly with Asset Tokenization Studio:

```mermaid
graph LR
    A[Create Token<br/>in ATS] --> B[Import Asset<br/>to Mass Payout]
    B --> C[Sync Holders<br/>& Balances]
    C --> D[Create<br/>Distribution]
    D --> E[Execute<br/>Payout]
    E --> F[Monitor<br/>Status]
    F -.Recurring.-> D

    style A fill:#e1f5ff
    style B fill:#fff4e1
    style C fill:#ffe1f5
    style D fill:#e1ffe1
    style E fill:#f3e5f5
    style F fill:#e8f5e9
```

1. **Create tokens in ATS**: Issue equity or bond tokens
2. **Import to Mass Payout**: Sync token holder information
3. **Configure distributions**: Set up payment parameters
4. **Execute payouts**: Distribute payments to holders

You can use Mass Payout independently if you have existing tokens on Hedera.

## Getting Started

#### 👤 For End Users

Try the Mass Payout web application

* Quick start in minutes
* Import assets from ATS
* Create and manage distributions
* Monitor payout status

[Quick Start Guide](getting-started/quick-start/)

#### 👨‍💻 For Developers

Integrate Mass Payout or contribute

* Full development environment
* Backend + Frontend setup
* SDK integration
* Contract deployment

[Full Development Setup](getting-started/full-setup/)

## Documentation

#### 📚 User Guides

Step-by-step guides for the application

* Importing assets
* Creating distributions
* Managing payouts
* Scheduled distributions

[View Guides](user-guides/)

#### 🛠️ Developer Guides

Technical guides for developers

* Smart contract deployment
* SDK integration
* Backend API extension
* Frontend customization

[View Guides](developer-guides/)

#### 📖 API Documentation

Technical reference documentation

* Smart contract functions
* SDK methods
* REST API endpoints
* WebSocket events

[View API Docs](api/)

## Technical Stack

### Backend

* **NestJS**: TypeScript Node.js framework
* **PostgreSQL**: Relational database for persistence
* **TypeORM**: Object-relational mapping
* **Domain-Driven Design**: Clean architecture patterns

### Frontend

* **React 18**: Modern UI framework
* **Chakra UI**: Component library
* **React Query**: Data fetching and caching
* **Zustand**: State management

### Blockchain

* **Hedera Network**: DLT platform
* **Solidity**: Smart contract language
* **Hardhat**: Development environment

## System Requirements

* **Node.js**: v24.0.0 or newer
* **PostgreSQL**: 12 or newer
* **npm**: v10.9.0 or newer
* **Hedera Account**: With HBAR for transactions

## Support and Resources

* [GitHub Repository](https://github.com/hashgraph/asset-tokenization-studio)
* [Report Issues](https://github.com/hashgraph/asset-tokenization-studio/issues)
* [Hedera Documentation](https://docs.hedera.com)
* [Hedera Discord](https://hedera.com/discord)

## License

Licensed under Apache License 2.0. See [LICENSE](https://github.com/hashgraph/asset-tokenization-studio/blob/main/LICENSE) for details.
