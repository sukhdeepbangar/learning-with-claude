# System Design Curriculum

**Goal:** Interview-ready system design skills in 4-6 months.

**Approach:** Three integrated tracks per topic:
1. **DDIA** — Deep understanding of *why* things work the way they do
2. **Alex Xu (Vol 1 & 2)** — Interview-style patterns and designs
3. **AWS** — Real-world service knowledge to ground your designs

**Books:**
- *Designing Data-Intensive Applications* (Martin Kleppmann)
- *System Design Interview Vol 1* (Alex Xu)
- *System Design Interview Vol 2* (Alex Xu)

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
- [x] The 7-step approach

---

## Phase 2: Building Blocks — Load Balancing & Observability

### Load Balancing
- [x] L4 vs L7 load balancers
- [x] Algorithms (round-robin, least connections, IP hash, consistent hashing)
- [x] Health checks and failover
- [x] Active-passive vs active-active
- [x] Stateless design and session management
- [x] SSL termination
- [x] DNS-based load balancing (overview)

### Observability
- [ ] Logging: structured logs, centralized aggregation
- [ ] Metrics: RED method (Rate/Errors/Duration), USE method (Utilization/Saturation/Errors)
- [ ] Distributed tracing basics
- [ ] Alerting and on-call basics
- [ ] What interviewers want to hear: "how would you know if this is broken?"

### AWS Services
- [ ] CloudWatch — metrics, logs, alarms
- [ ] X-Ray — distributed tracing

### Practice Design: Warmup
- [ ] Design Pastebin — minimal version (single region, single DB, LB + app servers). Goal: produce an end-to-end sketch now, so every later phase has something concrete to deepen. You will hit the walls this design has — that's the point. It motivates Phase 3.

---

## Phase 3: Storage Foundations

Deep theory before touching specific systems.

### Data Models & Query Languages — DDIA Ch 2
- [ ] Relational vs document vs graph models
- [ ] Schema-on-read vs schema-on-write
- [ ] When to use what (decision framework)

**Decision: which data model?**

| Need | Pick | Why |
|------|------|-----|
| Strong relationships, joins, transactions | Relational | SQL + ACID, mature ecosystem |
| Flexible/nested schema, one-aggregate reads | Document | Schema-on-read, locality |
| Many-to-many, traversal-heavy (social, knowledge graphs) | Graph | Edges are first-class |
| Simple lookup by known key, huge scale | Key-value | O(1), trivial to shard |

### Storage Engines — DDIA Ch 3
- [ ] Log-structured (LSM trees, SSTables)
- [ ] Page-oriented (B-trees)
- [ ] How indexes work, tradeoffs
- [ ] Column-oriented storage (analytics use case)

### SQL Fundamentals
- [ ] ACID properties (basics — deep dive in Phase 7)
- [ ] Indexing strategies and query optimization
- [ ] Denormalization — when and why

---

## Phase 4: Databases & Storage Systems

Now apply the theory to real systems.

**Decision: which storage system?**

| Use case | Pick | Why |
|----------|------|-----|
| Predictable access by key, huge scale | DynamoDB / Redis | O(1) lookup, horizontal scale |
| Write-heavy, linear scale, tunable consistency | Cassandra | LSM, multi-leader |
| Full-text / faceted search | Elasticsearch / OpenSearch | Inverted indexes |
| Flexible schema, rich queries on nested data | MongoDB | Document model |
| Time-series (metrics, sensor data) | TimescaleDB / InfluxDB | Time-partitioned, compression |
| Large blobs, static assets | S3 | Cheap, durable, infinite |
| Relational + transactions + moderate scale | RDS / Aurora | SQL + ACID, managed |

### NoSQL & Specialized Storage
- [ ] Key-value (DynamoDB, Redis)
- [ ] Document (MongoDB)
- [ ] Column-family (Cassandra)
- [ ] Search engines (Elasticsearch, inverted indexes)
- [ ] Time-series databases
- [ ] Blob/object storage

### AWS Services
- [ ] RDS & Aurora — managed relational, why Aurora exists
- [ ] DynamoDB — partition keys, GSIs, capacity modes
- [ ] S3 — storage classes, lifecycle policies
- [ ] ElastiCache — Redis vs Memcached (intro; deep dive in Phase 9)
- [ ] OpenSearch — managed Elasticsearch

### Practice Design: Key-Value Store
- [ ] Design a key-value store (Xu Vol 1 Ch 6)

---

## Phase 5: Encoding, APIs & Networking

### Encoding & Evolution — DDIA Ch 4
- [ ] JSON, XML, binary formats (Protobuf, Avro, Thrift)
- [ ] Schema evolution and compatibility (forward/backward)
- [ ] Dataflow through databases, services, messaging

### Networking & APIs
- [ ] DNS and CDNs (push vs pull)
- [ ] Reverse proxy vs load balancer
- [ ] API design: REST vs RPC vs GraphQL
- [ ] Rate limiting (token bucket, leaky bucket, sliding window)

### Caching Primer
Just enough to use caching in the designs from here on. Deep dive in Phase 9.
- [ ] Where caches live (browser, CDN, app, DB)
- [ ] Cache-aside pattern, TTL basics
- [ ] Cache hit/miss and the latency math

### AWS Services
- [ ] API Gateway — REST/WebSocket APIs, throttling
- [ ] CloudFront — CDN, edge caching
- [ ] Route 53 — DNS, routing policies

### Practice Designs
- [ ] Design a Rate Limiter (Xu Vol 1 Ch 4)
- [ ] Design a URL Shortener (Xu Vol 1 Ch 8)

---

## Phase 6: Replication & Partitioning

### Replication — DDIA Ch 5
- [ ] Leader-based replication (sync vs async)
- [ ] Multi-leader replication
- [ ] Leaderless replication (quorums, read repair, anti-entropy)
- [ ] Replication lag problems (read-after-write, monotonic reads)

### Partitioning (Sharding) — DDIA Ch 6
- [ ] Partitioning strategies (key range, hash)
- [ ] Secondary indexes and partitioning
- [ ] Rebalancing partitions
- [ ] Request routing

### AWS Services
- [ ] RDS Multi-AZ & read replicas
- [ ] DynamoDB Global Tables (multi-region replication)
- [ ] Aurora Global Database

### Practice Designs
- [ ] Design a Unique ID Generator (Xu Vol 1 Ch 7)
- [ ] Design Consistent Hashing (Xu Vol 1 Ch 5)

### Checkpoint
- [ ] Consolidation exercise: design a globally-distributed read-heavy service end-to-end using only Phase 1-6 material. 45 minutes, out loud.

---

## Phase 7: Transactions, Consistency & Consensus

The hardest theory in the curriculum. Take your time here.

### Transactions — DDIA Ch 7
- [ ] ACID in depth (what isolation levels really mean)
- [ ] Read committed, snapshot isolation, serializability
- [ ] Write skew and phantoms
- [ ] Two-phase locking vs SSI

### Trouble with Distributed Systems — DDIA Ch 8
- [ ] Unreliable networks, clocks, process pauses
- [ ] Truth and lies in distributed systems

### Consistency & Consensus — DDIA Ch 9
- [ ] Linearizability vs serializability
- [ ] Ordering guarantees (total order broadcast)
- [ ] Distributed consensus (Raft — conceptual)
- [ ] Leader election
- [ ] Fencing tokens

### AWS Services
- [ ] SQS FIFO — exactly-once processing

---

## Phase 8: Reliability Patterns & Security

### Reliability Patterns
- [ ] Circuit breaker
- [ ] Idempotency
- [ ] Failover patterns
- [ ] Saga pattern (distributed transactions)

### Security
- [ ] Auth: authentication vs authorization, OAuth/OIDC, JWT basics
- [ ] Encryption at rest and in transit (TLS)
- [ ] DDoS mitigation and WAF concepts
- [ ] Secrets management

### AWS Services
- [ ] Step Functions — workflow orchestration, saga pattern
- [ ] IAM, Cognito — auth
- [ ] KMS — key management
- [ ] WAF, Shield — edge protection

### Practice Design: Real-World
- [ ] Design a Payment System (Xu Vol 2 Ch 12) — exercises Phase 7 + 8 together
- [ ] Design a Ticketing System (seat booking, concurrency)

---

## Phase 9: Caching & Real-time Communication

### Caching Deep Dive
- [ ] Cache levels revisited (browser, CDN, application, database)
- [ ] Strategies (cache-aside, read-through, write-through, write-behind)
- [ ] Eviction policies (LRU, LFU, TTL)
- [ ] Cache invalidation — the hard problem
- [ ] Distributed cache architecture

**Decision: which caching strategy?**

| Scenario | Strategy | Tradeoff |
|----------|----------|----------|
| Read-heavy, tolerate stale data | Cache-aside | Simple; app handles misses and invalidation |
| Read-heavy, want consistency | Read-through | Cache owns load logic; cold-start penalty |
| Write-heavy, consistency matters | Write-through | Slow writes, never stale reads |
| Write-heavy, throughput matters | Write-behind | Fast writes, data-loss risk on cache crash |

### Real-time Communication
- [ ] Long polling
- [ ] Server-sent events (SSE)
- [ ] WebSockets

### AWS Services
- [ ] ElastiCache deep dive — cluster mode, replication
- [ ] CloudFront — caching behaviors, invalidation
- [ ] AppSync / API Gateway WebSockets

### Practice Designs
- [ ] Design a Chat System (Xu Vol 1 Ch 12)
- [ ] Design a Notification System (Xu Vol 1 Ch 10)

---

## Phase 10: Async Processing & Streaming

### Batch Processing — DDIA Ch 10
- [ ] MapReduce and dataflow
- [ ] Beyond MapReduce (Spark-style dataflows)

### Stream Processing — DDIA Ch 11
- [ ] Event sourcing and change data capture
- [ ] Stream processing frameworks
- [ ] Joins in stream processing
- [ ] Fault tolerance in streaming

### Message Queues & Event-Driven Architecture
- [ ] Message queues vs event streams
- [ ] Pub/sub pattern
- [ ] Back pressure
- [ ] Event-driven architecture

**Decision: queue vs stream vs pub/sub?**

| Need | Pick (AWS) | Why |
|------|-----------|-----|
| One consumer, at-least-once delivery | SQS | Simple managed queue |
| Strict ordering, dedup | SQS FIFO | Message groups + dedup IDs |
| Many independent subscribers (fan-out) | SNS | Pub/sub topic |
| Replayable, ordered stream (event sourcing, analytics) | Kinesis | Log-based, retention window |
| Event routing by content-based rules | EventBridge | Filter + route to multiple targets |

### AWS Services
- [ ] SQS & SNS — queues vs pub/sub
- [ ] Kinesis — real-time streaming
- [ ] EventBridge — event bus
- [ ] Lambda — event-driven compute

### Practice Designs
- [ ] Design a News Feed (Xu Vol 1 Ch 11 — fan-out problem)
- [ ] Design a Web Crawler (Xu Vol 1 Ch 9)

### Checkpoint
- [ ] Consolidation exercise: design a write-heavy event-driven system end-to-end using only Phase 1-10 material. 45 minutes, out loud.

---

## Phase 11: Full System Designs

Apply everything. Each design practiced in 45-minute interview format.

> Note: Some designs below overlap with earlier Practice Designs. Those are now **timed full-length mocks under interview pressure**, not re-learning. The goal is execution speed and communication, not new material.

### Media & Content
- [ ] Design YouTube (Xu Vol 1 Ch 14)
- [ ] Design Google Drive (Xu Vol 1 Ch 15)

### Location & Matching
- [ ] Design a Proximity Service (Xu Vol 2 Ch 1)
- [ ] Design Uber / Ride Sharing

### Social & Feed
- [ ] Design Instagram / Photo Sharing
- [ ] Design Typeahead / Autocomplete (Xu Vol 1 Ch 13)

### Infrastructure
- [ ] Design a Distributed Cache
- [ ] Design a Distributed Message Queue (Xu Vol 2 Ch 4)
- [ ] Design a Stock Exchange (Xu Vol 2 Ch 7)

### AWS Architecture Patterns
- [ ] Multi-AZ and multi-region design
- [ ] Serverless patterns (API Gateway + Lambda + DynamoDB)
- [ ] Event-driven architecture (SNS + SQS + Lambda)

---

## Phase 12: Interview Readiness

### Structured Practice
- [ ] Full 45-minute mock designs (at least 5)
- [ ] Micro-designs: 15-20 minute sprints
- [ ] Practicing the 7-step framework under time pressure

### Communication Skills
- [ ] Thinking aloud
- [ ] Handling ambiguity
- [ ] Taking and using hints
- [ ] Articulating tradeoffs with AWS service knowledge

### Product Sense
- [ ] Connecting design choices to user needs
- [ ] Discussing business implications
- [ ] Prioritization under constraints

### AWS Fluency Check
- [ ] Can name the right AWS service for any building block
- [ ] Understand key limits and tradeoffs of core services
- [ ] Can sketch an AWS architecture diagram for any design

---

## Core AWS Services Cheat Sheet

Learn these as you encounter them — not all at once.

| Category | Services | When You'll Learn |
|----------|----------|-------------------|
| **Compute** | EC2, ECS/EKS, Lambda | Throughout |
| **Database** | RDS, Aurora, DynamoDB | Phase 3-4 |
| **Cache** | ElastiCache (Redis/Memcached) | Phase 4 intro, Phase 9 deep |
| **Storage** | S3 | Phase 4 |
| **Messaging** | SQS, SNS, Kinesis, EventBridge | Phase 10 |
| **Networking** | Route 53, CloudFront, API Gateway, ELB | Phase 5 |
| **Auth & Security** | IAM, Cognito, KMS, WAF | Phase 8 |
| **Orchestration** | Step Functions | Phase 8 |
| **Search** | OpenSearch | Phase 4 |
| **Observability** | CloudWatch, X-Ray | Phase 2 |

---

## Resources

| Resource | Best For |
|----------|----------|
| DDIA (Kleppmann) | Deep theory — the *why* |
| Alex Xu Vol 1 | Core designs + building blocks |
| Alex Xu Vol 2 | Advanced designs (proximity, payment, stock exchange) |
| AWS Free Tier | Hands-on with real services |
| [System Design Primer (GitHub)](https://github.com/donnemartin/system-design-primer) | Free supplementary reference |
| [ByteByteGo](https://bytebytego.com/) | Visual explanations |

---

## Progress Notes

| Date | Phase | Topics Covered | Notes |
|------|-------|----------------|-------|
| 2026-01-28 | Phase 1 | All foundations | Core concepts, estimation, 7-step framework |
| 2026-02-05 | Phase 2 | Load Balancing | Algorithms, L4/L7, health checks, HA patterns. Observability pending. |

**Notes:**
- [phase-1-foundations-notes.md](phase-1-foundations-notes.md)
- [phase-2-load-balancing-notes.md](phase-2-load-balancing-notes.md)
