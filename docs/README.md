# RupeeLink 🟡

### Secure P2P Crypto Trading — INR ↔ USDC, Powered by Blockchain

[![Next.js](https://img.shields.io/badge/Next.js-16-black?logo=next.js)](https://nextjs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-blue?logo=typescript)](https://typescriptlang.org)
[![Deployed on Vercel](https://img.shields.io/badge/Deployed-Vercel-black?logo=vercel)](https://rupeelink.vercel.app)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**Live Demo → [rupeelink.vercel.app](https://rupeelink.vercel.app)**

---

## What is RupeeLink?

RupeeLink is a peer-to-peer cryptocurrency trading platform that allows users in India to buy and sell USDC using Indian Rupees (INR). Payments are processed via Razorpay (UPI/bank transfer), and crypto settlement happens on-chain via a custom smart contract deployed on Monad Testnet.

No centralized exchange. No KYC delays. Just direct peer-to-peer trades.

---

## Features

- 🔐 **Auth** — Clerk-powered sign up / sign in with email & social login
- 📋 **Onboarding** — 4-step KYC flow: personal info, bank details, wallet linking
- 💱 **P2P Exchange** — Browse live buy/sell orders on the exchange board
- 💳 **Razorpay Payments** — INR payments via UPI, net banking, cards (test mode)
- ⛓️ **On-chain Settlement** — USDC transferred via Payment.sol smart contract on Monad
- 👛 **Wallet Dashboard** — View USDC balance, transaction history
- 🔔 **Notifications** — Real-time trade alerts
- 📊 **Payout Tracking** — View INR payouts to linked bank account

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Next.js 16, TypeScript, Tailwind CSS, shadcn/ui |
| Auth | Clerk |
| Database | Neon PostgreSQL (serverless) + Prisma ORM |
| Payments | Razorpay (Orders + Payouts API) |
| Blockchain | Ethers.js, Solidity, Monad Testnet |
| Smart Contract | Payment.sol (custom escrow) |
| Deployment | Vercel (frontend) |

---

## Smart Contract

**Payment.sol** is deployed on Monad Testnet:

```
Contract Address: 0x736d728451D0E6d649373c533269317EDb68710c
Network: Monad Testnet
USDC (Polygon Amoy): 0x41E94Eb019C0762f9Bfcf9Fb1E58725BfB0e7582
```

The contract handles USDC escrow and release upon payment confirmation.

---

## Project Structure

```
crypto-P2P/
├── app/
│   ├── api/                  # API routes
│   │   ├── razorpay/         # Payment order + verification
│   │   ├── p2p/orders/       # P2P trade order management
│   │   └── user/             # Onboarding, profile
│   ├── components/
│   │   ├── ui/               # shadcn UI components
│   │   └── Navbar.tsx
│   ├── hooks/                # Custom React hooks
│   ├── exchange/             # P2P order board
│   ├── wallet/               # Wallet dashboard
│   ├── payouts/              # Payout history
│   └── onboarding/           # KYC onboarding flow
├── lib/
│   └── utils.ts              # Shared utilities
├── prisma/
│   └── schema.prisma         # Database schema
├── contracts/
│   └── Payment.sol           # Escrow smart contract
└── scripts/
    └── deploy.mjs            # Contract deployment script
```

---

## Getting Started

### Prerequisites

- Node.js 20+
- npm
- A [Clerk](https://clerk.com) account
- A [Neon](https://neon.tech) PostgreSQL database
- A [Razorpay](https://razorpay.com) test account
- A crypto wallet with Polygon Amoy testnet USDC

### Installation

```bash
# Clone the repo
git clone https://github.com/hsay123/crypto-P2P.git
cd crypto-P2P

# Install dependencies
npm install --legacy-peer-deps
```

### Environment Variables

Create a `.env.local` file in the root:

```env
# Clerk Auth
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_...
CLERK_SECRET_KEY=sk_test_...

# Database
DATABASE_URL=postgresql://...

# Razorpay
RAZORPAY_KEY_ID=rzp_test_...
RAZORPAY_KEY_SECRET=...
NEXT_PUBLIC_RAZORPAY_KEY_ID=rzp_test_...

# Blockchain
INFURA_API_KEY=...
PRIVATE_KEY=0x...
PAYMENT_ADDRESS=0x736d728451D0E6d649373c533269317EDb68710c
```

### Database Setup

```bash
npx prisma generate
npx prisma migrate deploy
```

### Run Locally

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

---

## P2P Trade Flow

```
Buyer places order → Razorpay payment (INR) → Payment verified
→ Smart contract releases USDC → Buyer wallet receives USDC
→ Seller receives INR payout to bank account
```

---

## Deployment

The project is deployed on Vercel with GitHub CI/CD. Every push to `main` triggers an automatic production deployment.

**Environment variables** must be set in Vercel Dashboard → Settings → Environment Variables.

---

## Known Limitations

- Razorpay payouts to seller bank accounts require **Live mode** (KYC approved)
- Smart contract is on **Monad Testnet** — not mainnet
- Neon free tier may have occasional cold start delays (~1-2s)

---

## Roadmap

- [ ] Mainnet deployment (Monad / Polygon)
- [ ] Razorpay Live mode + seller payouts
- [ ] Order matching engine
- [ ] Mobile app (React Native)
- [ ] Multi-currency support (USDT, ETH)

---

## License

MIT © 2025 Yash Landge

---

<p align="center">Built with ☕ and way too many Vercel deploys.</p>
