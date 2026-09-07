# AIT - TalentShare: Technical System Architecture

## 1. System Overview & Core Philosophy
**AIT - TalentShare** is engineered as a curated talent ecosystem operated by **Agrabad IT (AIT)**. It features an escrow-backed financial ledger, multi-role RBAC, dynamic badges, versioned submissions, and strict anti-disintermediation protections.

---

## 2. Core Architectural Pillars

### 2.1 Two Marketplace Models (Unified Opportunity Engine)
1. **Contest Model (Primary)**:
   - Buyer posts brief & budget.
   - Admin reviews, configures parameters, and approves.
   - Buyer pays escrow to Agrabad IT.
   - Admin publishes contest -> eligible sellers submit work.
   - Buyer reviews submissions, requests revisions, and selects **strictly ONE winner**.
   - Admin verifies outcome and authorizes payment release.
   - Winner's wallet is credited (Budget minus configurable platform commission).
2. **Direct Assignment Model**:
   - Buyer requests or Admin directly assigns a task to a designated seller.
   - Seller accepts -> submits work -> buyer reviews -> completion -> Admin releases payment.

### 2.2 Strict Admin Escrow & No-Winner Resolution Policy
- **No Direct Transfers**: Funds are held in Agrabad IT platform escrow.
- **Admin Escrow Release Gate**: Buyer selecting a winner does not automatically release funds; it requests an Admin payment release.
- **Failed / No-Winner Contests**: No automatic refunds. Funds remain pending; Admin executes a manual financial resolution (`FULL_REFUND`, `PARTIAL_REFUND`, `BUYER_CREDIT`, `REPOST_CONTEST`, `EXTEND_DEADLINE`) with an immutable audit trail.

### 2.3 Strict Privacy & Anti-Disintermediation (Zero Internal Chat in V1)
- Buyers evaluate sellers solely based on portfolio, submissions, credentials, and verification badges.
- **Zero Private Contact Exposure**: Phone numbers, personal emails, and private handles are stripped via server-side DTO projection (`toPublicSellerProfile`).
- **No In-Platform Chat in V1**: Structured revision notes and public/task briefs keep all interactions transparent and trackable.

---

## 3. Immutable Financial Ledger Architecture
The financial architecture uses an immutable ledger model:
- `BUYER_PAYMENT`: Inflow from buyer to platform escrow.
- `PLATFORM_COMMISSION`: Platform revenue retained by Agrabad IT (default 20%).
- `SELLER_PAYOUT_HELD`: Escrow staged in seller pending balance.
- `SELLER_PAYMENT_RELEASED`: Admin authorization moves funds from pending to available balance.
- `BUYER_REFUND`: Admin manual refund to buyer.
- `WITHDRAWAL_REQUEST`: Seller initiates withdrawal (debits available balance, creates hold).
- `WITHDRAWAL_PROCESSED`: Admin disburses funds via bKash / Nagad / Bank Transfer.

---

## 4. Domain State Machines

### 4.1 Task Lifecycle
`DRAFT` $\rightarrow$ `PENDING_ADMIN_REVIEW` $\rightarrow$ `APPROVED` $\rightarrow$ `PAYMENT_PENDING` $\rightarrow$ `PUBLISHED` $\rightarrow$ `ACTIVE` $\rightarrow$ `UNDER_REVIEW` $\rightarrow$ `COMPLETED` / `CLOSED` / `CANCELLED` / `DISPUTED`

### 4.2 Submission Lifecycle
`SUBMITTED` $\rightarrow$ `UNDER_REVIEW` $\rightarrow$ `SHORTLISTED` / `REVISION_REQUIRED` $\rightarrow$ `ACCEPTED` $\rightarrow$ `WINNER`

---

## 5. Storage & Payment Provider Abstraction
- **Storage**: `StorageProvider` interface with local disk driver (randomized UUID keys, path traversal validation, signed URL generation) and S3 driver ready for production deployment.
- **Payments**: `PaymentProvider` interface with MockProvider and gateways ready for bKash, Nagad, and SSLCommerz.
