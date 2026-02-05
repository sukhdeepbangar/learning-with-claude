# Phase 1: Foundations — Notes

Quick reference for system design fundamentals.

---

## Core Concepts

### Scaling

| Type | What it means | Example |
|------|---------------|---------|
| **Vertical** | Bigger machine | 10GB RAM → 20GB RAM |
| **Horizontal** | More machines | 1 server → 2 servers with 10GB each |

Vertical has limits (hardware ceiling). Horizontal scales further but adds complexity (distributed systems).

---

### CAP Theorem

In a distributed data store, when a **network partition** occurs, you must choose between:

- **C**onsistency — Every read gets the most recent write
- **A**vailability — Every request gets a response (not an error)
- **P**artition tolerance — System works despite network failures between nodes

**Key points:**
- Partition tolerance isn't optional — network failures *will* happen
- You're really choosing between **CP** (reject requests to stay consistent) or **AP** (serve requests but allow stale reads)
- CAP is about *data* in distributed systems — what happens when nodes holding your data can't communicate

**CA "doesn't exist"** in distributed systems. If you're distributed, partitions can happen.

---

### PACELC Theorem

Extends CAP to cover normal operation (not just during partitions):

```
Partition → choose A or C
Else      → choose L (latency) or C (consistency)
```

Even when everything's fine, replicating data to stay consistent adds latency. You're always trading off.

---

### Latency vs Throughput

| Term | Definition | Analogy (highway) |
|------|------------|-------------------|
| **Latency** | Time between request and response | How long one car takes A → B |
| **Throughput** | Requests handled per unit time | Cars passing per hour |

**Percentiles matter for latency:**
- **p50 (median)** — Half of requests faster than this
- **p99** — 99% of requests faster than this
- **p999** — 99.9% faster than this

Your p50 might be 50ms but p99 might be 2 seconds. In interviews, usually target p99.

**Relationship:**
- Batching ↑ throughput but ↑ latency (items wait for batch)
- More servers can improve both
- Caching improves both

---

### Availability, Reliability, Fault Tolerance

| Term | Question it answers | Measurement |
|------|---------------------|-------------|
| **Availability** | Is it up? | Percentage of uptime |
| **Reliability** | Does it work correctly? | Success rate, error rate, MTBF |
| **Fault tolerance** | Does it survive failures? | — (it's a capability) |

**The nines:**
- 99.9% (three nines) = ~8.7 hours downtime/year
- 99.99% (four nines) = ~52 minutes downtime/year
- 99.999% (five nines) = ~5 minutes downtime/year

**Fault tolerance** is a mechanism to achieve high availability and reliability (redundancy, replicas, failover).

---

### SLIs, SLOs, SLAs

```
SLI (measure) → SLO (internal target) → SLA (external promise)
```

| Term | What it is | Example |
|------|------------|---------|
| **SLI** (Indicator) | The metric, the fact | "We measured 99.97% availability" |
| **SLO** (Objective) | Internal target | "We target 99.95%" |
| **SLA** (Agreement) | External contract with penalties | "We promise 99.9% or refund" |

SLA is usually looser than SLO — gives you buffer before owing customers money.

---

### Consistency Models

```
Strong ——————— Causal ——————— Eventual
(strictest)                    (loosest)
(slowest)                      (fastest)
```

| Model | Guarantee | Use case |
|-------|-----------|----------|
| **Strong** | Every read sees most recent write. As if one copy. | Banking, inventory |
| **Causal** | If A caused B, everyone sees A before B. Unrelated events can vary. | Social feeds, comments, chat |
| **Eventual** | Nodes may temporarily disagree, but converge over time. | DNS, caches, likes count |

Strong consistency is the CP choice — slower, less available during partitions.

---

## Estimation

### Latency Numbers to Know

| Operation | Latency |
|-----------|---------|
| L1 cache | ~1 ns |
| L2 cache | ~10 ns |
| RAM | ~100 ns |
| SSD random read | ~100 μs (0.1 ms) |
| HDD random read | ~10 ms |
| Same datacenter round trip | ~0.5 ms |
| Cross-continent round trip | ~100-150 ms |

**Key ratios:**
- Memory is ~1000x faster than SSD
- SSD is ~100x faster than HDD

---

### Traffic Estimation (DAU → QPS)

**Formula:**
```
QPS = (DAU × requests per user) / 100,000
Peak QPS = QPS × 2 or 3
```

**Key number:** ~100,000 seconds in a day (actual: 86,400)

**Example:** 200M DAU, 20 reads + 1 write per user
- Read QPS: 200M × 20 / 100K = 40,000 QPS (120K peak)
- Write QPS: 200M × 1 / 100K = 2,000 QPS (6K peak)
- Read:Write ratio = 20:1 (read-heavy → invest in caching, read replicas)

Always separate read/write — they scale differently.

---

### Storage Estimation

**Example:** 5 years of tweets (200M DAU, 1 tweet/day, 250 bytes/tweet)

```
Daily:  200M × 250 bytes = 50 GB/day
Yearly: 50 GB × 365 = ~18 TB/year
5 years: 18 TB × 5 = ~90 TB
With overhead (2x): ~180 TB
```

---

### Bandwidth Estimation

**Bandwidth** = data transferred per unit time (bytes/second)

**Example:** 40,000 read QPS, 250 bytes per response
```
40,000 × 250 = 10 MB/second
Peak: 30 MB/second
```

- **Ingress** = data coming in (uploads, writes)
- **Egress** = data going out (responses, downloads) — usually costs more

---

### Useful Conversions

| Unit | Bytes |
|------|-------|
| 1 KB | 10³ (1,000) |
| 1 MB | 10⁶ (1,000,000) |
| 1 GB | 10⁹ |
| 1 TB | 10¹² |

**Size estimates:**
- 1 character ≈ 1-2 bytes
- 1 image ≈ 200 KB - 1 MB
- 1 minute video ≈ 50-100 MB

---

## Interview Framework

### The 7-Step Approach

| Step | Time | Question to answer |
|------|------|-------------------|
| 1. Requirements | 3-5 min | What are we building? (functional + non-functional) |
| 2. Estimation | 3-5 min | How big? (QPS, storage, bandwidth) |
| 3. API | 2-3 min | What does it do? (core endpoints) |
| 4. Data model | 3-5 min | What do we store? (tables, SQL vs NoSQL) |
| 5. High-level design | 5-10 min | Main components? (draw the boxes) |
| 6. Deep dive | 10-15 min | How does X work? (interviewer picks areas) |
| 7. Bottlenecks | 5 min | What could break? (SPOFs, scaling, failures) |

**Step 1 — Requirements clarification**

Ask, don't assume:
- Functional: What features?
- Non-functional: Scale? Latency? Availability?
- Constraints: Tech requirements?

**Step 2 — Estimation**

Show you think about scale:
- DAU → QPS (read/write separately)
- Storage for N years
- Bandwidth needs

**Step 3 — API definition**

Define before designing internals:
```
POST /shorten { long_url } → { short_url }
GET /{short_url} → redirect
```

**Step 4 — Data model**

- Key tables/collections and fields
- SQL vs NoSQL decision
- Relationships

**Step 5 — High-level design**

Draw the architecture:
```
Client → LB → App Servers → Cache → DB
```

Don't go deep yet.

**Step 6 — Deep dive**

Interviewer picks 1-2 areas:
- "How handle 10x traffic?"
- "What if DB goes down?"
- "Walk through a write"

**Step 7 — Bottlenecks**

Proactively find weaknesses:
- Single points of failure?
- Traffic spikes?
- Data loss scenarios?

Propose solutions: replication, caching, queues.

---

## What's Next

Phase 1 gives you vocabulary and estimation skills. Phase 2 (Building Blocks) covers the actual components you'll use in designs: load balancers, caching, databases, queues, etc.
