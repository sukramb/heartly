# heartly

Heartly – Flash Sale SaaS Platform
Business Overview

Heartly is a B2C experience delivered via B2B SaaS.

Merchants (B2B) subscribe to Heartly and instantly get a dedicated mobile app (iOS/Android) for their online shop.
End-customers (B2C) download this app to access exclusive flash sales — limited-time, limited-stock deals that drive urgency and engagement.

Key Business Value

For Merchants:

Increase conversion through FOMO-driven flash sales

Provide a branded mobile app without custom development costs

Manage flash sales easily via dashboard connected to Shopify

For Customers:

Get a simple, branded app dedicated to their favorite shop

Receive push notifications about exclusive deals

Enjoy fast checkout (Apple Pay / Google Pay)

Heartly = “Shopify merchants get their own shopping app with flash-sale power.”

Technical Overview

Heartly is a multi-tenant SaaS platform hosted on Vercel (Frontend) and Railway (Backend microservices).
It provides:

A Merchant Dashboard (to configure flash sales)

Customer-facing Apps (container app or white-label app per merchant)

A Super Admin Panel (for operator visibility across all merchants)

Target Architecture
Frontend (Vercel)

Next.js + TailwindCSS + Framer Motion

Landing Page (one-scroll)

Merchant Dashboard: flash sale creation, iPhone mockup preview

Backend (Railway – Microservices)

API Gateway with rate limiting & authentication

Microservices with dedicated PostgreSQL DBs:

Tenant & Billing

Catalog Connector (Shopify)

Flash Sale Engine

Order & Payment

Notify (Push)

Analytics

Audit & Compliance

Super Admin API

Mobile (Flutter)

Option A: Heartly container app (multi-tenant, theme per shop)

Option B: White-label apps for each merchant (separate App Store presence)

Features: push notifications, realtime stock countdown, fast checkout

Core Features

From the Business Perspective

Dedicated App per Merchant (B2C)

End-customers download a shop-specific Heartly app

Each app carries merchant branding and product catalog

Flash sales appear as special “event windows” inside the app

Flash Sale Creation (B2B)

Merchant dashboard → load products via Shopify API

Define discounts, timing, and stock limits

Preview sale in iPhone mockup before publishing

Flash Sale Experience (B2C)

Countdown timers, limited stock visibility (urgency/FOMO)

Push notification at sale start

Apple Pay / Google Pay for instant checkout

Analytics & KPIs (B2B)

Merchant dashboard with tiles: revenue, participants, conversion rates

Insights into flash sale performance

Super Admin Panel (Operator view)

Multi-tenant overview: all merchants, total revenue, number of flash sales

Audit logs: merchant activity, API calls, feature usage

Tech Stack

Frontend: Next.js, TailwindCSS, Framer Motion (Vercel)

Backend: Node.js/Express, Firebase, Railway microservices

Database: PostgreSQL (separate DB per service; RLS for multi-tenancy)

Mobile: Flutter (iOS + Android, container or white-label)

Integrations: Shopify API (API Key → later OAuth)

Payments: Shopify Checkout / Stripe with Apple Pay & Google Pay

Development Priorities

Landing Page (modern, one-scroll)

Merchant Dashboard (login, flash sale creator, Shopify integration)

Backend Microservices (tenant-aware DBs, audit logging)

Super Admin Panel (global metrics and tenant management)

Mobile Container App (multi-tenant, branded themes)

Push Notifications & Checkout (Apple Pay/Google Pay integration)

🔑 In Short:
Heartly lets merchants give their customers a dedicated flash-sale shopping app — while the operator runs a multi-tenant SaaS backend with secure, granular microservices and a Super Admin panel.
