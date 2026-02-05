# Phase 2: Load Balancing — Notes

Quick reference for load balancing concepts.

---

## Algorithms

| Algorithm | Question it asks | Good when |
|-----------|------------------|-----------|
| **Round robin** | Whose turn? | Requests are uniform, servers identical |
| **Weighted round robin** | Whose turn? (some get more turns) | Servers have different capacities |
| **Least connections** | Who has fewest active requests? | Request processing time varies |
| **IP hash** | What's the client's IP? | Need sticky sessions (stateful servers) |
| **Consistent hashing** | What's the data key? | Sharded data, caches |

**Round robin problem:** Assumes all requests are equal. If one request takes 5 seconds and others take 10ms, the slow server becomes a bottleneck while others sit idle.

---

## L4 vs L7 Load Balancers

| | L4 (Transport) | L7 (Application) |
|---|---|---|
| **Sees** | IP, port, protocol | Everything: URL, headers, cookies, body |
| **Speed** | Faster (forwards packets) | Slower (parses HTTP) |
| **Resource usage** | Lighter | Heavier |
| **Routing smarts** | Dumb (IP/port only) | Smart (path-based, header-based) |
| **SSL termination** | No | Yes |

**Common production pattern:**
```
Internet → L4 LB → multiple L7 LBs → app servers
```
- L4: fast, cheap, distributes across L7 instances
- L7: smart routing, SSL termination, content-based decisions

---

## SSL Termination

L7 load balancer decrypts HTTPS traffic, inspects it, makes routing decisions.

**Benefits:**
- Centralized certificate management
- Offloads CPU-intensive encryption from app servers
- Enables inspection for routing and security

**Internal traffic options:**

| Pattern | Security | Complexity |
|---------|----------|------------|
| Plain HTTP internally | Trusted network | Simple |
| Internal certificates | Encrypted, self-managed CA | Medium |
| End-to-end (zero trust) | High security | Complex |

Most systems use plain HTTP or internal certs within private networks.

---

## Health Checks

**Passive:** Watch real traffic for errors. Con: users hit errors first.

**Active:** Ping servers periodically. Preferred — catches failures before users.

```
LB → GET /health → Server
LB ← 200 OK or timeout/500
```

### Liveness vs Readiness

| Endpoint | Checks | Used by |
|----------|--------|---------|
| `/health/live` | Is process running? | LB routing |
| `/health/ready` | Can handle requests? (DB, deps) | Deployments, monitoring |

**Why separate:** If DB goes down and all servers fail readiness, LB marks everything dead. Users get nothing, even though servers could serve cached/degraded responses.

### Failover Timing

```
Check interval: 5 seconds
Failure threshold: 3 checks
Server crash at T=0 → Traffic stops at T=15 (worst case)
```

**Tradeoff:** Faster detection risks false positives (healthy server removed). Slower detection means more failed requests.

---

## High Availability for Load Balancers

### Active-Passive

```
LB1 (active) ←── traffic
     ↕ heartbeat
LB2 (standby)

LB1 dies → LB2 takes over floating IP
```

- **Pro:** Simple
- **Con:** LB2 sits idle, failover delay (seconds of downtime)

### Active-Active

```
LB1 ←── traffic
LB2 ←── traffic

One dies → other handles all
```

- **Pro:** Full utilization, no failover delay
- **Con:** Need DNS or another layer to distribute across LBs

Cloud LBs (AWS ALB, GCP) are active-active by default.

---

## Stateless Design

**Problem:** Sticky sessions (IP hash) break when server dies — user loses session.

**Solution:** Externalize session state.

```
Stateful (bad):
  User → always Server B → session in B's memory
  B dies = session lost

Stateless (good):
  User → any server → reads session from Redis
  B dies = C picks up, same session
```

**Tradeoff:** Extra hop to Redis adds latency. Gain fault tolerance and free scaling.

**Interview tip:** "We'll keep servers stateless and store sessions in Redis so we can load balance freely and handle server failures."

---

## DNS-Based Load Balancing

DNS returns multiple IPs for one domain:
```
api.example.com → 52.1.1.1, 52.1.1.2, 52.1.1.3
```

Client picks one. DNS rotates order — simple round robin.

**Real usage:** Global/regional routing
```
api.example.com → LB1 (us-east), LB2 (us-west)
```

| Pros | Cons |
|------|------|
| Global distribution | Slow failover (DNS caching, TTL) |
| No single point of failure | Can't see server load |
| Cheap, simple | No fine-grained routing |

**Pattern:** DNS for global routing → LB for actual balancing within region.

---

## What's Next

Caching — cache levels, strategies, eviction policies, invalidation, distributed caches.
