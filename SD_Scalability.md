Youtube -- https://www.youtube.com/watch?v=xpDnVSmNFX0


Absolutely bro. Let's make this **interview-ready and easy to remember**.

# 1. What is Scalability?

**Interview answer:**

> **Scalability is the ability of a system to handle increasing users, requests, or workload by adding resources without significantly reducing performance.**

Example:

```text
100 users  → System works fine
1,000 users → System should still work fine
100,000 users → We need to scale the system
```

There are mainly **two ways to scale**:

```text
                    SCALABILITY
                         |
             ┌───────────┴───────────┐
             ↓                       ↓
      Horizontal Scaling       Vertical Scaling
       Add more servers        Increase server power
```

---

# 2. Horizontal Scaling

### Simple meaning

> **Add more servers/machines to handle the increasing load.**

Suppose you have one server:

```text
        Users
          |
          ↓
      Server 1
```

1000 users come → Server struggles.

Instead of making Server 1 bigger, add more servers:

```text
             Users
               |
               ↓
        Load Balancer
          /    |    \
         ↓     ↓     ↓
      Server Server Server
        1      2      3
```

The **Load Balancer distributes requests** among the servers.

### Pros

✅ Can handle a large number of users
✅ Better availability
✅ If one server fails, other servers can continue
✅ Easy to add/remove servers based on demand
✅ Good for cloud and distributed systems

### Cons

❌ More infrastructure cost
❌ Requires load balancing
❌ Application usually needs to be **stateless**
❌ Distributed-system complexity
❌ Data synchronization can become complicated

---

# 3. Vertical Scaling

### Simple meaning

> **Increase the power of an existing server.**

Suppose:

```text
Server
4 CPU
8 GB RAM
```

You upgrade it:

```text
Server
32 CPU
128 GB RAM
```

You haven't added another server. You have made the existing server **more powerful**.

### Pros

✅ Simple to implement
✅ No load balancer required
✅ No distributed-system complexity
✅ Existing application may work without major changes
✅ Easier database scaling initially

### Cons

❌ Hardware has a maximum limit
❌ Expensive at higher configurations
❌ Usually creates a **single point of failure**
❌ Scaling may require downtime depending on infrastructure
❌ Doesn't scale indefinitely

---

# 4. Horizontal vs Vertical

|               | Horizontal                 | Vertical                           |
| ------------- | -------------------------- | ---------------------------------- |
| Basic idea    | Add servers                | Increase server power              |
| Example       | 1 → 5 servers              | 8 GB → 64 GB RAM                   |
| Load Balancer | Usually required           | Usually not                        |
| Availability  | Better                     | Lower                              |
| Limit         | Can scale much further     | Hardware limit                     |
| Complexity    | Higher                     | Lower                              |
| Cost          | More infrastructure        | Powerful hardware can be expensive |
| Failure       | Other servers can continue | Server failure can stop service    |

---

# 5. When to use what?

### Use Vertical Scaling when:

* Application is relatively small
* Traffic is predictable
* You want a simple architecture
* You don't yet need distributed systems
* Database is the main bottleneck and can benefit from a larger machine

Example:

```text
Small application
      ↓
One powerful server
      ↓
Vertical Scaling
```

---

### Use Horizontal Scaling when:

* Number of users is growing significantly
* You need high availability
* Traffic can increase unexpectedly
* You need to handle very large workloads
* You want to scale servers independently
* You're building cloud-native/microservice systems

Example:

```text
Millions of users
       ↓
 Load Balancer
   ↓    ↓    ↓
 S1    S2    S3
```

---

# 6. Explaining Your Image

The image is comparing **Horizontal vs Vertical Scaling**.

### Horizontal side

The image shows multiple boxes:

```text
[1] [2] [3] [4] [5]
```

Meaning **multiple servers**.

The notes mention:

### ① Load balancing required

Because you have multiple servers, you need something to distribute requests:

```text
Users
  ↓
Load Balancer
 ↓  ↓  ↓
S1 S2 S3
```

### ② Resilient

If Server 2 fails:

```text
Load Balancer
   ↓      ↓
  S1     S3
```

The system can continue working.

So horizontal scaling generally provides **better fault tolerance**.

### ③ Network calls / RPC

Because your application is distributed across multiple machines/services, they may need to communicate over the network.

Example:

```text
Order Service
      ↓
Payment Service
      ↓
Inventory Service
```

That introduces network-related issues such as latency and failures.

### ④ Data inconsistency

With multiple servers/services, maintaining consistent data can become more complicated.

For example:

```text
Server 1 → Database
Server 2 → Database
Server 3 → Database
```

You need to carefully handle concurrent updates, caching, replication, etc.

### ⑤ Scales well as users increase

This is the biggest advantage.

```text
10K users
   ↓
3 servers

100K users
   ↓
10 servers

1M users
   ↓
50 servers
```

You can keep adding capacity.

---

# 7. Vertical Side of the Image

The image shows one **"HUGE BOX"**.

That's your powerful server:

```text
       HUGE SERVER
    ┌───────────────┐
    │ CPU: 64 cores │
    │ RAM: 256 GB   │
    │ Storage: ...  │
    └───────────────┘
```

### ① N/A – Load Balancing

Since there is only one server, you don't need a load balancer to distribute traffic.

### ② Single Point of Failure

This is important for interviews.

If the server goes down:

```text
Users
  ↓
❌ Server
```

The entire application can become unavailable.

### ③ Inter-process communication

Since everything may be running on the same machine, communication can happen internally rather than across separate machines.

That generally reduces network complexity.

### ④ Consistent

Having a centralized application/database setup can make consistency simpler compared with a distributed architecture.

### ⑤ Hardware limit

You cannot keep increasing the machine forever.

Eventually:

```text
32 GB
 ↓
64 GB
 ↓
128 GB
 ↓
256 GB
 ↓
???
```

The machine has a physical/configuration limit.

---

# ⭐ Interview Answer to Memorize

If interviewer asks:

**"What is the difference between horizontal and vertical scaling?"**

Say:

> **Horizontal scaling means increasing capacity by adding more servers, while vertical scaling means increasing the CPU, RAM, or other resources of an existing server. Horizontal scaling provides better availability and can scale much further, but it introduces additional complexity such as load balancing, distributed communication, and data consistency. Vertical scaling is simpler but has hardware limitations and can create a single point of failure.**

### One-line memory trick

```text
Horizontal = MORE MACHINES
Vertical   = MORE POWER
```

And remember:

```text
Horizontal
    ↓
More servers
    ↓
Load Balancer
    ↓
Better availability
    ↓
More complexity


Vertical
    ↓
Bigger server
    ↓
Simple
    ↓
Hardware limit
    ↓
Single point of failure
```

------

-----



----
Prerequisites -- Skip if you want
---

# 1. What is RPC?

**RPC = Remote Procedure Call**

In simple English:

> **RPC allows one application/service to call a function or method running on another machine/service as if it were calling a local function.**

### Normal function call

```text
Application
    ↓
CalculatePrice()
    ↓
Result
```

Everything is inside the same application/process.

### RPC

```text
Order Service
     |
     |  CalculatePrice()
     ↓
Payment/Pricing Service
     |
     ↓
   Result
```

The `CalculatePrice()` function actually runs in another service/machine.

The network communication is handled by the RPC framework.

### Common RPC technologies

* gRPC
* WCF
* Apache Thrift
* XML-RPC

### Interview answer

> **RPC is a communication mechanism that allows one service to invoke a method on another remote service over a network.**

### Important

RPC is **not the same as REST**.

REST usually focuses on **resources and HTTP APIs**:

```text
GET /users/10
POST /orders
```

RPC focuses more on **operations/methods**:

```text
CreateOrder()
GetUser()
CalculatePrice()
```

---

# 2. What is a Distributed System?

This is **very important for System Design interviews**.

> **A distributed system is a system where multiple independent computers/services work together over a network to provide one application or service.**

For example:

```text
                Users
                  |
                  ↓
             Load Balancer
              /         \
             ↓           ↓
        Order Service   User Service
             |              |
             ↓              ↓
        Order DB         User DB
             |
             ↓
           Kafka
          /     \
         ↓       ↓
     Payment   Notification
```

These are different machines/services, but together they form one system.

### Why do we use distributed systems?

Main reasons:

* **Scalability**
* **High availability**
* **Fault tolerance**
* **Performance**
* **Separation of services**

### But distributed systems introduce problems

This is where interviewers go deeper:

```text
Network failure
Latency
Data inconsistency
Service failure
Distributed transactions
Message duplication
Concurrency
```

### Interview answer

> **A distributed system consists of multiple independent computers or services that communicate over a network and work together as a single system. It helps achieve scalability and availability but introduces challenges such as network failures, latency, consistency, and coordination.**

---

# 3. What is Inter-Process Communication?

**IPC = Inter-Process Communication**

First understand **process**.

A process is basically a running instance of a program.

For example:

```text
Machine
│
├── Process 1 → Order Service
├── Process 2 → Payment Service
└── Process 3 → Notification Service
```

These processes may need to communicate with each other.

**IPC is the mechanism used for communication between processes.**

### Example

```text
Process A
Order Service
     |
     | IPC
     ↓
Process B
Payment Service
```

They exchange data/messages.

### Common IPC mechanisms

* Pipes
* Shared memory
* Sockets
* Message queues
* Signals

---

# 4. IPC vs RPC

This is where it can get confusing.

### IPC

General communication between processes.

```text
Process A
    ↕
   IPC
    ↕
Process B
```

They could be on the **same machine**.

### RPC

A mechanism specifically designed to call functionality on a **remote process/service**, normally across a network.

```text
Machine A                    Machine B

Order Service  ── RPC ──→   Payment Service
```

### Easy way to remember

> **IPC = How processes communicate**

> **RPC = How you call a remote service/method**

RPC itself ultimately uses network communication mechanisms underneath.

---






