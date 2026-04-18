# Reuse Bharat

> India's sustainable campus marketplace — connecting students to buy, sell, and share resources within their college community.

[![License: MIT](https://img.shields.io/badge/License-MIT-orange.svg)](LICENSE)
[![Platform: Celo](https://img.shields.io/badge/Platform-Celo-brightgreen.svg)](https://celo.org)
[![Stack: MERN](https://img.shields.io/badge/Stack-MERN%2BWeb3-purple.svg)](https://celo.org)

A full-stack Web3 platform enabling college students to trade textbooks, lab manuals, stationery, food, and medicines — reducing waste and saving costs across campuses in India.

## Why Reuse Bharat?

```
┌────────────────────────────────────────────────────────────────────────┐
│                           THE PROBLEM                                   │
├────────────────────────────────────────────────────────────────────────┤
│  💔 40%      of cooked college mess food is thrown daily              │
│  💔 ₹18,000 Cr of sealed medicine expires unused in Indian homes    │
│  💔 1 Student buys. 1 year later, it's landfill.                   │
│       Textbooks, lab coats, calculators — forgotten in corners.      │
└────────────────────────────────────────────────────────────────────────┘
```

### Our Solutions

| App | Description | Category |
|-----|-------------|----------|
| **Campus Samagri** | Buy/sell textbooks, lab manuals, notes | Academic |
| **Annapurna** | Surplus mess food connecting to those in need | Food Rescue |
| **AushadhMitra** | Share unopened medicines before expiry | Healthcare |

## Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                            REUSE BHARAT                               │
├─────────────────────────────────────────────────────────────────────┤
│  ┌─────────────┐   ┌─────────────┐   ┌─────────────────────────────┐  │
│  │   Frontend  │◄──│   Backend   │◄──│    Celo Blockchain         │  │
│  │  (React)    │   │ (Express)  │   │ (CampusMarketplace.sol)      │  │
│  │             │   │  MongoDB   │   │  Data Storage Only         │  │
│  └─────────────┘   └─────────────┘   └─────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────┘
```

### Tech Stack

| Layer | Technology |
|-------|------------|
| **Frontend** | React 18, Vite, React Router, Framer Motion |
| **Backend** | Express.js, MongoDB (Mongoose), Multer, Cloudinary |
| **Database** | MongoDB |
| **Blockchain** | Solidity, Hardhat, Celo Sepolia |
| **Storage** | Cloudinary (images) |

## Project Structure

```
reuse-bharat/
├── frontend/                 # React + Vite application
│   ├── src/
│   │   ├── components/      # Reusable UI components
│   │   │   ├── hero/
│   │   │   ├── layout/
│   │   │   └── sections/
│   │   ├── pages/           # Page components
│   │   │   ├── Landing.jsx         # Landing page
│   │   │   ├── CampusSamagri.jsx   # Marketplace
│   │   │   ├── Annapurna.jsx       # Food rescue
│   │   │   ├── AushadhMitra.jsx    # Medicine sharing
│   │   │   ├── Dashboard.jsx
│   │   │   └── Auth.jsx
│   │   ├── lib/            # Utilities
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── index.html
│   ├── vite.config.js
│   └── package.json
│
├── backend/                 # Express API
│   ├── src/
│   │   ├── config/         # Database & cloud config
│   │   ├── controllers/   # Route logic
│   │   ├── models/        # Mongoose schemas
│   │   ├── routes/        # API routes
│   │   ├── middleware/    # Upload middleware
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
├── hardhat.config.js       # Hardhat configuration
├── package.json           # Root package.json
└── README.md
```

## Getting Started

### Prerequisites

- Node.js 18+
- MongoDB (local or Atlas)
- npm or yarn
- Celo Wallet (for blockchain features)

### Installation

```bash
# Clone and navigate
cd reuse-bharat

# Install all dependencies
npm install
cd frontend && npm install && cd ..
cd backend && npm install && cd ..
```

### Environment Variables

Create `.env` files:

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

### Running the Application

```bash
# Terminal 1: Start Backend
cd backend
npm run dev

# Terminal 2: Start Frontend
cd frontend
npm run dev
```

- Frontend: http://localhost:5173
- Backend: http://localhost:5000

### Blockchain Deployment

```bash
# Compile contracts
npm run compile

# Deploy to Celo Sepolia
npx hardhat run scripts/deploy.js --network celoSepolia
```

## Smart Contract

### CampusMarketplace

A data-only storage contract on Celo blockchain — no payment logic on-chain.

- **Network**: Celo Sepolia
- **Address**: `0x0f4A570a593F27Fa78Bf09F4F0301Ae41c4ee075`

#### Functions

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
```

#### Enums

```solidity
enum Category { Textbooks, LabManuals, Notebooks, Stationery, Calculators, Other }
enum Condition { New, LikeNew, Good, Fair }
```

## API Endpoints

| Method | Endpoint | Description |
|--------|-----------|-------------|
| `POST` | `/api/users/register` | Register user |
| `POST` | `/api/users/login` | User login |
| `GET` | `/api/listings` | Get all listings |
| `POST` | `/api/listings` | Create listing |
| `PUT` | `/api/listings/:id` | Update listing |
| `DELETE` | `/api/listings/:id` | Delete listing |
| `POST` | `/api/upload/image` | Upload image |

## Features

### Campus Samagri
- List textbooks, lab manuals, stationery
- Browse by category and condition
- Filter by price range
- Mark items as sold

### Annapurna
- Connect surplus mess food to those in need
- Real-time availability tracking

### AushadhMitra
- Share unopened medicines before expiry
- Medicine type and quantity tracking

## License

MIT License — see [LICENSE](LICENSE) for details.

## Disclaimer

This project is for educational/demonstration purposes. When deploying to production:
- Add proper authentication and authorization
- Implement rate limiting
- Add input validation and sanitization
- Use environment-appropriate private key management
- Add comprehensive tests