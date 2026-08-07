# WatchTowerX

Live demo: https://ping-alert-chi.vercel.app

A modern monitoring and alerting platform built with Next.js, Clerk, Stripe, PostgreSQL/Neon, Discord, and Tailwind CSS.

WatchTowerX is designed for teams who want instant, actionable event notifications delivered directly to Discord and a beautiful analytics dashboard for real-time uptime and event tracking.

---

## 🚀 What this project does

- Provides a polished public landing page for WatchTowerX.
- Supports user signup and sign-in using Clerk.
- Offers a secure dashboard where authenticated users can:
  - create event categories with emoji and color labels
  - manage custom categories
  - view analytics for category event traffic
  - manage their API key
  - upgrade to Pro using Stripe
- Accepts event ingestion via a protected API endpoint and delivers notifications to a Discord DM channel.
- Automatically tracks monthly event quota usage and enforces plan limits.
- Handles Stripe webhook events to upgrade users after successful payments.

---

## ✨ Key features

- **Beautiful Next.js landing and dashboard UI** with animation, responsive layout, and dark mode
- **Clerk authentication** for secure sign-in / sign-up flows
- **Stripe checkout** for one-time lifetime access and plan upgrades
- **Discord DM alerts** for event notifications through a bot
- **API key management** for secure event ingestion
- **Category-based event tracking** with dynamic fields, quota enforcement, and analytics
- **Prisma + Neon** database integration for fast, serverless data access
- **Stateful usage limits** for free and pro plans

---

## 🧱 Architecture

- `src/app` — Next.js app routes, pages, and layouts
- `src/components` — UI components, landing page blocks, dashboard widgets
- `src/lib` — reusable client utilities, Discord client, Stripe helpers
- `src/db.ts` — Prisma client setup for Neon database
- `src/server` — backend router and procedure layer
- `src/app/api/v1/events/route.ts` — authenticated event ingestion endpoint
- `src/app/api/webhooks/stripe/route.ts` — Stripe webhook handler

---

## 📁 Notable pages

- `/` — Landing page
- `/pricing` — Stripe pricing and checkout page
- `/sign-up` — Clerk sign-up flow
- `/sign-in` — Clerk sign-in flow
- `/dashboard` — Authenticated dashboard overview
- `/dashboard/upgrade` — Upgrade and payment success flow
- `/dashboard/category/[name]` — Event category details
- `/dashboard/(settings)/api-key` — API key management
- `/dashboard/(settings)/account-settings` — User profile settings

---

## 🔧 Tech stack

- **Next.js 16** with App Router
- **TypeScript**
- **Tailwind CSS** + **tailwindcss-animate**
- **Clerk** authentication
- **Stripe** payments
- **Discord.js REST** for Discord bot messages
- **Prisma** + **@neondatabase/serverless** adapter
- **React Query** for client data fetching
- **Framer Motion** for polished page animation
- **Radix UI** for accessible components

---

## 🌐 Environment variables

The app currently depends on the following environment values:

- `DATABASE_URL` — Neon / PostgreSQL connection string
- `NEXT_PUBLIC_APP_URL` — Base app URL used for Stripe redirects
- `STRIPE_SECRET_KEY` — Stripe server secret key
- `STRIPE_PRICE_ID` — Stripe product price identifier
- `STRIPE_WEBHOOK_SECRET` — Stripe webhook signing secret
- `DISCORD_BOT_TOKEN` — Discord bot token for DM delivery
- Clerk variables as required by Clerk Next.js (`CLERK_*`)

> The project also uses `NODE_ENV` to select the correct Prisma/Neon client behavior.

---

## 🧪 API usage

### Event ingestion endpoint

- `POST /api/v1/events`

Headers:

```http
Authorization: Bearer <API_KEY>
Content-Type: application/json
```

Body:

```json
{
  "category": "bug",
  "description": "An error has occurred in the checkout flow.",
  "fields": {
    "userId": "1234",
    "status": "failed",
    "amount": 49.99
  }
}
```

If the request is valid, WatchTowerX delivers an embedded Discord message to the user's registered Discord account.

---

## 🧩 Plans and quotas

- **Free plan**
  - 3 event categories
  - 100 events per month
- **Pro plan**
  - 10 event categories
  - 1,000 events per month

---

## 🚀 Local setup

```bash
cd watchtower-x
pnpm install
pnpm dev
```

If you prefer npm:

```bash
npm install
npm run dev
```

Then set up your `.env` file with the required variables and run Prisma migrations.

---

## 🗂 Prisma / database

- Prisma is configured with `@prisma/client` and the Neon adapter
- `src/db.ts` handles global cached Prisma instances for development
- Use `prisma migrate dev` to apply schema migrations

---

## 💡 Why this project stands out

WatchTowerX is not just a generic monitoring app — it is a complete workflow for developers and product teams who want:

- event-based alerts delivered to Discord
- intuitive category management and dashboards
- frictionless onboarding via Clerk
- a polished marketing presence and pricing flow

It combines real-time delivery, product analytics, and a premium purchase experience into a modern full-stack Next.js application.

---

## 📌 Notes

- The app is branded internally as `WatchTowerX`.
- Checkout is implemented as a one-time lifetime plan purchase.
- The Discord integration uses bot DMs and embeds.
- The project includes both `pnpm-lock.yaml` and `package-lock.json`, so either package manager can be used.

---

## 📞 Need help?

If you want, I can also add a shorter landing README, deployment instructions, or a project presentation summary for `watchtower-x`.
