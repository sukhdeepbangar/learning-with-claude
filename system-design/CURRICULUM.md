# System Design Curriculum

Prepared for FAANG interview preparation. Topics validated against current (2025-2026) interview expectations and popular resources.

**Goal:** Build system design skills from foundations to interview-ready.

**Approach:** Each topic covered through discussion sessions, with practice designs as we progress.

---

## Phase 1: Foundations

### Core Concepts
- [ ] Scaling: vertical vs horizontal
- [ ] Latency vs throughput
- [ ] Availability, reliability, fault tolerance
- [ ] SLIs, SLOs, SLAs (the nines)
- [ ] CAP theorem
- [ ] PACELC theorem
- [ ] Consistency models (strong, eventual, causal)

### Estimation
- [ ] Latency numbers everyone should know
- [ ] Traffic estimation (DAU → QPS → peak)
- [ ] Storage and bandwidth estimation
- [ ] Back-of-envelope practice

### Interview Framework
- [ ] The 7-step approach:
  1. Requirements clarification
  2. Back-of-envelope estimation
  3. System interface definition (API)
  4. Data model definition
  5. High-level design
  6. Detailed design (deep dives)
  7. Identifying and resolving bottlenecks

---

## Phase 2: Building Blocks

### Load Balancing
- [ ] L4 vs L7 load balancers
- [ ] Algorithms (round-robin, least connections, IP hash, consistent hashing)
- [ ] Health checks and failover
- [ ] Active-passive vs active-active
- [ ] Stateless design and session management

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

*Session notes and observations will be added here as we progress.*
