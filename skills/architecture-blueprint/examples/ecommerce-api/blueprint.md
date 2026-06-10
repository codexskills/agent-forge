# E-Commerce API — Architecture Blueprint

## 1. Project Overview
A RESTful e-commerce backend API supporting product catalog, shopping cart, checkout with payments, order management, and admin dashboard. Headless — no frontend in scope.

## 2. Feasibility Assessment
**Complexity:** Complex
**Effort:** 8-12 weeks (3-person team)
**Verdict:** PROCEED

**Top 3 Risks:**
1. Payment processing integration — PCI compliance, failed payments, refunds
2. Inventory management — race conditions on concurrent purchases
3. Order state machine — incorrect transitions lead to shipping errors

## 3. Architecture

### Pattern: Modular Monolith

### Stack
| Layer | Technology |
|---|---|
| Runtime | Node.js + Fastify |
| Database | PostgreSQL |
| Cache | Redis (cart, sessions, product cache) |
| Queue | BullMQ (order processing, emails) |
| Payments | Stripe |
| Search | Meilisearch (product search) |
| Auth | JWT (lucia-auth) |
| Hosting | Railway |

## 4. Data Model

### Product
id, name, slug, description, price (integer, cents), compare_at_price, sku, inventory_count, status (active/draft/archived), images (JSONB), created_at, updated_at

### Cart
id, user_id (FK, nullable for guest), session_id, created_at, updated_at

### CartItem
id, cart_id (FK), product_id (FK), quantity, unit_price (snapshot at add time)

### Order
id, user_id (FK), status (pending/confirmed/processing/shipped/delivered/cancelled/refunded), total_cents, tax_cents, shipping_cents, stripe_payment_intent_id, shipping_address (JSONB), tracking_number, placed_at

### OrderItem
id, order_id (FK), product_id (FK), quantity, unit_price_cents

## 5. API Contract (abbreviated)

### Products
- GET /api/products — List with search, filter, pagination
- GET /api/products/:slug — Single product
- POST /api/products — Admin: create
- PATCH /api/products/:id — Admin: update
- POST /api/products/:id/inventory — Admin: adjust stock

### Cart
- GET /api/cart — Get current cart
- POST /api/cart/items — Add item
- PATCH /api/cart/items/:id — Update quantity
- DELETE /api/cart/items/:id — Remove item

### Checkout
- POST /api/checkout — Create order from cart
- POST /api/checkout/:id/pay — Confirm payment
- GET /api/orders — List user orders
- GET /api/orders/:id — Order detail

## 6. Validation

Scalability: PASS (5/6) — S6: long-running report generation not yet async
Security: PASS (5/6) — SEC6: rate limiting on checkout not specified
Maintainability: PASS (6/6)
Performance: PASS (4/4)
Consistency: PASS (3/3)

**Result: PASS WITH WARNINGS — Resolve SEC6 before production launch.**
