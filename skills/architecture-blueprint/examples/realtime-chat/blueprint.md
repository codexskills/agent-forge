# Real-Time Chat — Architecture Blueprint

## 1. Project Overview
A real-time group chat application supporting multiple rooms, typing indicators, message history, file/image sharing, and online presence indicators.

## 2. Feasibility Assessment
**Complexity:** Moderate
**Effort:** 5-8 weeks (2-person team)
**Verdict:** PROCEED

**Top Risks:**
1. WebSocket scaling — sticky sessions or external pub/sub
2. Message ordering — clock skew on distributed servers
3. File upload abuse — content scanning, size limits

## 3. Architecture

### Pattern: Modular Monolith with WebSocket server

### Stack
| Layer | Technology |
|---|---|
| WebSocket Server | Socket.io + Node.js |
| HTTP API | Same Node.js process (Express) |
| Database | PostgreSQL (messages, users, rooms) |
| Real-time State | Redis (presence, typing indicators) |
| Pub/Sub | Redis adapter for Socket.io |
| File Storage | Cloudflare R2 (images, files) |
| Auth | JWT short-lived tokens |
| Hosting | Railway (WebSocket support) |

## 4. Data Model

### Room
id, name, type (public/private/dm), created_by (FK), created_at, archived_at

### RoomMember
room_id (FK), user_id (FK), joined_at, last_read_at
Unique: (room_id, user_id)

### Message
id, room_id (FK), user_id (FK), type (text/image/file/system), content (text or file URL), replied_to_id (nullable FK), created_at
Index: (room_id, created_at DESC)

## 5. API + WebSocket Contract

### REST Endpoints
- POST /api/rooms — Create room
- GET /api/rooms — List user's rooms
- POST /api/rooms/:id/members — Invite user
- GET /api/rooms/:id/messages?before=X&limit=50 — Message history (cursor pagination)

### WebSocket Events (Socket.io)

Client → Server:
- chat:join { roomId } — Join room
- chat:leave { roomId } — Leave room
- chat:message { roomId, content, type, replyTo } — Send message
- chat:typing { roomId, isTyping } — Typing indicator

Server → Client:
- chat:message { message } — New message broadcast to room
- chat:presence { userId, status } — Online/offline update
- chat:typing { userId, roomId, isTyping } — Typing indicator
- chat:joined { user } — User joined notification
- chat:left { user } — User left notification

## 6. Key Design Decisions

**Message Ordering:** Server-assigned sequential message IDs per room. Clients sort by message ID, not timestamp (handles clock skew).

**History Loading:** Cursor-based pagination with `before=<messageId>`. Infinite scroll in client.

**Presence:** Redis key per user with TTL (30s heartbeat). On disconnect, wait 10s before marking offline (handles brief reconnects).

**File Sharing:** Upload via presigned R2 URL. Image thumbnails generated server-side. Malware scanning via ClamAV on upload.

## 7. Validation

Result: PASS — Safe to begin implementation. WebSocket rate limiting documented for Milestone 3.
