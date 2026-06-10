# Performance Checklist

## Core Web Vitals Targets

| Metric | Good | Needs Improvement | Poor |
|--------|------|-------------------|------|
| LCP (Largest Contentful Paint) | ≤ 2.5s | 2.5s - 4.0s | > 4.0s |
| FID (First Input Delay) | ≤ 100ms | 100ms - 300ms | > 300ms |
| CLS (Cumulative Layout Shift) | ≤ 0.1 | 0.1 - 0.25 | > 0.25 |
| INP (Interaction to Next Paint) | ≤ 200ms | 200ms - 500ms | > 500ms |
| TTFB (Time to First Byte) | ≤ 800ms | 800ms - 1800ms | > 1800ms |
| FCP (First Contentful Paint) | ≤ 1.8s | 1.8s - 3.0s | > 3.0s |

## Frontend Performance Checklist

### Loading Performance

#### Critical Rendering Path
- [ ] Critical CSS inlined in `<head>`
- [ ] Non-critical CSS deferred (media="print" then swap)
- [ ] Render-blocking resources eliminated (defer JS, inline CSS)
- [ ] Preload key resources (`<link rel="preload">`)
- [ ] Preconnect to third-party origins (`<link rel="preconnect">`)
- [ ] Font-display: swap for web fonts
- [ ] Lazy-load below-the-fold images (`loading="lazy"`)
- [ ] Server-side rendering or static generation for initial content

#### JavaScript
- [ ] Code splitting (route-based, component-based)
- [ ] Tree shaking enabled (dead code elimination)
- [ ] Minified and compressed (Brotli > Gzip)
- [ ] Async/defer for non-critical scripts
- [ ] Bundle size budgets enforced
- [ ] No render-blocking JS in critical path
- [ ] Dynamic imports for heavy components

#### Images
- [ ] WebP/AVIF format used (with JPEG/PNG fallback)
- [ ] Responsive images (`srcset`, `sizes`)
- [ ] Image CDN used for resizing/optimization
- [ ] Lazy loading for below-fold images
- [ ] Proper image dimensions set (prevent CLS)
- [ ] `<picture>` element for art direction

#### Caching
- [ ] Service worker for offline support and caching
- [ ] Cache-first strategy for static assets
- [ ] Network-first for API responses
- [ ] Long cache headers for versioned assets (1 year)
- [ ] ETags for unversioned resources

### Runtime Performance

#### Rendering
- [ ] No layout thrashing (batch DOM reads/writes)
- [ ] Will-change property used intentionally (not on everything)
- [ ] Animations use GPU-accelerated properties (transform, opacity)
- [ ] Avoid `requestAnimationFrame` for non-visual updates
- [ ] Virtual scrolling for long lists (react-window, tanstack-virtual)
- [ ] Debounce/throttle scroll and resize handlers
- [ ] Passive event listeners for scroll/touch events

#### State Management
- [ ] Component state as local as possible
- [ ] Memoization for expensive computations (useMemo, useCallback)
- [ ] Context API splitting (separate contexts for different concerns)
- [ ] Avoid unnecessary re-renders
- [ ] Normalized data in stores (avoid deeply nested objects)

#### Network
- [ ] API responses paginated
- [ ] GraphQL for over-fetching prevention (or partial responses)
- [ ] API request deduplication
- [ ] Optimistic updates for better UX
- [ ] Prefetching for likely user actions
- [ ] HTTP/2 or HTTP/3 enabled

## Backend Performance Checklist

### API Performance
- [ ] Response compression enabled (Brotli)
- [ ] Connection pooling for database
- [ ] Database queries indexed (check EXPLAIN ANALYZE)
- [ ] N+1 queries eliminated (use eager loading, batching)
- [ ] Caching layer (Redis, Memcached) for frequent queries
- [ ] Rate limiting to prevent abuse
- [ ] Pagination for list endpoints
- [ ] Timeouts configured for external calls
- [ ] Circuit breaker for failing dependencies
- [ ] Request coalescing for duplicate concurrent requests

### Database Performance
- [ ] Slow query log enabled (threshold: 100ms)
- [ ] Indexes on WHERE, JOIN, ORDER BY columns
- [ ] Composite indexes for multi-column queries
- [ ] No table scans on large tables (>10k rows)
- [ ] Query plan reviewed for hot paths
- [ ] Read replicas for read-heavy workloads
- [ ] Connection pooling configured
- [ ] Database connection limits set
- [ ] Vacuum/optimize on regular schedule

### Caching Strategy
```
Layer 1: Browser Cache (CDN)
  - Static assets: immutable, 1 year
  - HTML: short TTL (5 min) or ETag

Layer 2: CDN Cache
  - API responses: vary by user, short TTL
  - Public data: long TTL, stale-while-revalidate

Layer 3: Application Cache (Redis)
  - Session data
  - Frequent queries (user profiles, configs)
  - Computed values (aggregations, recommendations)

Layer 4: Database Cache
  - Query cache (if supported)
  - Materialized views for complex queries
```

### Asynchronous Processing
- [ ] Heavy tasks offloaded to queue (Bull, RabbitMQ, SQS)
- [ ] Email, notifications, report generation async
- [ ] Image/video processing async
- [ ] Queue monitoring and alerting
- [ ] Dead letter queue for failed messages

## Performance Measurement

### Tools
```bash
# Lighthouse CI (automated)
npx lighthouse https://example.com --view

# WebPageTest
# https://www.webpagetest.org/

# Bundle analysis
npx vite-bundle-analyzer  # Vite
npx source-map-explorer dist/*.js  # Webpack

# API benchmarking
npx autocannon http://localhost:3000/api/users
npx k6 run script.js

# Database profiling
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'test@example.com';

# Node.js profiling
node --cpu-prof --heap-prof server.js
```

### Budgets (example)
```json
{
  "budgets": [
    {
      "resourceType": "script",
      "budget": 150
    },
    {
      "resourceType": "total",
      "budget": 400
    },
    {
      "resourceType": "image",
      "budget": 200
    },
    {
      "timing": {
        "metric": "interactive",
        "budget": 5000
      }
    },
    {
      "timing": {
        "metric": "first-meaningful-paint",
        "budget": 2500
      }
    }
  ]
}
```

## Performance Budget Template

```markdown
## Performance Budget

### Size Budgets
| Resource | Budget | Current | Status |
|----------|--------|---------|--------|
| Total JS | < 300 KB | 245 KB | ✅ |
| Total CSS | < 50 KB | 32 KB | ✅ |
| Total Images | < 500 KB | 420 KB | ✅ |
| Total Page | < 1 MB | 700 KB | ✅ |

### Timing Budgets
| Metric | Budget | Current | Status |
|--------|--------|---------|--------|
| TTFB | < 800ms | 320ms | ✅ |
| FCP | < 1.8s | 1.2s | ✅ |
| LCP | < 2.5s | 1.8s | ✅ |
| TBT | < 200ms | 95ms | ✅ |
| CLS | < 0.1 | 0.02 | ✅ |

### API Response Times
| Endpoint | P50 | P95 | Budget |
|----------|-----|-----|--------|
| GET /api/users | 45ms | 120ms | < 200ms |
| POST /api/orders | 120ms | 350ms | < 500ms |
| GET /api/search | 80ms | 250ms | < 300ms |
```

## Common Performance Issues

| Issue | Symptom | Fix |
|-------|---------|-----|
| Unoptimized images | Large page weight | Use WebP, responsive images, CDN |
| Render-blocking JS | Slow FCP | Defer non-critical scripts |
| No code splitting | Large bundles | Route-based code splitting |
| Missing cache headers | Repeated downloads | Set Cache-Control, ETag |
| N+1 queries | Slow API responses | Eager load, batch, dataloader |
| Memory leaks | Increasing memory over time | Fix forgotten listeners, closures |
| Layout thrashing | Janky scrolling | Batch DOM reads/writes |
| Too many re-renders | Slow React | Memoization, state optimization |
| Missing compression | Large transfers | Enable Brotli/Gzip |
| No CDN | High latency everywhere | Add CDN for static assets |

## Profiling Commands

```bash
# Node.js
node --inspect-brk server.js                    # Chrome DevTools profiling
node --cpu-prof --cpu-prof-dir=./profile server.js
node --heap-prof --heap-prof-dir=./profile server.js
clinic doctor -- node server.js                  # Node clinic
clinic flame -- node server.js                   # Flame graphs
clinic heapprofiler -- node server.js            # Heap profiling

# React
# React DevTools Profiler
# Why Did You Render? library

# Browser
# Chrome DevTools Performance tab
# Chrome DevTools Lighthouse tab
# Chrome DevTools Coverage tab

# Database
EXPLAIN ANALYZE <query>;
# pg_stat_statements (PostgreSQL)
# Performance Insights (AWS RDS)
```

## Usage
Reference this checklist when performance tuning, before deploying performance-sensitive changes, and during performance reviews. Run Lighthouse CI in CI to enforce budgets automatically.
