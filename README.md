# Sunday Studio — curated lifestyle shop

A responsive multi-page lifestyle store with a pastel storefront, persistent shopping bag, demo checkout, Express API for local development, Netlify Functions for deployment, and a PostgreSQL Prisma schema.

## Deploy on Netlify

In the Netlify site settings, set the **Base directory** to the project root (the folder containing `netlify.toml`) and deploy. The included config publishes `public/`, routes `/api/*` to a serverless function, and sends other paths to the storefront. No build command is required. If you uploaded only the `public` folder before, redeploy the complete project folder so Netlify can package the function.

## Run locally

Requires Node.js 18 or later.

```sh
npm install
npm run dev
```

Open http://localhost:3000. The local Express server serves the storefront and API. Checkout simulates an order and does not collect or process real payments.

## API

- `GET /api/products` — product list; optional `category`, `search`, and `sort=low|high` query values.
- `GET /api/products/:id` — one product.
- `POST /api/checkout` — validates a non-empty cart and email and returns a simulated order receipt.

In Netlify, these routes run through `netlify/functions/api.mjs`. The browser cart persists in `localStorage`. Promo code `SUNDAY10` displays a demo validation message. Use `/#/admin` for the sample admin overview.

## Database setup

`prisma/schema.prisma` defines users, products, and orders. To connect PostgreSQL and generate the client, install Prisma (`npm install prisma @prisma/client`), set `DATABASE_URL` in `.env`, and run `npx prisma migrate dev --name init`. The current API uses in-memory sample catalog data and simulated checkout; it does not yet persist orders, authenticate users, or connect to a payment provider. Replace the mock handler with verified server-side payment processing before accepting real payments.

## Environment

- `PORT` (optional, local server default `3000`)
- `DATABASE_URL` (only needed when enabling Prisma persistence)

Product imagery uses remote Unsplash URLs and Google Fonts, so those assets need network access.
