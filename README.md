# Shopping Website

A full-stack shopping website project inspired by PC e-commerce flows (product browsing, cart, checkout, likes, order tracking, and admin management), built with SvelteKit + Prisma + MySQL.

---

## Project Highlights

- **Full-stack flow in one repo**: frontend pages + server endpoints + relational database schema
- **Data-heavy shopping experience**: product table with search/sort/pagination, likes, cart, and checkout
- **Role-based UI**: separate navigation and management pages for normal users vs admin users
- **Practical DB design**: Prisma models covering products, users, cart, orders, payment info, and many-to-many relations
- **Local reproducibility**: Docker Compose bootstraps MySQL and seeded data via `init.sql`

---

## Tech Stack

- **Frontend**: SvelteKit, Svelte, Skeleton UI, Tailwind CSS, Flowbite
- **Backend**: SvelteKit server routes (`+server.js`)
- **Database**: MySQL 8, Prisma ORM
- **Tooling**: Node.js, npm, Docker Compose, Vite, Prettier, Playwright

---

## Architecture Overview

```text
Svelte UI (routes/*.svelte)
   |
   | fetch(...)
   v
SvelteKit Server Routes (routes/**/+server.js)
   |
   v
Data Access Layer (src/lib/server/server.js)
   |
   v
Prisma Client (src/lib/server/prisma.js)
   |
   v
MySQL (Docker, initialized by init.sql)
```

### Key folders

- `src/routes/`
  - UI pages (`+page.svelte`)
  - HTTP endpoints (`+server.js`) for CRUD and business operations
- `src/lib/server/server.js`
  - centralized DB operations (query/create/update/delete)
- `prisma/schema.prisma`
  - relational schema and constraints
- `docker-compose.yml`
  - local MySQL container setup
- `init.sql`
  - DB initialization/seed data

---

## Core Features

### User Side

- Registration and login
- Product browsing with:
  - sorting
  - pagination
  - keyword search + search-history persistence
- Add-to-cart and quantity update
- Product likes and liked-list
- Checkout flow (payment + delivery info)
- Transaction history page (with order status)
- Currency exchange utility page

### Admin Side

- Product management (create/update/delete)
- User list and user deletion
- Transaction overview across orders and payments

---

## Data Model Snapshot

Main entities from `prisma/schema.prisma`:

- `user`, `user_phone`
- `product`
- `cart_item`
- `liking_list`
- `orders`, `order_item`
- `paying_info`, `paying`
- `search_history`

This schema covers:

- **many-to-many joins** (`cart_item`, `liking_list`, `order_item`, `paying`)
- **order and payment lifecycle**
- **user behavior tracking** (search history, likes, purchases)

---

## Local Setup

### 1) Prerequisites

- Node.js + npm
- Docker + Docker Compose

### 2) Install dependencies

```bash
npm install
```

### 3) Configure environment

Create `.env` in project root and copy values from `.env.example`:

```env
MYSQL_ROOT_PASSWORD=123456789
MYSQL_DATABASE=Team5DBFinal
MYSQL_PASSWORD=team5
MYSQL_USER=team5
MYSQL_PORT=8000
DATABASE_URL="mysql://root:123456789@localhost:8000/Team5DBFinal"
```

### 4) Start database

```bash
docker-compose up --build -d
```

### 5) Run app

```bash
npm run dev
```

Open the app in browser (usually `http://localhost:5173`).

---

## Demo Accounts

Default admin account in seeded data:

```text
account: admin
password: admin
```

---

## Scripts

```bash
npm run dev
npm run build
npm run preview
npm run check
npm run lint
npm run format
npm run test
```

---

## Talking Points

- Designed and integrated a complete shopping workflow from DB schema to UI interactions.
- Built modular server routes and centralized Prisma data access for maintainable backend logic.
- Implemented role-specific UX and admin operations without splitting into separate projects.
- Applied relational modeling for orders, payments, and product interactions in a real-world-like domain.
- Containerized local database environment to improve setup consistency across team members.

---

## Current Limitations

- Authentication/session flow is lightweight (not production-grade auth/session hardening).
- Sensitive data handling and credential management still need production-level improvements.
- Automated testing exists but is currently minimal.

---

## Future Improvements

- Add secure authentication/session strategy (hashing, token/cookie session, authorization guards).
- Split service layer into domain modules and add request validation middleware.
- Improve transaction handling for checkout consistency.
- Expand E2E and integration test coverage.
- Add CI pipeline and deployment-ready environment profiles.

---

## Team

1. Akinom  
2. [SunGj](https://github.com/SunGj921028)  
3. KJC  
4. Notpotato
