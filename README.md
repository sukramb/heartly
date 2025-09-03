# Heartly – Flash Sale SaaS Platform

## Business Overview
**Heartly** is a **B2C shopping experience delivered via B2B SaaS**.  

Merchants (B2B) subscribe to Heartly and instantly get a **dedicated mobile app (iOS/Android)** for their online shop.  
End-customers (B2C) download this app to access **exclusive flash sales** — limited-time, limited-stock deals that drive urgency and engagement.  

### Value Proposition
- **For Merchants:**  
  - Launch flash sales without custom development  
  - Provide a branded mobile app to customers  
  - Increase conversion rates with urgency-driven sales  
- **For Customers:**  
  - Simple, branded app dedicated to their favorite shop  
  - Push notifications about exclusive deals  
  - Fast checkout (Apple Pay / Google Pay)

---

## Technical Overview
Heartly is a **multi-tenant SaaS platform** hosted on **Vercel (Frontend)** and **Railway (Backend microservices)**.  
It provides:  
- A **Merchant Dashboard** (for flash sale setup and analytics)  
- **Customer-facing mobile apps** (container app or white-label)  
- A **Super Admin Panel** (for operator visibility across all merchants)  

---

## Target Architecture

### Frontend (Vercel)
- Next.js + TailwindCSS + Framer Motion  
- Landing Page (one-scroll)  
- Merchant Dashboard: flash sale creation, iPhone mockup preview  

### Backend (Railway – Microservices)
- **API Gateway** – rate limiting, authentication passthrough, request tracing  
- **Microservices (each with own DB):**  
  - Tenant & Billing Service  
  - Catalog Connector Service (Shopify)  
  - Flash Sale Service  
  - Order & Payment Service  
  - Notify Service (Push)  
  - Analytics Service  
  - Audit & Compliance Service  
  - Super Admin API  

- **Eventing:** Redis Streams / NATS  
- **Secrets:** Railway Vars + optional external Secrets Manager  

### Mobile (Flutter)
- **Option A:** Heartly container app (multi-tenant, shop theming)  
- **Option B:** White-label apps per merchant (published under merchant Dev Accounts)  
- Features: realtime stock counters, Apple/Google Pay, push notifications  

---

## Core Features

### Business Perspective
1. **Dedicated App per Merchant (B2C)**  
   - End-customers download a shop-specific Heartly app  
   - Each app is branded and tied to the merchant’s catalog  
   - Flash sales appear as special event windows  

2. **Flash Sale Creation (B2B)**  
   - Merchants load products via Shopify API  
   - Set discounts, timing, and stock limits  
   - Preview sales in an iPhone mockup  

3. **Flash Sale Experience (B2C)**  
   - Countdown timers and limited stock (FOMO effect)  
   - Push notifications at sale start  
   - One-click checkout via Apple/Google Pay  

4. **Analytics & KPIs (B2B)**  
   - Revenue, participants, conversion rates shown in dashboard  
   - Performance insights for flash sales  

5. **Super Admin Panel (Operator)**  
   - Overview of all tenants and KPIs  
   - Metrics: revenue, sales count, feature usage  
   - Tenant activity logs and audit trails  

---

## Data Architecture

### Database per Microservice
- **Tenant & Billing DB:** tenants, plans, feature flags, settings  
- **Catalog DB:** product cache, encrypted Shopify tokens  
- **Flash Sale DB:** flash sales, items, inventory locks, stats  
- **Order & Payment DB:** orders, order items, payments, refunds, webhooks  
- **Notify DB:** device tokens, topics, message logs  
- **Analytics DB:** events, daily KPIs, realtime KPIs  
- **Audit DB:** immutable append-only log  

### Tenant Isolation
- Default: Shared tables with `tenant_id` + Row Level Security (RLS)  
- Optional: Schema-per-tenant or DB-per-tenant for premium isolation  

---

## Tech Stack
- **Frontend:** Next.js, TailwindCSS, Framer Motion (Vercel)  
- **Backend:** Node.js / Express, Firebase, Railway microservices  
- **Database:** PostgreSQL (per service, RLS enforced)  
- **Mobile:** Flutter (iOS + Android)  
- **Integrations:** Shopify API (API Key → OAuth later)  
- **Payments:** Shopify Checkout / Stripe + Apple/Google Pay  

---

## Development Priorities
1. Landing Page (modern, one-scroll)  
2. Merchant Dashboard (login, flash sale creation, Shopify API integration)  
3. Backend Microservices (tenant-aware DBs, audit logging)  
4. Super Admin Panel (global metrics and tenant management)  
5. Mobile Container App (multi-tenant, branded themes)  
6. Push Notifications & Checkout (Apple Pay / Google Pay integration)  

---

## CI/CD & Environments
- **Repos:** mono-repo or multi-repo (per service)  
- **Pipelines (GitHub Actions):**  
  - Backend: Lint/Test → Build → Deploy (Railway)  
  - Mobile: Lint/Test → Fastlane → App Store Connect / Play Console  
- **Environments:** dev, staging, prod → isolated DBs per service & env  

---

## Operational Policies
- Rate limiting per tenant and per IP  
- Idempotent orders with request keys  
- Inventory locks (optimistic or pessimistic)  
- Observability with OpenTelemetry and central logging  
- Service-level runbooks for incidents  

---

## Example Schemas

**Flash Sale DB**
