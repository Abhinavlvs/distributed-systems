# Initial Roadmap
---

### Step 1: Big-picture overview (no heavy math, just intuition)

### Videos
1. [Distributed Systems in One Lesson](https://learning.oreilly.com/videos/-/9781491924914/) by Tim Berglund  
   - Description: **A fast-paced conceptual tour of core distributed systems ideas: consistency, availability, partitioning, replication, and coordination. Great as a first exposure.**  
   - Publication Date: **June 2015**  
   - Duration: **~4h 8m**

Use this to get familiar with terminology: nodes, replication, consensus, CAP, eventual consistency.

---

### Step 2: Fundamentals and mental models

### Books
1. [Think Distributed Systems](https://learning.oreilly.com/library/view/-/9781633436176/) by Dominik Tornow  
   - Description: **Conceptual guide to thinking in distributed terms: events, state, ordering, and failures. Focus on intuition rather than any single technology.**  
   - Publication Date: **September 2025**  
   - Page Count: **192 pages**

2. [Patterns of Distributed Systems](https://learning.oreilly.com/library/view/-/9780138222246/) by Unmesh Joshi  
   - Description: **Catalog of reusable patterns (leader election, sharding, replica nodes, etc.) with explanations of when and why to use them. Bridges theory and real-world designs.**  
   - Publication Date: **December 2023**  
   - Page Count: **464 pages**

Study order suggestion:
- Skim *Think Distributed Systems* first for intuition.
- Then work steadily through *Patterns of Distributed Systems* (a few patterns per week).

---

### Step 3: Practical design and architectures

Since you already have *Designing Distributed Systems* in your history, use it as your practical backbone.

### Books
1. [Designing Distributed Systems](https://learning.oreilly.com/library/view/-/9781491983638/) by Brendan Burns  
   - Description: **Component- and container-based design patterns with Kubernetes examples—sidecars, ambassadors, adapters, batch jobs, etc.**  
   - Publication Date: **February 2018**  
   - Page Count: **162 pages**

2. [Designing Distributed Systems, 2nd Edition](https://learning.oreilly.com/library/view/-/9781098156343/) by Brendan Burns  
   - Description: **Updated edition (forthcoming) expanding patterns for modern cloud-native environments, advanced Kubernetes usage, and newer ecosystem tools.**  
   - Publication Date: **December 2024**  
   - Page Count: **220 pages**

How to use:
- Read the 1st edition now for patterns + concrete Kubernetes examples.
- When the 2nd edition is fully out, skim it for updated practices and new chapters.

---

### Step 4: Reliability and advanced topics

### Books
1. [Building Resilient Distributed Systems](https://learning.oreilly.com/library/view/-/9781098163532/) by Sam Newman  
   - Description: **Focuses on resilience: timeouts, retries, backpressure, bulkheads, circuit breakers, and handling partial failures in microservices and distributed systems.**  
   - Publication Date: **September 2026**  
   - Page Count: **390 pages**

2. [Building Distributed Applications that Work](https://learning.oreilly.com/library/view/-/9781633435124/) by Fiodar Sazanavets  
   - Description: **Practical guidance on getting real distributed apps correct: state management, messaging, coordination, and dealing with real-world deployment environments.**  
   - Publication Date: **September 2026**  
   - Page Count: **272 pages**

Optional, more specialized:
3. [Distributed AI Systems](https://learning.oreilly.com/library/view/-/9781807301712/) by Fuheng Wu  
   - Description: **Applies distributed systems ideas to AI/ML workloads: distributed training, inference, and data pipelines.**  
   - Publication Date: **June 2026**  
   - Page Count: **558 pages**

---

### How to progress from scratch to advanced (study plan)

Assuming you can study ~6–8 hours/week:

**Month 1–2: Foundations**
- Watch: *Distributed Systems in One Lesson* (take notes on key concepts).
- Read: *Think Distributed Systems* (1–2 chapters/week).
- Start: *Patterns of Distributed Systems* (aim for ~3–4 patterns/week).

**Month 3–4: Design patterns in practice**
- Read: *Designing Distributed Systems* (1st ed.), implement at least 2–3 patterns in simple demos (any language you’re comfortable with).
- Continue: *Patterns of Distributed Systems* focusing on patterns that match your demos.

**Month 5–6: Resilience and “real world”**
- Read: *Building Resilient Distributed Systems*.
- If possible, refactor an existing side project or work service using these resilience patterns.
- Start: *Building Distributed Applications that Work* to connect theory with deployment and operations.

**After that (advanced)**
- Revisit tricky topics (consensus, distributed transactions, event sourcing).
- Dive into domain-specific areas like *Distributed AI Systems* if relevant to your work.

---

To tailor this better:  
- What’s your current programming language of choice?  
- Are you more interested in microservices/web backends, data systems (Kafka, databases), or AI/ML platforms?

---

# Language 

## 1. Keep the same learning backbone

The resources I suggested before still stand:

- Conceptual:  
  - *Distributed Systems in One Lesson* – video  
  - *Think Distributed Systems* – high-level mental models  
  - *Patterns of Distributed Systems* – core patterns

- Practical design:  
  - *Designing Distributed Systems* (and later its 2nd edition)

- Reliability / advanced:  
  - *Building Resilient Distributed Systems*  
  - *Building Distributed Applications that Work*

Use those as your theory and architecture base.

---

## 2. How to practice with Python

Use Python to quickly prototype and “see” distributed behavior.

**Suggested progression:**

1. **Basics of communication**
   - Build tiny scripts using:
     - `socket` module: simple TCP server + client.
     - `asyncio`: concurrent echo server with multiple clients.
   - Goal: understand latency, timeouts, and how failures look (e.g., client disconnect).

2. **RPC & microservices**
   - Use something like:
     - `FastAPI` or `Flask` for HTTP APIs between services.
   - Practice:
     - A “user” service and an “order” service communicating over HTTP.
     - Add retries and timeouts with `httpx` or `requests`.

3. **Messaging / queues**
   - Use:
     - RabbitMQ (via `pika`) or Kafka (via `confluent-kafka-python`).
   - Build:
     - A producer that sends events.
     - One or more consumers that process them (e.g., email sending, logging).

4. **State & consistency**
   - Implement:
     - A simple “event-sourced” service: append events to a log (file or DB) and rebuild state from the log.
     - A simple “replica” that subscribes to the log and keeps a local copy.
   - Connect with patterns from *Patterns of Distributed Systems* (e.g., Replicated Log, Leader Election using a basic coordinator).

5. **Resilience patterns (aligned with the books)**
   - Use libraries or simple wrappers to implement:
     - Timeouts and retries.
     - Circuit breaker (can even hand-roll a basic one using a decorator).
   - Run experiments:
     - Kill one service and observe behavior.
     - Introduce artificial latency and see where things break.

---

## 3. How to practice with Rust

Use Rust to internalize *correctness and performance* in distributed systems.

Given your history (e.g., “Programming Rust, 3rd Edition”), you’re already on a good path.

**Suggested progression:**

1. **Networking with Rust**
   - Implement:
     - A TCP echo server and client using `std::net` or `tokio`.
   - Move to asynchronous:
     - Use `tokio` for async I/O, spawn multiple tasks, handle many clients.

2. **Binary protocols and correctness**
   - Define a small custom protocol (e.g., framed messages with length prefix).
   - Implement:
     - Encoder/decoder (consider using `bincode`, `serde`).
   - This teaches you how real distributed systems define and evolve protocols.

3. **Cluster of simple services**
   - Build:
     - N nodes that each maintain a key-value store in memory.
     - A basic “coordinator” that routes requests to one of the nodes (round-robin).
   - Add:
     - Health checks: nodes send heartbeats to the coordinator.

4. **Failure handling**
   - Implement:
     - Heartbeat messages.
     - Node timeouts and removal from the cluster.
   - Compare your implementation with leader election / membership patterns you see in *Patterns of Distributed Systems*.

5. **Advanced (optional but powerful)**
   - Implement simplified versions of:
     - A replicated log (Raft-style but much simpler).
     - Or a basic CRDT counter (grow-only, then PN-counter).
   - Rust’s type system helps you encode invariants, which is very close to how real production systems are built.

---

## 4. How to combine both languages in your learning

You don’t need to choose only one:

- **Prototype concepts in Python**:
  - Test an idea fast (e.g., event sourcing, CQRS, pub/sub).
  - Once you understand the behavior, move to…

- **Re-implement the core in Rust**:
  - Focus on performance, concurrency, and safety.
  - This “double implementation” will force you to understand the pattern deeply.

Example learning loop for a single pattern (e.g., leader election):

1. Read the pattern in *Patterns of Distributed Systems*.
2. Implement a simple “coordinator election” in Python with basic HTTP or sockets.
3. Re-implement the same in Rust with `tokio`, focusing on:
   - Timeouts.
   - Message formats.
   - Edge cases (network partitions).

---

## 5. Next step for you

Given what you’ve said and your history:

1. Start the video:  
   - *Distributed Systems in One Lesson* – watch it once, then note key concepts.
2. In parallel:
   - Begin *Think Distributed Systems*.
   - Implement a simple TCP echo server/client in **both Python and Rust**.

If you’d like, tell me:
- Your current Rust level (comfortable with `tokio` or still basic)?  
- Whether you already know `asyncio`/FastAPI in Python?

I can then give you a concrete 4-week, step-by-step coding plan with specific mini-projects in both languages.
