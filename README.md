# BlowUpBot 🚀

A comprehensive Solana trading and token launch platform powered by Telegram. Trade with automated DCA strategies, launch tokens with bonding curves, and manage your portfolio - all from Telegram. **Currently running on Solana Devnet** for safe testing and development.

![BlowUpBot](https://img.shields.io/badge/Solana-Devnet-blueviolet)
![Raydium](https://img.shields.io/badge/Raydium-SDK_v2-blue)
![TypeScript](https://img.shields.io/badge/TypeScript-Monorepo-informational)
![License](https://img.shields.io/badge/license-MIT-green)

## 🌟 Features

### 💼 Wallet Management
- **Automatic Wallet Creation**: Each user gets a secure Solana wallet on first interaction
- **Encrypted Storage**: Private keys encrypted with AES-256-GCM
- **Balance Tracking**: View SOL and all SPL token balances
- **Token Transfers**: Send any SPL token to any Solana address
- **Devnet Airdrop**: Request test SOL for devnet testing

### 📊 DCA Trading (Dollar Cost Averaging)
- **Automated Trading**: Set up recurring buys at fixed intervals
- **Flexible Intervals**: Hourly, Daily, Weekly, or Monthly execution
- **Multiple Strategies**: Run multiple DCA strategies simultaneously
- **Real-time Analytics**: Track performance, average buy price, and ROI
- **Strategy Management**: Pause, resume, or cancel strategies anytime
- **Execution History**: View complete transaction history with explorer links

### 🪙 Token Launchpad
- **Token Creation**: Launch custom SPL tokens on Solana Devnet
- **Raydium Pool Creation**: Automatic liquidity pool creation using Raydium SDK
- **Bonding Curve Integration**: Fair launch mechanism with automatic liquidity
- **Metadata Support**: Add token name, symbol, description, and logo
- **Instant Deployment**: Deploy tokens in seconds via Telegram
- **Pump.fun Alternative**: Similar to pump.fun but through Telegram on devnet

### 💱 Token Swaps
- **Quick Swaps**: Swap any SPL token for another
- **Raydium DEX Integration**: Powered by Raydium SDK v2 for reliable devnet trading
- **Liquidity Pool Management**: Direct interaction with Raydium liquidity pools
- **Slippage Control**: Customizable slippage tolerance
- **Price Impact Warnings**: Real-time price impact calculations

### 📈 Portfolio Tracking
- **Portfolio Overview**: View all token holdings and current values
- **Price Tracking**: Real-time price updates for any token
- **Performance Analytics**: Track gains/losses across all positions
- **Transaction History**: Complete audit trail of all trades

### 🎯 Quick Actions
- **Popular Token Lists**: Quick access to trending tokens
- **Recent Activity**: View your latest transactions
- **Favorites**: Save frequently traded tokens
- **Custom Watchlists**: Track specific tokens

## 🏗️ Architecture

BlowUpBot is built as a **Turborepo monorepo** with multiple services working together:

```
┌─────────────────────────────────────────────────────────────┐
│                         Frontend (Next.js)                   │
│                    Marketing & Documentation                 │
└─────────────────────────────────────────────────────────────┘
                                │
┌─────────────────────────────────────────────────────────────┐
│                    Telegram Bot Service                      │
│              • User interactions & commands                  │
│              • Session management                            │
│              • Real-time responses                           │
└──────────────────────┬──────────────────────────────────────┘
                       │
        ┌──────────────┼──────────────┐
        │              │              │
┌───────▼──────┐ ┌────▼─────┐ ┌─────▼──────┐
│  Scheduler   │ │ Database │ │  Relayer   │
│   Service    │ │(Postgres)│ │  Service   │
│              │ │          │ │            │
│ • DCA Exec   │ │ • Prisma │ │ • On-chain │
│ • Cron Jobs  │ │ • Users  │ │   Pools    │
│ • Background │ │ • DCA    │ │ • Token    │
│   Tasks      │ │ • Tokens │ │   Creation │
└──────────────┘ └──────────┘ └────────────┘
        │              │              │
        └──────────────┼──────────────┘
                       │
        ┌──────────────▼──────────────┐
        │       Shared Packages        │
        │                              │
        │  • @repo/database (Prisma)  │
        │  • @repo/services (Solana)  │
        │  • @repo/config-typescript  │
        └──────────────────────────────┘
                       │
        ┌──────────────▼──────────────┐
        │   Solana Blockchain (Devnet) │
        │   • SPL Token Program        │
        │   • Raydium DEX & SDK v2     │
        │   • Liquidity Pools          │
        │   • Custom Programs          │
        └──────────────────────────────┘
```

### Service Breakdown

#### 🤖 **Bot Service** (`apps/bot`)
- Built with **Telegraf** (Telegram Bot Framework)
- Handles all user interactions and commands
- Manages wallet operations and transactions
- Executes swaps and trades via Raydium SDK v2
- Coordinates with other services for complex operations

#### ⏰ **Scheduler Service** (`apps/scheduler`)
- Executes DCA strategies at scheduled intervals via Raydium DEX
- Background job processing
- Automatic retry logic for failed trades
- Monitors strategy health and execution status

#### 🔗 **Off-chain Relayer** (`apps/off-chain-relayer`)
- Manages Raydium liquidity pool creation for token launches
- Handles bonding curve operations using Raydium SDK
- Creates and initializes token pools on devnet
- Transaction batching and optimization

#### 🌐 **Frontend** (`apps/fe`)
- **Next.js 16** with App Router
- **Tailwind CSS** for styling
- Marketing website and documentation
- Real-time bot integration demos

#### 📦 **Shared Packages**

**`packages/database`**
- Prisma ORM setup
- Database migrations and schemas
- Typed database operations
- User, DCA, Token, and Execution models

**`packages/services`**
- Solana Web3.js utilities
- Token operations (swap, transfer, create)
- Raydium SDK v2 integration for all DEX operations
- Liquidity pool interactions
- Encryption/decryption utilities
- Portfolio and price tracking

## 🛠️ Tech Stack

### Backend
- **TypeScript** - Type-safe development
- **Node.js 18+** - Runtime environment
- **Telegraf** - Telegram Bot framework
- **Prisma** - Type-safe database ORM
- **PostgreSQL** - Primary database

### Blockchain
- **Solana Web3.js** - Blockchain interactions
- **@solana/spl-token** - SPL Token operations
- **Raydium SDK v2** - DEX operations, swaps, and liquidity pool management
- **Devnet Environment** - Safe testing and development environment

### Frontend
- **Next.js 16** - React framework with App Router
- **TypeScript** - Type safety
- **Tailwind CSS 4** - Utility-first styling
- **Lucide React** - Icon library

### DevOps
- **Turborepo** - Monorepo build system
- **Docker** - Containerization
- **Docker Compose** - Multi-container orchestration
- **pnpm** - Fast package manager

## 📋 Prerequisites

Before setting up BlowUpBot, ensure you have:

- **Node.js** 18 or higher
- **pnpm** 10.10.0 or higher
- **Docker** and **Docker Compose** (for containerized deployment)
- **PostgreSQL** 15+ (or use Docker)
- **Telegram Bot Token** (from [@BotFather](https://t.me/botfather))
- **Solana RPC URL** (Devnet/Mainnet)

## 🚀 Setup Guide

### 1. Clone the Repository

```bash
git clone https://github.com/jassBawa/BlowUpBot.git
cd BlowUpBot
```

### 2. Install Dependencies

```bash
# Install pnpm if you haven't
npm install -g pnpm

# Install all dependencies
pnpm install
```

### 3. Environment Configuration

Create `.env` files in the following locations:

#### **Root `.env`** (for Docker Compose)
```env
# Telegram Bot
BOT_TOKEN=your_telegram_bot_token

# Solana Configuration
SOLANA_RPC_URL=https://api.devnet.solana.com
SOLANA_CLUSTER=devnet
PROGRAM_ID=your_custom_program_id

# Security
ENCRYPTION_KEY=your_32_byte_encryption_key

# Relayer (for token launches)
RELAYER_PRIVATE_KEY=your_relayer_wallet_private_key
RPC_URL=https://api.devnet.solana.com
```

#### **`packages/database/.env`**
```env
DATABASE_URL="postgresql://postgres:postgres@localhost:5432/telegram_bot"
```

#### **`apps/bot/.env`**
```env
BOT_TOKEN=your_telegram_bot_token
DATABASE_URL="postgresql://postgres:postgres@localhost:5432/telegram_bot"
ENCRYPTION_KEY=your_32_byte_encryption_key
SOLANA_RPC_URL=https://api.devnet.solana.com
SOLANA_CLUSTER=devnet
PROGRAM_ID=your_custom_program_id
```

#### **`apps/scheduler/.env`**
```env
DATABASE_URL="postgresql://postgres:postgres@localhost:5432/telegram_bot"
SOLANA_RPC_URL=https://api.devnet.solana.com
SOLANA_CLUSTER=devnet
PROGRAM_ID=your_custom_program_id
ENCRYPTION_KEY=your_32_byte_encryption_key
```

### 4. Database Setup

```bash
# Generate Prisma Client
pnpm run generate

# Run database migrations
pnpm run db:migrate:dev

# Seed the database with initial data (optional)
pnpm run db:seed
```

### 5. Build the Project

```bash
# Build all packages and apps
pnpm run build
```

### 6. Start Development

#### Option A: Local Development (All Services)
```bash
# Start all services in watch mode
pnpm run dev
```

This will start:
- Bot service on auto-reload
- Scheduler service
- Frontend on http://localhost:3000

#### Option B: Docker Compose (Production-like)
```bash
# Start all services with Docker
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

Docker Compose will start:
- PostgreSQL database
- Database migrations
- Bot service
- Scheduler service
- Off-chain relayer service

### 7. Verify Setup

1. Open Telegram and search for your bot
2. Send `/start` command
3. You should receive a welcome message with your wallet address
4. Test basic commands like `/balance` or `/about`

## 📦 Project Structure

```
BlowUpBot/
├── apps/
│   ├── bot/                  # Telegram bot service
│   │   ├── commands/         # Bot command handlers
│   │   │   ├── dca/         # DCA-related commands
│   │   │   ├── start.ts     # Start & main menu
│   │   │   ├── wallet.*.ts  # Wallet commands
│   │   │   ├── swap.ts      # Token swap commands
│   │   │   ├── token.ts     # Token creation
│   │   │   └── portfolio.ts # Portfolio tracking
│   │   ├── bot/             # Bot initialization
│   │   ├── utils/           # Utility functions
│   │   └── index.ts         # Entry point
│   │
│   ├── fe/                   # Next.js frontend
│   │   ├── src/
│   │   │   ├── app/         # App router pages
│   │   │   ├── components/  # React components
│   │   │   └── lib/         # Utilities
│   │   └── public/          # Static assets
│   │
│   ├── scheduler/            # DCA execution service
│   │   └── src/
│   │       ├── executor.ts  # DCA execution logic
│   │       └── index.ts     # Cron scheduler
│   │
│   └── off-chain-relayer/    # Token pool relayer
│       └── src/
│           └── handlers/    # Pool creation handlers
│
├── packages/
│   ├── database/            # Prisma ORM package
│   │   ├── prisma/
│   │   │   ├── schema.prisma # Database schema
│   │   │   └── migrations/   # Migration files
│   │   └── src/
│   │       ├── client.ts    # Prisma client
│   │       ├── user/        # User operations
│   │       ├── dca/         # DCA operations
│   │       └── tokenPair/   # Token pair operations
│   │
│   └── services/            # Shared Solana services
│       └── src/
│           ├── solana.ts    # Wallet & transaction utils
│           ├── token.ts     # Token operations
│           ├── swap.ts      # Swap logic
│           ├── price.ts     # Price fetching
│           ├── portfolio.ts # Portfolio tracking
│           └── encryption.ts # Key encryption
│
├── docker-compose.yml       # Multi-service orchestration
├── turbo.json              # Turborepo configuration
├── pnpm-workspace.yaml     # pnpm workspace config
└── package.json            # Root package.json
```

## 🔧 Available Scripts

### Root Level
```bash
pnpm run dev              # Start all services in development
pnpm run build            # Build all apps and packages
pnpm run lint             # Lint all packages
pnpm run format           # Format code with Prettier
pnpm run generate         # Generate Prisma client
pnpm run db:migrate:dev   # Run database migrations
pnpm run db:seed          # Seed database
```

### Individual Apps
```bash
# Bot service
cd apps/bot
pnpm run dev              # Start bot in watch mode
pnpm run build            # Build bot
pnpm run start            # Start production bot

# Frontend
cd apps/fe
pnpm run dev              # Start Next.js dev server
pnpm run build            # Build for production
pnpm run start            # Start production server

# Scheduler
cd apps/scheduler
pnpm run dev              # Start scheduler in watch mode
pnpm run build            # Build scheduler
pnpm run start            # Start production scheduler
```

## 🐳 Docker Commands

```bash
# Start all services
docker-compose up -d

# View logs
docker-compose logs -f [service_name]

# Restart a service
docker-compose restart [service_name]

# Stop all services
docker-compose down

# Rebuild and start
docker-compose up -d --build

# Remove volumes (careful!)
docker-compose down -v
```

## 🎮 Bot Commands Reference

### Wallet Commands
- `/start` - Initialize bot and create wallet
- `/balance` - Check wallet balance
- `/wallet_send <token> <address> <amount>` - Send tokens
- `/portfolio` - View complete portfolio

### DCA Commands
- `/dca` - Set up new DCA strategy
- `/dca_list` or `/dcas` - List all strategies
- `/dca_stats` - View DCA performance statistics
- `/dca_history` - View execution history

### Trading Commands
- `/swap` - Swap tokens via Raydium DEX
- `/quick` - Quick access to popular devnet tokens
- `/price <token>` - Check token price

### Token Commands
- `/token` - Access token launchpad
- Create custom SPL tokens with metadata

### General
- `/about` - Bot information
- `/help` - Show help message

## 🔐 Security Features

- **Encrypted Private Keys**: All user private keys encrypted with AES-256-GCM
- **Secure Key Derivation**: Using PBKDF2 with salt
- **Non-custodial**: Users have full control of their wallets
- **Environment Variables**: Sensitive data in environment variables
- **Input Validation**: All user inputs validated and sanitized
- **Rate Limiting**: Built-in protection against spam/abuse

## 🌐 Network Support

- **Devnet**: Currently operating on Solana Devnet for safe testing and development
- **Risk-Free Testing**: Use devnet SOL (no real money) to test all features
- **Future Mainnet Support**: Architecture is designed to support mainnet deployment

**Note**: All trading, DCA strategies, and token launches currently happen on Solana Devnet. Request devnet SOL via the `/airdrop` command or from [Solana Faucet](https://faucet.solana.com).

## 📊 Database Schema

Key models:
- **TelegramUser**: User profiles with encrypted wallet keys
- **DcaStrategy**: Automated trading strategies
- **DcaExecution**: Trade execution history
- **TokenPair**: Supported trading pairs with metadata

See `packages/database/prisma/schema.prisma` for complete schema.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🔗 Links

- **GitHub**: [https://github.com/jassBawa/BlowUpBot](https://github.com/jassBawa/BlowUpBot)
- **Telegram Bot**: [@BlowUpBot](https://t.me/BlowUpBot)
- **Website**: Coming soon

## 👥 Team

Built with ❤️ by:
- [@jassBawa](https://github.com/jassBawa) - Jaspreet Bawa
- [@Vivekk-11](https://github.com/Vivekk-11) - Vivek

## 💬 Support

For support, questions, or feedback:
- Open an issue on GitHub
- Contact via Telegram: [@BlowUpBot](https://t.me/BlowUpBot)

## 🎯 Roadmap

- [ ] Mainnet deployment
- [ ] Multi-wallet support
- [ ] Advanced charting and analytics
- [ ] Mobile app (React Native)
- [ ] Additional DEX integrations (Jupiter, Orca)
- [ ] Portfolio rebalancing automation
- [ ] Social trading features
- [ ] Advanced order types (limit orders, stop-loss)
- [ ] NFT trading support

---

**⚠️ Disclaimer**: This bot currently operates on Solana Devnet and is for educational and testing purposes only. No real funds are involved. When deployed on mainnet, cryptocurrency trading carries significant risk. Always do your own research and never invest more than you can afford to lose.
