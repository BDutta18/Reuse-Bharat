# Reuse Bharat

> A unified platform to address resource wastage in India through real-time coordination and transparent systems.

[![License: MIT](https://img.shields.io/badge/License-MIT-orange.svg)](LICENSE)
[![Platform: Celo](https://img.shields.io/badge/Platform-Celo-brightgreen.svg)](https://celo.org)
[![Stack: MERN+Web3](https://img.shields.io/badge/Stack-MERN%2BWeb3-purple.svg)](https://celo.org)

## The Vision

India faces a critical resource wastage crisis:
- **78–80 million tonnes** of food wasted annually
- **484 tonnes** of biomedical waste generated daily
- **194 million** people remain undernourished
- **40+ million** college students with unused educational materials

**Reuse Bharat** connects surplus food, study materials, and near-expiry medicines to those in need through:
- Real-time coordination
- Verified networks
- Transparent system powered by Web2 + Web3 technologies
- Wallet-based identity
- On-chain data storage using Celo blockchain

## Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                            REUSE BHARAT                               │
├─────────────────────────────────────────────────────────────────────┤
│  ┌─────────────┐   ┌─────────────┐   ┌─────────────────────────────┐  │
│  │   Frontend  │◄──│   Backend   │◄──│    Celo Blockchain         │  │
│  │  (React)    │   │ (Express)  │   │ (On-chain Data Storage)     │  │
│  │             │   │  MongoDB   │   │                             │  │
│  └─────────────┘   └─────────────┘   └─────────────────────────────┘  │
│                                                                     │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │              Features Module                                 │   │
│  │  ┌─────────────┐ ┌─────────────┐ ┌───────────────────────┐ │   │
│  │  │CampusSamagri│ │ Annapurna   │ │   AushadhMitra        │ │   │
│  │  │ (Academic)  │ │ (Food)      │ │   (Healthcare)       │ │   │
│  │  └─────────────┘ └─────────────┘ └───────────────────────┘ │   │
│  └─────────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────┘
```

### Tech Stack

| Layer | Technology |
|-------|------------|
| **Frontend** | React 18, Vite, React Router, Framer Motion |
| **Backend** | Express.js, MongoDB (Mongoose), Multer, Cloudinary |
| **Blockchain** | Solidity, Hardhat, Celo Sepolia |
| **Storage** | Cloudinary (images), Celo (on-chain data) |

## Features

| Module | Description | Impact |
|--------|-------------|--------|
| **Campus Samagri** | Buy/sell textbooks, lab materials, stationery | Reduce educational waste |
| **Annapurna** | Connect surplus food to those in need | Combat food wastage |
| **AushadhMitra** | Share near-expiry medicines | Improve healthcare access |

### Campus Samagri
- List textbooks, lab manuals, stationery
- Browse by category and condition
- Filter by price range
- Wallet-based transactions

### Annapurna
- Real-time surplus food listing
- Verified donor/recipient network
- QR-based pickup verification

### AushadhMitra
- Medicine sharing before expiry
- Batch and expiry tracking
- Verified medicine sources

## Project Structure

```
reuse-bharat/
├── frontend/                 # React + Vite application
│   ├── src/
│   │   ├── components/      # UI components
│   │   │   ├── hero/
│   │   │   ├── layout/
│   │   │   └── sections/
│   │   ├── pages/           # Page components
│   │   │   ├── Landing.jsx
│   │   │   ├── CampusSamagri.jsx   # Academic marketplace
│   │   │   ├── Annapurna.jsx       # Food rescue
│   │   │   ├── AushadhMitra.jsx    # Medicine sharing
│   │   │   ├── Dashboard.jsx
│   │   │   └── Auth.jsx
│   │   ├── lib/
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── index.html
│   ├── vite.config.js
│   └── package.json
│
├── backend/                 # Express API
│   ├── src/
│   │   ├── config/
│   │   ├── controllers/
│   │   ├── models/
│   │   ├── routes/
│   │   ├── middleware/
│   │   └── utils/
│   ├── app.js
│   ├── index.js
│   └── package.json
│
├── contracts/              # Solidity smart contracts
│   ├── CampusMarketplace.sol
│   └── ...
│
├── scripts/                # Deployment scripts
│   └── deploy.js
│
├── hardhat.config.js
├── package.json
└── README.md
```

## Getting Started

### Prerequisites

- Node.js 18+
- MongoDB (local or Atlas)
- Celo Wallet (for blockchain features)

### Installation

```bash
# Clone
cd reuse-bharat

# Install dependencies
npm install
cd frontend && npm install && cd ..
cd backend && npm install && cd ..
```

### Environment Variables

**backend/.env**
```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/reusebharat
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
```

**Root .env**
```env
PRIVATE_KEY=your_celo_wallet_private_key
```

### Running

```bash
# Terminal 1: Backend
cd backend
npm run dev

# Terminal 2: Frontend
cd frontend
npm run dev
```

- Frontend: http://localhost:5173
- Backend: http://localhost:5000

### Blockchain Deployment

```bash
# Compile
npm run compile

# Deploy to Celo Sepolia
npx hardhat run scripts/deploy.js --network celoSepolia
```

## Smart Contract

### CampusMarketplace

Data storage on Celo blockchain.

- **Network**: Celo Sepolia
- **Address**: `0x0f4A570a593F27Fa78Bf09F4F0301Ae41c4ee075`

```solidity
// Write Functions
function listItem(title, description, price, category, condition, imageURI) -> itemId
function markAsSold(itemId)
function updateItem(itemId, title, description, price, category, condition, imageURI)
function deleteItem(itemId)

// Read Functions
function getActiveItems() -> Item[]
function getItemsByCategory(Category) -> Item[]
function getItemsByPriceRange(minPrice, maxPrice) -> Item[]
function getItemsByCondition(Condition) -> Item[]
function getSellerItems(seller) -> Item[]

enum Category { Textbooks, LabManuals, Notebooks, Stationery, Calculators, Other }
enum Condition { New, LikeNew, Good, Fair }
```

## Impact Goals

| Metric | Target |
|--------|--------|
| Food rescued | 1000+ kg/month |
| Medicines shared | 500+ units/month |
| Educational materials | 2000+ items |
| Active users | 10,000+ |

## License

MIT License — see [LICENSE](LICENSE).

## Disclaimer

This project is for educational/demo purposes. Production deployment requires:
- Proper authentication/authorization
- Rate limiting
- Input validation
- Secure key management
- Comprehensive tests