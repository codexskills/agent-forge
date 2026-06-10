# Social Mobile Backend — Architecture Blueprint

## 1. Project Overview
Backend API for a social mobile app — user profiles, posts with images, follow relationships, feed generation, push notifications. Mobile frontend (iOS/Android) out of scope.

## 2. Feasibility Assessment
**Complexity:** Moderate
**Effort:** 4-6 weeks (2-person team)
**Verdict:** PROCEED

## 3. Architecture

### Pattern: Modular Monolith

### Stack
| Layer | Technology |
|---|---|
| Runtime | Node.js + Express |
| Database | PostgreSQL |
| Cache | Redis (feed cache, session cache) |
| File Storage | Cloudflare R2 (images) |
| Image Processing | Sharp (on upload resize) |
| Push Notifications | Firebase Cloud Messaging |
| Auth | Firebase Auth (phone/email) |
| Hosting | Railway |

## 4. Data Model

### User
id, firebase_uid, username (unique), display_name, bio, avatar_url, follower_count, following_count, post_count, created_at

### Post
id, user_id (FK), text_content, images (JSONB array of URLs), like_count, comment_count, created_at, updated_at

### Follow
follower_id (FK → user), following_id (FK → user), created_at
Unique: (follower_id, following_id)

### Like
user_id (FK), post_id (FK), created_at
Unique: (user_id, post_id)

### Comment
id, user_id (FK), post_id (FK), parent_comment_id (nullable, FK → self), text, created_at

## 5. API Contract (abbreviated)

### Feed
- GET /api/feed — Paginated feed of followed users' posts (cursor-based)

### Posts
- POST /api/posts — Create post with images (multipart)
- GET /api/posts/:id — Single post with comments
- DELETE /api/posts/:id — Delete own post

### Social
- POST /api/users/:id/follow — Follow user
- DELETE /api/users/:id/follow — Unfollow
- GET /api/users/:id/followers — Follower list
- GET /api/users/:id/following — Following list

### Notifications
- GET /api/notifications — Paginated notification list
- PATCH /api/notifications/:id/read — Mark as read

## 6. Key Design Decisions

**Feed Generation:** Pull-based (read-time merge of followed users' posts). Redis cache of followed user IDs per user. Cache feed results for 30 seconds.

**Image Upload:** Direct to presigned R2 URL. Server validates type/dimensions post-upload. Thumbnails generated server-side via Sharp.

**Push Notifications:** FCM for delivery. Notification content generated server-side and queued via BullMQ.

## 7. Validation

Result: PASS — Safe to begin implementation.
