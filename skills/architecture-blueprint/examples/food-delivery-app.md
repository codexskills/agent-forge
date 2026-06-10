# Example: Food Delivery App

## User Request
"Build me a food delivery app like Swiggy/Zomato"

## Phase 0 — Feasibility
- Complexity: High (real-time tracking, payments, multiple user types)
- Effort: 2-3 months for MVP
- Risks: Payment integration, real-time logistics, scaling

## Phase 1 — Requirements
- Functional: User auth, restaurant listing, menu browsing, ordering, payment, tracking, reviews
- Non-functional: < 2s load time, 99.9% uptime, support 10K concurrent users
- Assumptions: User has location services, restaurants have tablets for order management
- Missing: Delivery partner app, admin dashboard, refund flow

## Phase 2 — Architecture
- Pattern: Event-driven microservices
- Services: User, Restaurant, Order, Payment, Delivery, Notification
- Database: PostgreSQL (orders), MongoDB (catalog), Redis (cache)
- Queue: RabbitMQ for async events
- Storage: S3 for images
- Frontend: React Native (customer), React (admin), React Native (delivery)

## Phase 3 — Specification
- Auth: JWT + OTP for customers, email/password for restaurants
- APIs: REST for CRUD, WebSocket for real-time tracking
- Data Models: User, Restaurant, MenuItem, Order, Payment, Delivery, Review

## Phase 4 — Roadmap
- M1 (Week 1-4): Auth, restaurant listing, menu, basic ordering
- M2 (Week 5-8): Payments, order tracking, notifications
- M3 (Week 9-10): Reviews, ratings, admin dashboard
- M4 (Week 11-12): Scaling, performance, production hardening

## Phase 5 — Validation
- Scalability: Pass (horizontal scaling via microservices)
- Security: Pass (JWT, HTTPS, payment tokenization)
- Maintainability: Pass (clear service boundaries, shared libs)
- Performance: Pass (caching, CDN, DB indexing)
