# AIT - TalentShare (Agrabad IT Talent Marketplace)

> **Verified Talent. Real Opportunities.**  
> A curated, enterprise-grade talent marketplace and escrow engine operated by **Agrabad IT (AIT)** in partnership with the Kaarjo ecosystem.

---

## 🌟 Overview & Product Context
Agrabad IT is an established EdTech institution teaching high-demand IT, design, and freelancing skills. **AIT - TalentShare** bridges education with economic empowerment by allowing students, alumni, and Kaarjo-verified talent to participate in real-world contests and assignments posted by companies, organizations, and individuals under strict Admin escrow and quality curation.

### Core Ecosystem Loop
```
       [ LEARN at Agrabad IT ]
                 ↓
      [ BUILD VERIFIED SKILLS ]
                 ↓
     [ EARN VERIFICATION BADGES ]
                 ↓
    [ CURATED TALENT PROFILE ]
                 ↓
   [ DISCOVER CONTESTS / ASSIGNMENTS ]
                 ↓
    [ SUBMIT WORK & REVISION VERSIONS ]
                 ↓
   [ WIN / GET SELECTED BY BUYER ]
                 ↓
 [ ESCROW RELEASED BY ADMIN TO WALLET ]
                 ↓
 [ WITHDRAW VIA BKASH / NAGAD / BANK ]
```

---

## 🛠️ Technology Stack
- **Frontend & Fullstack Framework**: Next.js 14 (App Router), React 18, TypeScript (Strict Mode)
- **Styling & UI**: Tailwind CSS, Lucide Icons, Accessible Design Tokens
- **Database & ORM**: PostgreSQL with Prisma ORM
- **Validation**: Zod
- **Security & Crypto**: bcryptjs, jose (JWT), HTTP-Only Secure Cookies, Server-Side DTO Projection
- **Testing**: Vitest
- **Storage**: Storage Abstraction Layer (Local secure disk storage + S3/R2 interface)
- **Payments**: Payment Provider Abstraction (bKash, Nagad, SSLCommerz, Mock Provider)
- **Email & Notifications**: In-App Notification Center + Templated Transactional Email Logging

---

## 🚀 Getting Started

### 1. Prerequisites
- Node.js `v20+` or `v24+`
- PostgreSQL database instance

### 2. Environment Setup
Copy `.env.example` to `.env`:
```bash
cp .env.example .env
```

Configure your PostgreSQL connection string in `.env`:
```env
DATABASE_URL="postgresql://postgres:postgres@localhost:5432/ait_talentshare?schema=public"
JWT_SECRET="your-secure-jwt-secret-key"
```

### 3. Install Dependencies & Generate Prisma Client
```bash
npm install
npx prisma generate
```

### 4. Database Setup & Seed
```bash
npx prisma db push
npm run db:seed
```

### 5. Running the Application
```bash
npm run dev
```
Open [http://localhost:3000](http://localhost:3000) to view the Foundation Status Dashboard.

---

## 🧪 Testing & Verification
Run the automated unit and domain test suite:
```bash
npm run test
```

Type checking:
```bash
npm run typecheck
```

---

## 👥 Seed Accounts (Development)
| Role | Email | Password | Details |
|---|---|---|---|
| **Admin** | `admin@ait.edu.bd` | `Password123!` | Agrabad IT Administrator |
| **Buyer** | `buyer@techfusion.com` | `Password123!` | TechFusion Bangladesh Ltd. |
| **Seller (AIT Student)** | `student@ait.edu.bd` | `Password123!` | Sabbir Hossain (Batch 42 Graphic Designer) |
| **Seller (Kaarjo Talent)** | `kaarjo.talent@kaarjo.com` | `Password123!` | Nusrat Jahan (Motion Graphics Specialist) |

---

## 📄 License & Ownership
Copyright © 2026 Agrabad IT (AIT). All rights reserved.
