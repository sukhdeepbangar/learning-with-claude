# System Design Curriculum

Prepared for FAANG interview preparation. Topics validated against current (2025-2026) interview expectations and popular resources.

**Goal:** Build system design skills from foundations to interview-ready.

**Approach:** Each topic covered through discussion sessions, with practice designs as we progress.

---

## Phase 1: Foundations ✓

### Core Concepts
- [x] Scaling: vertical vs horizontal
- [x] Latency vs throughput
- [x] Availability, reliability, fault tolerance
- [x] SLIs, SLOs, SLAs (the nines)
- [x] CAP theorem
- [x] PACELC theorem
- [x] Consistency models (strong, eventual, causal)

### Estimation
- [x] Latency numbers everyone should know
- [x] Traffic estimation (DAU → QPS → peak)
- [x] Storage and bandwidth estimation
- [x] Back-of-envelope practice

### Interview Framework
- [x] The 7-step approach:
  1. Requirements clarification
  2. Back-of-envelope estimation
  3. System interface definition (API)
  4. Data model definition
  5. High-level design
  6. Detailed design (deep dives)
  7. Identifying and resolving bottlenecks

---

## Phase 2: Building Blocks

### Load Balancing ✓
- [x] L4 vs L7 load balancers
- [x] Algorithms (round-robin, least connections, IP hash, consistent hashing)
- [x] Health checks and failover
- [x] Active-passive vs active-active
- [x] Stateless design and session management
- [x] SSL termination
- [x] DNS-based load balancing (overview)

### Caching
- [ ] Cache levels (browser, CDN, application, database)
- [ ] Strategies (cache-aside, read-through, write-through, write-behind, refresh-ahead)
- [ ] Eviction policies (LRU, LFU, TTL)
- [ ] Cache invalidation
- [ ] Distributed cache (Redis, Memcached)

### Databases — SQL
- [ ] ACID properties
- [ ] Indexing (B-trees, how indexes work, tradeoffs)
- [ ] Replication (primary-replica, sync vs async)
- [ ] Federation
- [ ] Sharding (partitioning strategies, shard keys, rebalancing)
- [ ] Denormalization
- [ ] SQL tuning basics

### Databases — NoSQL & Specialized
- [ ] NoSQL types (key-value, document, column-family, graph)
- [ ] When SQL vs NoSQL (decision framework)
- [ ] Blob/object storage (S3)
- [ ] Search engines (Elasticsearch, inverted indexes)
- [ ] Time-series databases

### Async Processing & Messaging
- [ ] Message queues vs task queues
- [ ] Kafka, RabbitMQ, SQS — when to use each
- [ ] Pub/sub pattern
- [ ] Event-driven architecture
- [ ] Back pressure

### Real-time Communication
- [ ] Long polling
- [ ] Server-sent events (SSE)
- [ ] WebSockets

### Networking & APIs
- [ ] DNS and DNS-based load balancing
- [ ] CDNs (push vs pull)
- [ ] Reverse proxy vs load balancer
- [ ] API design (REST vs RPC vs GraphQL)
- [ ] Rate limiting (token bucket, leaky bucket, sliding window)
- [ ] Communication protocols (TCP, UDP basics)

---

## Phase 3: Distributed Systems Concepts

### Core Algorithms & Patterns
- [ ] Consistent hashing
- [ ] Bloom filters
- [ ] Merkle trees
- [ ] Gossip protocol
- [ ] Heartbeat mechanisms
- [ ] Read repair
- [ ] Quorum consensus

### Reliability Patterns
- [ ] Leader election
- [ ] Distributed consensus (Paxos, Raft — conceptual)
- [ ] Circuit breaker
- [ ] Failover patterns
- [ ] Idempotency

### Data Patterns
- [ ] Sharding strategies
- [ ] Replication strategies
- [ ] Eventual consistency patterns
- [ ] MapReduce (conceptual)
- [ ] Batch vs stream processing

### Security Basics
- [ ] Authentication vs authorization
- [ ] OAuth, JWT basics
- [ ] HTTPS, TLS
- [ ] Rate limiting as defense

---

## Phase 4: Design Practice

### Starter Designs
- [ ] URL Shortener / Pastebin
- [ ] Rate Limiter
- [ ] Unique ID Generator

### Feed & Social
- [ ] Twitter / News Feed (fan-out problem)
- [ ] Instagram / Photo Sharing
- [ ] Notification System

### Real-time & Communication
- [ ] Chat System (WhatsApp/Messenger)
- [ ] Collaborative Editing (Google Docs)
- [ ] Typeahead / Autocomplete

### Media & Streaming
- [ ] YouTube / Video Platform
- [ ] Netflix / Streaming Service

### Location & Matching
- [ ] Uber / Ride Sharing
- [ ] Nearby Friends / Proximity Service

### Search & Infrastructure
- [ ] Web Crawler
- [ ] Distributed Cache (design Redis)
- [ ] Distributed Message Queue
- [ ] Key-Value Store
- [ ] Ticketing System (Ticketmaster — seat booking)

---

## Phase 5: Interview Readiness

### Structured Practice
- [ ] Full 45-minute mock designs
- [ ] Micro-designs (15-20 minute sprints)
- [ ] Practicing the 7-step framework

### Communication Skills
- [ ] Thinking aloud
- [ ] Handling ambiguity
- [ ] Taking and using hints
- [ ] Articulating tradeoffs

### Product Sense
- [ ] Connecting design choices to user needs
- [ ] Discussing business implications
- [ ] Prioritization under constraints

---

## Resources

Request these as needed during sessions:

| Resource | Best For |
|----------|----------|
| [System Design Primer (GitHub)](https://github.com/donnemartin/system-design-primer) | Free comprehensive roadmap |
| [ByteByteGo](https://bytebytego.com/) | Visual explanations |
| [Grokking System Design](https://www.designgurus.io/) | Structured framework |
| [Designing Data-Intensive Applications](https://dataintensive.net/) | Deep theory |
| [Exponent](https://www.tryexponent.com/) | Mock interviews |

---

## Progress Notes

| Date | Phase | Topics Covered | Notes |
|------|-------|----------------|-------|
| 2026-01-28 | Phase 1 | All foundations | Core concepts, estimation, 7-step framework |
| 2026-02-05 | Phase 2 | Load Balancing | Algorithms, L4/L7, health checks, HA patterns |

**Notes:**
- [phase-1-foundations-notes.md](phase-1-foundations-notes.md)
- [phase-2-load-balancing-notes.md](phase-2-load-balancing-notes.md)
