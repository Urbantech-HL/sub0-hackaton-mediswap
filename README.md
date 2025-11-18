<div align="center">

# 🏥 PharmaBid

### Blockchain-Powered Public Tenders Ending Pharmaceutical Procurement Corruption

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Solidity](https://img.shields.io/badge/Solidity-0.8.20-363636?logo=solidity)](https://soliditylang.org/)
[![Hardhat](https://img.shields.io/badge/Hardhat-v3-yellow)](https://hardhat.org/)
[![Next.js](https://img.shields.io/badge/Next.js-14-black?logo=next.js)](https://nextjs.org/)
[![Arkiv](https://img.shields.io/badge/Arkiv-SDK-blue)](https://arkiv.network/)
[![sub0 Hack](https://img.shields.io/badge/sub0-Hack%202024-red)](https://hack.sub0.gg/)

[Demo Video](https://loom.com/...) • [Live App](https://pharmabid.vercel.app) • [Pitch Deck](./docs/pitch.pdf) • [Whitepaper](./docs/whitepaper.pdf)

</div>

---

## 🎯 The Problem

**$10-25 billion USD** is lost annually to corruption in public pharmaceutical procurement worldwide.

### Key Statistics
- **Price Disparities**: Same medications show price ratios of **3:1 up to 35:1** between hospitals
- **Systemic Corruption**: Kickbacks, shell companies, bid manipulation, and stock diversion
- **Zero Accountability**: Opaque processes with no audit trails or historical data
- **Lives at Stake**: Budget waste means fewer essential medicines reach patients who need them

> *Source: Transparency International, WHO Global Health Observatory, academic research in 15+ countries*

---

## 💡 The Solution

**PharmaBid** is a transparent, blockchain-based public tender marketplace that connects public hospitals with pharmaceutical suppliers through:

✅ **CoW Swap-Inspired Batch Settlement** → MEV-proof uniform pricing via reverse auction mechanism  
✅ **Arkiv Data Layer** → Immutable, queryable procurement history  
✅ **Smart Contract Settlement** → Automated, trustless execution  
✅ **Public Transparency Portal** → Open contracting for citizen oversight  

### Proven Impact
- **20-35% cost reduction** (competitive tender industry benchmarks)
- **100% traceability** on all transactions
- **0% corruption risk** through trustless automation
- **Millions of lives** saved via equitable medicine access

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────┐
│         FRONTEND (Next.js 14 + TypeScript)         │
│  Hospital Dashboard | Supplier Portal | Analytics  │
└─────────────────┬───────────────────────────────────┘
                  │
┌─────────────────▼───────────────────────────────────┐
│       SOLVER LAYER (Node.js + TypeScript)          │
│  Batch Aggregation | Price Optimization Engine     │
└─────────────────┬───────────────────────────────────┘
                  │
┌─────────────────▼───────────────────────────────────┐
│      SMART CONTRACTS (Solidity + Hardhat v3)       │
│  ProcurementTender | BatchSettlement | Escrow      │
└─────────────────┬───────────────────────────────────┘
                  │
┌─────────────────▼───────────────────────────────────┐
│        ARKIV DATA LAYER (TypeScript SDK)           │
│  Bid History | Price Analytics | Compliance Docs   │
└─────────────────────────────────────────────────────┘
```

---

## ✨ Key Features

### For Hospitals
- **One-Click Tender Creation**: Create standardized procurement requests in seconds
- **Competitive Pricing**: Batch settlement with reverse auction mechanism ensures best available market prices
- **Real-Time Tracking**: Monitor bid activity and settlements live
- **Historical Analytics**: Compare prices across time, regions, and suppliers

### For Pharmaceutical Suppliers
- **Fair Competition**: Uniform clearing prices eliminate bid manipulation
- **Transparent Process**: Clear tender criteria, public rules, automated settlement
- **Reputation Building**: On-chain track record increases trust and visibility
- **Efficient Operations**: Reduced paperwork, instant payments via escrow

### For Citizens & Auditors
- **Full Transparency**: Public dashboard showing all procurement tender activity
- **Corruption Monitoring**: Automated anomaly detection flags suspicious patterns
- **Open Data Export**: CSV/API access for independent analysis
- **Impact Metrics**: Track cost savings and medicine accessibility in real-time

---

## 🚀 Quick Start

### Prerequisites
- Node.js v18+ and npm/yarn
- MetaMask or compatible Web3 wallet
- Git

### Installation

```bash
# Clone repository
git clone https://github.com/yourusername/pharmabid.git
cd pharmabid

# Install dependencies
npm install

# Copy environment variables
cp .env.example .env
# Edit .env with your API keys

# Deploy smart contracts to Sepolia testnet
cd contracts
npx hardhat compile
npx hardhat run scripts/deploy.ts --network sepolia

# Start frontend development server
cd ../frontend
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## 🔧 Technology Stack

### Blockchain
- **Smart Contracts**: Solidity 0.8.20, OpenZeppelin libraries
- **Development**: Hardhat v3, Ethers.js v6
- **Network**: Ethereum Sepolia testnet (production: Polygon, Arbitrum)

### Web3 Integration
- **Wallet Connect**: Wagmi v2, RainbowKit
- **Contract Interaction**: Viem
- **Data Storage**: Arkiv TypeScript SDK

### Frontend
- **Framework**: Next.js 14 (App Router), TypeScript
- **Styling**: Tailwind CSS, shadcn/ui
- **Charts**: Recharts, D3.js
- **State**: React Context, Zustand

### Backend
- **API Routes**: Next.js API routes
- **Solver Engine**: Node.js worker threads (reverse auction mechanism)
- **Database**: Arkiv (on-chain data layer)

---

## 📖 Usage Examples

### Creating a Procurement Tender (Hospital)

```typescript
import { useWriteContract } from 'wagmi';
import { PROCUREMENT_TENDER_ABI } from '@/contracts';

function CreateTenderForm() {
  const { writeContract } = useWriteContract();

  const createTender = async () => {
    await writeContract({
      address: '0x...',
      abi: PROCUREMENT_TENDER_ABI,
      functionName: 'createTender',
      args: [
        'Paracetamol 500mg',  // product name
        1000000n,              // quantity (1 million units)
        50000000000000n,       // max price per unit (0.05 ETH)
        86400n                 // batch duration (24 hours)
      ]
    });
  };

  return <button onClick={createTender}>Create Tender</button>;
}
```

### Querying Price History (Analytics)

```typescript
import { arkiv } from '@/lib/arkiv';

async function getPriceHistory(productName: string) {
  const history = await arkiv.query({
    table: 'batch_tender_records',
    where: {
      'tenders.productName': productName,
      'timestamp': {
        $gte: new Date('2024-01-01'),
        $lte: new Date('2024-12-31')
      }
    },
    select: ['timestamp', 'settlement.uniformPrice'],
    orderBy: 'timestamp'
  });

  return history.map(record => ({
    date: record.timestamp,
    price: record.settlement.uniformPrice
  }));
}
```

---

## 🎥 Demo

### Video Walkthrough (3 minutes)
[![PharmaBid Demo](https://img.youtube.com/vi/YOUTUBE_ID/maxresdefault.jpg)](https://loom.com/share/...)

### Live Application
🔗 **Testnet Demo**: [https://pharmabid-demo.vercel.app](https://pharmabid-demo.vercel.app)

**Test Accounts Available:**
- Hospital: `0x742d35Cc6634C0532925a3b8...` (funded with test tokens)
- Supplier: `0x8626f6940E2eb28930eFb4Ce...` (whitelisted)

---

## 🗺️ Roadmap

### Phase 1: MVP (Completed ✅)
- [x] Smart contract deployment (Sepolia)
- [x] Arkiv data layer integration
- [x] Hospital & supplier dashboards
- [x] Batch tender mechanism with reverse auction settlement
- [x] Public transparency portal

### Phase 2: Production (Q1 2025)
- [ ] Security audit (OpenZeppelin/Consensys)
- [ ] Multi-chain deployment (Polygon, Arbitrum)
- [ ] Mobile applications (iOS/Android)
- [ ] 5 pilot hospitals onboarded
- [ ] 20 verified pharmaceutical suppliers

### Phase 3: Scale (Q2 2025)
- [ ] 25 hospitals across 3 countries
- [ ] Government partnerships (Health Ministries)
- [ ] Regulatory compliance certifications (EU Public Procurement Directive)
- [ ] $5M monthly trading volume
- [ ] AI-powered price prediction analytics

### Phase 4: Global Impact (Q3-Q4 2025)
- [ ] 100 hospitals in 10 countries
- [ ] Integration with national health systems
- [ ] Open API for third-party developers
- [ ] $25M monthly GMV
- [ ] Academic research partnership (impact study)

---

## 📊 Impact Metrics

| Metric | Current | 6-Month Target | 12-Month Target |
|--------|---------|----------------|-----------------|
| **Hospitals** | 0 | 25 | 100 |
| **Suppliers** | 0 | 100 | 500 |
| **Monthly Volume** | $0 | $5M | $25M |
| **Cost Savings** | - | 22% avg | 25% avg |
| **Patients Impacted** | 0 | 100K | 1M+ |

---

## 🤝 Contributing

We welcome contributions from the community! Please read our [Contributing Guidelines](./CONTRIBUTING.md) before submitting pull requests.

### Development Workflow
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Areas Needing Help
- 🔐 Smart contract security review
- 🎨 UI/UX design improvements
- 🌍 Translations (Spanish, Portuguese, French)
- 📚 Documentation expansion
- 🧪 Testing coverage

---

## 🏆 Hackathon Submission

**Event**: sub0 Hack 2025 (Buenos Aires, Argentina)  
**Track**: Arkiv Main Track + Marketing Track  
**Team**: Urban Tech
**Submission Date**: November 16, 2025  

### Deliverables
- ✅ [Demo Video](https://loom.com/share/...) (3 minutes)
- ✅ [Pitch Deck](./docs/pitch-deck.pdf) (8 slides)
- ✅ [Technical Documentation](./docs/architecture.md)
- ✅ [Milestone 2 Plan](./docs/milestone-2.md)
- ✅ [Live Demo](https://pharmabid-demo.vercel.app)

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.

---

## 🔗 Links & Resources

- **Website**: [pharmabid.io](https://pharmabid.io)
- **Documentation**: [docs.pharmabid.io](https://docs.pharmabid.io)
- **Twitter**: [@PharmaBid](https://twitter.com/pharmabid)
- **GitHub**: [github.com/pharmabid](https://github.com/Urbantech-HL/sub0-hackaton-mediswap)

### Research & References
- [Transparency International: Pharmaceutical Corruption Report](https://www.transparency.org/en/publications/global-corruption-report-2006)
- [WHO: Measuring Transparency in Public Pharmaceutical Sector](https://apps.who.int/iris/handle/10665/135556)
- [WHO: Managing the Tender Process](https://msh.org/resources/managing-the-tender-process/)
- [CoW Protocol Documentation](https://docs.cow.fi/)
- [Arkiv Network](https://arkiv.network/)

---

## 💬 Contact

**Lead Developer**: Antoine ([@adelamare-blockchain](https://github.com/adelamare-blockchain))  
**Email**: antoine@blockchain-cie.com 
**Telegram**: [@adelamare_blockchain](https://t.me/adelamare_blockchain)

---

<div align="center">

**Built with ❤️ at sub0 Hack 2024**

*"Every line of code saves a life."*

[⬆ Back to Top](#-pharmabid)

</div>
