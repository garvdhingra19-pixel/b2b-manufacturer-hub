# ARCHITECTURE CONSTITUTION & LOCKED DECISIONS
> Status: IMMUTABLE CORE | Region: India (`ap-south-1` / DPDP & CERT-In Compliant)

## 1. Locked Tech Stack (Decision Gates #1 & #2)
- **Monorepo**: Turborepo (`apps/web`, `apps/collector-agent`, `packages/database`, `packages/contracts`)
- **Full-Stack Web & API**: Next.js 15 (App Router, TypeScript, Server Actions + Route Handlers)
- **Database**: PostgreSQL 16 + Prisma ORM + `pgvector` (for semantic spec-to-factory matching)
- **Auth**: Auth.js (NextAuth v5) backed by PostgreSQL (Zero external vendor lock-in)
- **Storage**: S3-Compatible (Cloudflare R2 / AWS S3 Mumbai) with 15-minute pre-signed NDA URLs
- **Data Collector**: Python 3.11+ (`apps/collector-agent`) writing via strict Zod/Pydantic schema contracts

## 2. Locked Business & Domain Rules
- **Initial Verticals**: Strictly `APPAREL_TEXTILES` and `CUSTOM_PACKAGING`.
- **Directory-First Model**: Manufacturers start as `UNCLAIMED_PUBLIC_RECORD` populated from verified public registries (GST/MSME/Industrial Directories).
- **Scam Filter**: `isConfirmedManufacturer` is TRUE only when official registration explicitly includes Manufacturing/Factory activity.

## 3. Non-Negotiable Security & Regulatory Guardrails
- **DPDP Act 2023 Shield**: Never display personal mobile numbers on public pages. Store claim phone numbers encrypted (`AES-256-GCM`) in `encryptedContactVault`.
- **IT Act Sec 79 Safe Harbor**: Every profile exposes a `TakedownRequest` workflow and displays factual verification badges rather than subjective platform guarantees.
- **IP Protection**: Founder attachments are hashed (`SHA-256`) on upload and locked behind a recorded `NdaAcceptance` database row before generating a pre-signed download link.
- **CERT-In 180-Day Audit Trail**: Every state change writes an append-only row to `SecurityAuditLog`.