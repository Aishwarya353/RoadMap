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
# Sample Architecture 
Keep this picture in mind:

```text
                    SCALABILITY
                        |
              ┌─────────┴─────────┐
              ↓                   ↓
          SCALE-UP            SCALE-OUT
              ↓                   ↓
        Bigger Server        More Servers
                                  |
                                  ↓
                         Stateless Application
                                  |
                                  ↓
                            Auto Scaling
                                  |
                                  ↓
                            Elasticity
```

And separately:

```text
              SYSTEM PERFORMANCE
                     |
                     ↓
              Find Bottleneck
             /       |        \
           CPU      RAM       DB
            |        |         |
            └────────┴─────────┘
                     ↓
               Scale the right
                  component
```

And:

```text
Scalability ≠ High Availability

Scalability
    ↓
Handle MORE LOAD

High Availability
    ↓
Stay AVAILABLE when failures happen
```
----

Exactly bro. 💯

> **Scale Up = Vertical Scaling**
> **Scale Out = Horizontal Scaling**

### ❌ Application should preferably be stateless for Scale out

This is **very important**.

Suppose:

```text
Request 1 → Server 1
Request 2 → Server 2
```

If the user's session exists only on Server 1, Server 2 doesn't know about it.

That's why **stateless architecture** becomes important when scaling out.

We'll cover this next. 🔥

---

# 9. The Interview Comparison

|                    | **Scale Up**         | **Scale Out**           |
| ------------------ | -------------------- | ----------------------- |
| Other name         | Vertical Scaling     | Horizontal Scaling      |
| What changes?      | Existing server      | Number of servers       |
| Complexity         | Low                  | Higher                  |
| Hardware limit     | Yes                  | Much higher scalability |
| Load Balancer      | Usually unnecessary  | Usually needed          |
| Availability       | Lower                | Generally better        |
| Cost               | Can become expensive | More infrastructure     |
| Distributed system | Not necessarily      | Usually                 |
| Statelessness      | Less important       | Very important          |

---

# 🔥 Interview Question

### Interviewer:

**"Your application is getting 10x more traffic. Would you scale up or scale out?"**

Don't immediately say **horizontal**.

A good answer is:

> "It depends on the application's requirements and bottleneck. If the workload can be handled by increasing CPU or memory on the existing server and the system is relatively simple, I could scale up. But if I need to handle significantly higher traffic, require high availability, or expect continued growth, I would generally prefer scaling out by adding multiple instances behind a load balancer."

That's a **much stronger 4-year-level answer** than simply saying "horizontal scaling is better."

---

# 🧠 One Important Distinction

Don't confuse:

**Scale Out** with **Load Balancing**.

They're related but NOT the same.

```text
Scale Out
   ↓
Add more servers

        S1
        S2
        S3
```

Then:

```text
Load Balancing
   ↓
Distribute requests across those servers

             Users
               ↓
        Load Balancer
        /      |      \
       ↓       ↓       ↓
      S1       S2      S3
```

So:

> **Scale Out = Adding capacity**

> **Load Balancer = Distributing traffic**

---

### 🎯 Final memory trick

```text
SCALE UP
= Make ONE server stronger
= Vertical

SCALE OUT
= Add MORE servers
= Horizontal
```

And the next concept logically is **Stateless vs Stateful**, because once we have multiple servers, we immediately face the question:

> **"If the same user's requests go to different servers, how does the application remember that user?"**
--------

Exactly bro. This is one of the **most important questions** when learning horizontal scaling.

### ❓ Interview Question

> **"If the same user's requests go to different servers, how does the application remember that user?"**

### ✅ Interview Answer

> **In a horizontally scaled system, we should ideally keep the application servers stateless. Instead of storing the user's session information in a particular server's memory, we store it in a shared location such as a distributed cache like Redis or use a token-based approach such as JWT. This allows any server to handle the user's next request.**

### Example

Without statelessness:

```text
User
 ↓
Load Balancer
 ↓
Server 1
   ↓
Session stored in Server 1 memory
```

Next request:

```text
User
 ↓
Load Balancer
 ↓
Server 2
   ↓
❌ "I don't know this user"
```

Because Server 2 doesn't have Server 1's session data.

---

### ✅ Stateless approach

```text
                  User
                    ↓
              Load Balancer
               /          \
              ↓            ↓
          Server 1      Server 2
              \            /
               \          /
                  ↓
                 Redis
             Shared Session
```

Now either server can handle the request:

```text
Request 1 → Server 1 → Redis
Request 2 → Server 2 → Redis
Request 3 → Server 1 → Redis
```

All servers can access the same session information.

---

### Another approach: JWT

Instead of keeping the session on the server:

```text
User
 ↓
Login
 ↓
JWT Token
 ↓
Client stores token
```

Every request sends the token:

```text
Request → Server 1
          ↓
       Validate JWT

Request → Server 2
          ↓
       Validate JWT
```

The server doesn't need to remember the session in its own memory.

---

### ⚠️ What about Sticky Sessions?

There is another solution called **sticky session / session affinity**:

```text
User A → Server 1
User A → Server 1
User A → Server 1
```

The load balancer keeps sending that user to the same server.

It works, but it's generally **less desirable for highly scalable systems** because if Server 1 fails, the user's session can be affected, and traffic isn't distributed as freely.

---

### 🧠 Interview-ready answer

If they ask this in an interview, say:

> **"When scaling horizontally, I prefer stateless application servers. Session state should not be stored only in server memory. We can store shared session data in a distributed cache such as Redis, or use token-based authentication like JWT. This allows any server behind the load balancer to process the user's request."**

And if they ask:

**"Can we use sticky sessions?"**

Say:

> **"Yes, sticky sessions can keep a user mapped to the same server, but they introduce server dependency and can reduce the benefits of horizontal scaling. For a highly scalable architecture, I generally prefer stateless services with shared state in Redis or token-based authentication."**

### 🔑 Remember

```text
Stateful
= Server remembers you

Stateless
= Server doesn't need to remember you
  → state is stored/shared elsewhere
```

Bro 😄 the confusion is because **"stateful" sounds abstract**. Let's forget the formal definition for a minute and understand what the server is literally doing.

## 1. What does "remember" actually mean?

A server **doesn't magically remember you**.

It stores some information somewhere.

For example, you log in:

```text
Username: Alice
Password: ****
```

Server verifies you and creates:

```text
Session ID = ABC123
User = Alice
LoggedIn = true
```

Then the server stores this information, for example, in its **memory**:

```text
SERVER 1 MEMORY

ABC123 → Alice → Logged In
```

That's the **state**.

So:

> **State = information the server stores about what happened previously.**

---

# 2. Now let's see the actual request

You login:

```text
Browser
   |
   | POST /login
   ↓
Server 1
```

Server 1 says:

```text
"Login successful!"
```

And stores:

```text
Server 1 Memory

ABC123 → Alice
```

Then the server gives your browser a **cookie**:

```text
Cookie:
SessionId = ABC123
```

Your browser stores that cookie.

---

# 3. You make the next request

You click:

> "My Profile"

Browser automatically sends:

```text
GET /profile

Cookie:
SessionId = ABC123
```

Request goes to:

```text
Browser
   ↓
Server 1
```

Server 1 looks into its memory:

```text
ABC123
   ↓
Alice
```

So it knows:

> "Oh, this is Alice. He is logged in."

### That's how the server "remembers".

It doesn't actually remember your face 😂.

It remembers a **Session ID** and associated data.

---

# 4. Now the problem with multiple servers

This is where your confusion should disappear.

Suppose we have:

```text
              Load Balancer
              /           \
             ↓             ↓
        Server 1        Server 2
```

You login:

```text
Browser
   ↓
Load Balancer
   ↓
Server 1
```

Server 1 stores:

```text
SERVER 1 MEMORY

ABC123 → Alice
```

Now you make another request.

Load Balancer sends you to Server 2:

```text
Browser
   ↓
Load Balancer
   ↓
Server 2
```

Browser still sends:

```text
SessionId = ABC123
```

But Server 2 checks its memory:

```text
SERVER 2 MEMORY

?????
```

It doesn't have:

```text
ABC123 → Alice
```

So Server 2 says:

> "Who is ABC123? 🤷"

That's the **stateful problem**.

---

# 5. Then what is Sticky Session / Session Affinity?

**Affinity means "keep something associated with something else."**

So:

> **Session Affinity = Keep the same user's requests associated with the same server.**

Example:

```text
              Load Balancer
              /           \
             ↓             ↓
        Server 1        Server 2
           ↑
           |
       Alice
```

The Load Balancer remembers:

```text
Alice / Session ABC123
          ↓
       Server 1
```

So:

```text
Request 1 → Server 1
Request 2 → Server 1
Request 3 → Server 1
Request 4 → Server 1
```

Even though there are multiple servers.

That's called:

> **Sticky Session / Session Affinity**

---

# 6. But there is a better technique

Instead of:

```text
Server 1 Memory
      ↓
ABC123 → Alice
```

we can put the session in a **shared storage**.

For example, Redis:

```text
              Load Balancer
              /           \
             ↓             ↓
        Server 1        Server 2
             \            /
              \          /
                Redis
                  |
                  ↓
          ABC123 → Alice
```

Now:

```text
Request 1 → Server 1 → Redis
Request 2 → Server 2 → Redis
Request 3 → Server 1 → Redis
Request 4 → Server 2 → Redis
```

Every server can find:

```text
ABC123 → Alice
```

That's how we solve the problem.

---

# 7. And JWT is another technique

With JWT, we don't necessarily store the session on the server.

After login:

```text
Server
  ↓
Creates JWT
  ↓
Browser
```

The browser sends the JWT with every request:

```text
Request
   +
JWT
   ↓
Server 1
```

or:

```text
Request
   +
JWT
   ↓
Server 2
```

Both servers can validate the token.

So there is no need for:

```text
Server 1 Memory
```

to remember the user.

That's why JWT is commonly used with stateless APIs.

---

# 8. So there are 3 common approaches

### Approach 1 — Server memory

```text
User
 ↓
Server 1
 ↓
Session stored here
```

**Stateful**

---

### Approach 2 — Sticky Session

```text
User
 ↓
Load Balancer
 ↓
Always Server 1
 ↓
Session in Server 1
```

Still **stateful**, but the load balancer keeps you attached to that server.

---

### Approach 3 — Shared session / JWT

```text
             Load Balancer
             /           \
            ↓             ↓
        Server 1       Server 2
            \             /
             \           /
               Redis
```

or:

```text
User
 ↓
JWT
 ↓
Any Server
```

This is the typical direction for **stateless architectures**.

---

# 🔥 The ONE thing I want you to remember

Don't think:

> "Stateful means server remembers the user."

Think:

> **Stateful means the server/application maintains information about previous requests.**

And the technique behind that "memory" is usually:

```text
LOGIN
  ↓
Create Session
  ↓
Generate Session ID
  ↓
Store Session ID + User Information
  ↓
Send Session ID to Browser as Cookie
  ↓
Browser sends Cookie on future requests
  ↓
Server uses Session ID to find the user's state
```

That's it bro. **That's the actual mechanism.**

### Interview answer

If they ask:

**"How does a stateful server remember a user?"**

Say:

> "Typically, after authentication, the server creates a session and generates a session ID. The session ID is sent to the client, usually as a cookie. On subsequent requests, the client sends that session ID back, and the server uses it to retrieve the user's session state, either from its own memory or from shared session storage."

-----

# still why and when we use Stateful why can't all applciations use stateless

Yes bro — **this is the exact question that makes Stateful vs Stateless click.**

The short answer is:

> **We can make many applications stateless, but we cannot always avoid state. The application needs to remember some information somewhere. Stateless means the application server itself doesn't own that state.**

Let's make it very simple.

---

# 1. First: Why do we need "state"?

Imagine an **online shopping cart**.

You do:

```text
1. Login
2. Add iPhone to cart
3. Add AirPods to cart
4. Go to checkout
```

The system needs to know:

```text
User = Alice
Cart = iPhone + AirPods
```

That information is **state**.

Without state:

```text
Request 1 → "I am Alice"
Request 2 → "Add iPhone"
Request 3 → "Add AirPods"
Request 4 → "Checkout"
```

When request 4 arrives, the system needs to know:

> "Whose cart is this?"

So **state is necessary** in many applications.

---

# 2. Then what does Stateless mean?

This is where people get confused.

**Stateless does NOT mean "the application has no data."**

It means:

> **The individual application server does not depend on information stored in its own memory from previous requests.**

For example:

```text
             Load Balancer
             /           \
            ↓             ↓
        Server 1       Server 2
```

Request 1:

```text
User → Server 1
```

Request 2:

```text
User → Server 2
```

Server 2 can still process the request because the required state is available through:

* Database
* Redis
* JWT/token
* Other shared storage

---

# 3. Real example — Shopping Cart

### Stateful approach

```text
             Server 1
                |
                ↓
        Memory:
        Alice's Cart
        iPhone
        AirPods
```

Problem:

```text
Request 1 → Server 1 ✅
Request 2 → Server 2 ❌
```

Server 2 doesn't know about the cart.

---

### Stateless approach

Put the cart somewhere shared:

```text
            Server 1
               |
               ↓
              DB
               ↑
               |
            Server 2
```

Now:

```text
Request 1 → Server 1 → DB
Request 2 → Server 2 → DB
Request 3 → Server 1 → DB
```

Both servers can get the cart.

**That's stateless application servers.**

---

# 4. So why would we ever use Stateful?

Because sometimes keeping state **inside the server/process** is useful or simpler.

### Example: Online game

Imagine a multiplayer game server.

It might maintain:

```text
Player position
Health
Weapons
Current game state
Nearby players
Physics state
```

And the game server continuously manages that state.

```text
Player
  ↓
Game Server
  ↓
Game State
```

Moving all of that state to an external database on every operation could introduce:

* Latency
* Network overhead
* Complexity
* Performance problems

So a **stateful server can make sense**.

---

# 5. Another simple example: WebSocket

Imagine a chat application.

You establish a WebSocket connection:

```text
User
  |
  | WebSocket
  ↓
Server 1
```

The server maintains information about the active connection:

```text
Connection ABC
    ↓
User Alice
    ↓
Server 1
```

The server needs to know:

> "This WebSocket connection belongs to Alice."

That's state.

You **can** build distributed architectures around it, but connection state has to live somewhere, and keeping it local can be useful.

---

# 6. Then why does everyone prefer Stateless?

Because **horizontal scaling becomes much easier**.

Imagine:

```text
                 Load Balancer
              /       |       \
             ↓        ↓        ↓
           S1        S2       S3
```

If servers are stateless:

```text
Any request
     ↓
Any server
     ↓
Works
```

You can easily add:

```text
S4
S5
S6
```

And remove them when traffic drops.

This is excellent for scalability.

---

# 7. Stateful creates a problem

Suppose:

```text
User A
  ↓
Server 1
```

Server 1 has:

```text
Session A
Game State A
Connection A
```

Now Server 1 crashes:

```text
User A
  ↓
❌ Server 1
```

That state may be lost.

With stateless servers:

```text
User
 ↓
Server 1 ❌

       ↓

Server 2
 ↓
Shared State
```

Server 2 can continue.

That's a major advantage.

---

# 8. But Stateless doesn't eliminate state

This is **the most important point**.

Look at this:

```text
             Load Balancer
             /           \
            ↓             ↓
        Server 1       Server 2
             \           /
              \         /
               ↓       ↓
                  Redis
                    |
                    ↓
                Database
```

The servers are **stateless**.

But the **overall system is still storing state**.

For example:

```text
Database
    ↓
User information
Order information
Payment information

Redis
    ↓
Session
Cache
Temporary state
```

So:

> **Stateless application ≠ application with no state.**

It means:

> **State isn't tied to a particular application server.**

---

# 9. When should we use Stateful?

Use stateful when keeping state locally provides a strong benefit and the workload doesn't require every request to freely move between instances.

Common examples:

### Stateful

* Multiplayer game servers
* Long-lived connections
* Some WebSocket architectures
* Certain real-time processing systems
* Systems where local state is extremely performance-sensitive

### Stateless

* REST APIs
* Typical web applications
* Microservices
* Public APIs
* CRUD applications
* Authentication APIs using JWT
* Most cloud-native application services

---

# 10. Interview Question

### ❓ "If stateless is better for scalability, why don't we make everything stateless?"

### ⭐ Strong answer:

> **"Stateless services are generally preferred because they make horizontal scaling, load balancing, and failover easier. However, applications still need state for things like sessions, game state, or long-lived connections. We can move that state to shared storage such as a database or Redis, but doing so can introduce network latency, additional infrastructure, and complexity. Therefore, whether we use a stateful or stateless design depends on the application's requirements."**

That's a **very good 4-year interview answer**.

---

# 🧠 The easiest way to remember

Think about a **hotel receptionist**.

### Stateful receptionist

You go to Receptionist A:

> "My room is 501."

Receptionist A remembers you.

Next time you go to Receptionist B:

> "Who are you?" 😄

---

### Stateless receptionist

You give your booking number every time:

```text
Booking #12345
```

Any receptionist can look it up:

```text
Receptionist A → Database
Receptionist B → Database
Receptionist C → Database
```

They don't need to personally remember you.

**That's the whole idea.**

```text
STATEFUL
Server remembers
       ↓
Harder to move request between servers


STATELESS
Server doesn't personally remember
       ↓
State stored/shared elsewhere
       ↓
Any server can handle request
       ↓
Easy horizontal scaling
```

So the key question isn't **"Does my application have state?"**

The real question is:

> **"Where does the state live, and is my application server dependent on that local state?"**
-------
Let's go bro 🔥

## 3. Elasticity

Now that you understand **Scale Up, Scale Out, and Stateless**, elasticity is the natural next concept.

### ❓ What is Elasticity?

**Easy definition:**

> **Elasticity is the ability of a system to automatically increase or decrease resources based on the current workload.**

Think:

```text
Traffic
  ↑
  │
  │       More users
  │          ↓
  │     Add servers
  │          ↓
  │    Handle traffic
  │
  │       Traffic drops
  │          ↓
  │     Remove servers
  │          ↓
  │     Save resources
  └──────────────────→ Time
```

### Simple example

Normal traffic:

```text
Users
  ↓
Load Balancer
  ↓
S1  S2
```

Traffic suddenly increases:

```text
Users ↑↑↑
   ↓
Load Balancer
   ↓
S1  S2  S3  S4  S5
```

Traffic comes back down:

```text
Users ↓
   ↓
Load Balancer
   ↓
S1  S2
```

The system **adds and removes capacity according to demand**.

That's elasticity.

---

# Scalability vs Elasticity

This is a **very common interview question**.

### Scalability

> Can the system handle increasing load by adding resources?

Example:

```text
2 servers → 5 servers
```

### Elasticity

> Can the system **dynamically add and remove** resources as demand changes?

```text
Normal:
2 servers

Peak:
10 servers

After peak:
2 servers
```

### Easy memory trick

> **Scalability = ability to grow**

> **Elasticity = ability to grow AND shrink based on demand**

---

# Real-world example

Imagine an e-commerce website.

Normal day:

```text
10,000 users
    ↓
5 servers
```

During a major sale:

```text
500,000 users
    ↓
50 servers
```

After the sale:

```text
10,000 users
    ↓
5 servers
```

The ability to dynamically move:

```text
5 → 50 → 5
```

is **elasticity**.

---

# Why do we need Elasticity?

Main reason:

### 💰 Cost optimization

Without elasticity:

```text
Normal traffic
     ↓
50 servers running
     ↓
Most servers idle
     ↓
💰 Wasted money
```

With elasticity:

```text
Normal → 5 servers
Peak   → 50 servers
Normal → 5 servers
```

You only use additional capacity when required.

---

# Is Elasticity the same as Auto Scaling?

**No.**

They're closely related but different.

### Elasticity

The **capability/characteristic**:

> "The system can dynamically adjust resources."

### Auto Scaling

The **mechanism/tool/process** that performs it automatically.

```text
Elasticity
    ↑
The goal/capability

Auto Scaling
    ↑
The mechanism that implements it
```

We'll cover **Auto Scaling next**.

---

# Interview Question

### ❓ "What is elasticity?"

### ⭐ Answer:

> **Elasticity is the ability of a system to dynamically increase or decrease resources based on workload. For example, during a traffic spike, the system can add application instances, and when traffic decreases, it can remove those instances to optimize resource utilization and cost.**

---

### ❓ "Is a vertically scaled system elastic?"

It **can be**, but elasticity is much more commonly associated with dynamically adjusting resources in cloud environments.

For example:

```text
Vertical:
4 CPU → 16 CPU → 4 CPU
```

could technically be elastic, but changing machine size may be slower or require infrastructure changes.

Horizontal elasticity is usually more practical:

```text
2 instances
     ↓
10 instances
     ↓
2 instances
```

---

# 🧠 Remember this

```text
SCALABILITY
    ↓
Can handle more load
    ↓
Scale Up / Scale Out


ELASTICITY
    ↓
Dynamically adjust capacity
    ↓
Increase when needed
    ↓
Decrease when no longer needed


AUTO SCALING
    ↓
Automatically performs scaling
    ↓
Based on rules/metrics
```

### Our journey now:

```text
Scale Up / Scale Out ✅
        ↓
Stateless / Stateful ✅
        ↓
Elasticity ✅
        ↓
👉 Auto Scaling
        ↓
Bottleneck Identification
        ↓
High Availability vs Scalability
```

**Next: Auto Scaling** — this is where we'll see *exactly how the system decides "I need 5 more servers"* and what metrics it uses.
Yes bro — **Scale Up can also be elastic**, but there is an important difference.

## Can Scale Up be elastic?

**Yes.**

Elasticity means:

> Automatically increasing **or decreasing** resources based on demand.

That resource can theoretically be **CPU/RAM of a machine** (Scale Up) or the **number of machines** (Scale Out).

### Scale Up Elasticity

Imagine a cloud VM:

```text
Normal traffic
    ↓
4 CPU / 16 GB RAM
```

Traffic increases:

```text
    ↓
8 CPU / 32 GB RAM
```

Traffic increases more:

```text
    ↓
16 CPU / 64 GB RAM
```

Traffic decreases:

```text
    ↓
4 CPU / 16 GB RAM
```

So:

```text
4 CPU → 8 CPU → 16 CPU → 4 CPU
```

That's **elastic vertical scaling**.

Cloud platforms can support changing the size of a VM/instance, although it may involve **restarting/redeploying the instance** depending on the platform and configuration.

---

## Why do we usually talk about elasticity with Scale Out?

Because Scale Out is much more practical for automatic elasticity.

```text
Scale Out

2 servers
   ↓
5 servers
   ↓
10 servers
   ↓
5 servers
   ↓
2 servers
```

You can add/remove instances without making one machine increasingly powerful.

This is especially useful in cloud environments.

### Interview point ⭐

If asked:

> **"Can vertical scaling be elastic?"**

Say:

> **"Yes. Vertical scaling can also be elastic if the infrastructure dynamically increases or decreases the resources of an instance. However, horizontal scaling is more commonly used for cloud elasticity because instances can be added or removed more easily and it provides better scalability and availability."**

---

# 🚀 Now: Auto Scaling

This is the next concept.

## What is Auto Scaling?

Auto Scaling is the **automatic mechanism that adds or removes resources based on predefined conditions or metrics.**

For example:

```text
                Monitor
                   ↓
              CPU = 80%
                   ↓
             Auto Scaling
                   ↓
             Add Server
```

### Example

Suppose you normally have:

```text
        Load Balancer
          /       \
         ↓         ↓
       S1          S2
```

Your rule says:

> If average CPU > 70% for 5 minutes → add a server.

Traffic increases:

```text
CPU = 85%
   ↓
Auto Scaling
   ↓
Add S3
```

Now:

```text
        Load Balancer
       /      |      \
      ↓       ↓       ↓
     S1      S2      S3
```

Later traffic drops:

```text
CPU = 20%
   ↓
Auto Scaling
   ↓
Remove S3
```

Back to:

```text
        Load Balancer
          /       \
         ↓         ↓
       S1          S2
```

---

## What metrics can trigger Auto Scaling?

Not only CPU.

Common metrics include:

* **CPU utilization**
* **Memory utilization**
* **Requests per second**
* **Request latency**
* **Queue length**
* **Number of active connections**
* Custom application metrics

For example, for an API:

```text
Requests/sec > 1000
        ↓
Add instances
```

For a queue-based worker:

```text
Queue length > 10,000
        ↓
Add workers
```

---

## Scale Out + Auto Scaling

This is the most common pattern you'll see:

```text
                   Users
                     ↓
               Load Balancer
                     ↓
              ┌──────┴──────┐
              ↓             ↓
             S1             S2
                     ↑
                     │
                Auto Scaling
                     ↑
                     │
               Monitor Metrics
```

When demand increases:

```text
2 → 3 → 5 → 10 servers
```

When demand decreases:

```text
10 → 5 → 3 → 2 servers
```

That's where **Elasticity + Auto Scaling + Horizontal Scaling** work together.

---

## ⚠️ One important interview distinction

Don't say:

> "Auto Scaling means automatically scaling up."

That's incomplete.

Auto Scaling can mean:

**Scale OUT**

```text
2 servers → 5 servers
```

or **Scale IN**

```text
5 servers → 2 servers
```

And depending on infrastructure, it can also involve **vertical resource changes**.

### Remember:

```text
Scalability
   ↓
Ability to handle more load

Elasticity
   ↓
Ability to dynamically increase/decrease capacity

Auto Scaling
   ↓
Mechanism that automatically performs the adjustment
```

### Next after Auto Scaling:

**Bottleneck Identification** 🔥

This is very important because before saying *"Let's add more servers"*, an interviewer may ask:

> **"How do you know the server is actually the problem?"**

That's where bottleneck identification comes in.
-----

Perfect bro 🔥 Let's do **Bottleneck Identification**.

# 5. Bottleneck Identification

## First: What is a bottleneck?

A **bottleneck is the component that is limiting the performance of the overall system.**

Think of a water pipe:

```text
Big pipe → Big pipe → SMALL pipe → Big pipe
                         ↑
                    Bottleneck
```

Even if the other pipes are huge, water can only flow as fast as the **small pipe** allows.

Same thing in software.

```text
Users
  ↓
Load Balancer
  ↓
API Servers
  ↓
Database
  ↓
External API
```

If the database is slow:

```text
API Servers → Fast ✅
                    ↓
Database → Slow ❌
                    ↓
              Bottleneck
```

Adding more API servers may **not solve the problem**.

---

# Why is bottleneck identification important?

Imagine the interviewer says:

> "Your application is slow. What will you do?"

A weak answer:

> "I'll add more servers."

❌ Don't do that immediately.

A better answer:

> **"First, I would identify where the bottleneck is using monitoring and performance metrics. Then I would scale or optimize the component responsible for the bottleneck."**

That's the mindset they want.

---

# Where can bottlenecks occur?

There are several common places.

```text
                    Application
                         |
        ┌────────────────┼────────────────┐
        ↓                ↓                ↓
       CPU              RAM              Disk
        |
        ↓
      Network
        |
        ↓
     Database
        |
        ↓
   External APIs
```

Let's understand the important ones.

---

## 1. CPU Bottleneck

Suppose:

```text
CPU = 95%
RAM = 40%
Database = Fast
```

CPU is likely the bottleneck.

Typical causes:

* Heavy calculations
* Inefficient algorithms
* Infinite/long loops
* Too much processing
* CPU-intensive operations

Possible solutions:

```text
Optimize code
     ↓
Reduce computation
     ↓
Scale Up
     ↓
Scale Out
```

---

# 2. Memory Bottleneck

Example:

```text
RAM = 98%
CPU = 30%
```

Your application may be consuming too much memory.

Possible causes:

* Memory leaks
* Huge objects
* Large data loaded into memory
* Poor caching strategy
* Too many concurrent operations

Solutions:

```text
Fix memory leak
Reduce memory usage
Optimize code
Increase RAM
Add instances
```

---

# 3. Database Bottleneck ⭐

This is extremely common.

Imagine:

```text
10 API Servers
       ↓
       ↓
       ↓
   DATABASE
      ❌
```

You might have:

```text
API response = 5 ms
Database query = 2 seconds
```

The database is the bottleneck.

### Possible solutions:

* Add indexes
* Optimize SQL queries
* Avoid unnecessary joins
* Connection pooling
* Caching
* Read replicas
* Database scaling
* Partitioning/sharding

We'll study these deeply later.

---

# 4. Network Bottleneck

Example:

```text
API Server
    ↓
Network
    ❌
External Service
```

Maybe your application is fast, but an external API takes:

```text
2 seconds
```

Then increasing your API servers won't necessarily help.

Possible solutions:

* Reduce payload size
* Compression
* Connection reuse
* CDN
* Optimize network calls
* Parallelize independent calls
* Cache responses

---

# 5. External Service Bottleneck

Example:

```text
Your API
   ↓
Payment API
   ↓
3 seconds ❌
```

Your application might be perfectly optimized.

But the external service is slow.

You need to identify that dependency rather than blindly scaling your servers.

---

# 🔥 How do we actually FIND a bottleneck?

This is the important interview part.

We don't just guess.

We monitor metrics.

### Common metrics:

```text
CPU
Memory
Disk I/O
Network
Request rate
Response time
Error rate
Database query time
Queue length
```

Suppose you see:

```text
CPU             30%  ✅
Memory          40%  ✅
Network         20%  ✅
API processing  10ms ✅
DB query       1800ms ❌
```

Pretty obvious:

> **Database is the bottleneck.**

---

# Example interview scenario

Interviewer:

> "Your website has become slow after traffic increased 5x. What will you do?"

### Don't say:

> "Add more servers."

Instead:

### Step 1

Check overall metrics.

```text
Traffic
CPU
Memory
Network
Latency
Errors
```

### Step 2

Find where time is being spent.

```text
Request
  ↓
API = 20ms
  ↓
DB = 1500ms ❌
```

### Step 3

Identify DB as bottleneck.

### Step 4

Investigate why:

```text
Slow query?
Missing index?
Too many queries?
Connection pool exhausted?
Database CPU high?
```

### Step 5

Apply the appropriate solution.

Maybe:

```text
Slow query
    ↓
Optimize query
    ↓
Add index
```

Or:

```text
Read-heavy DB
    ↓
Read Replica
```

Or:

```text
Repeated data
    ↓
Cache
```

---

# 🔥 Very Important Concept: Bottleneck ≠ Always the Most Loaded Component

Suppose:

```text
CPU = 90%
Database = 50%
```

You might think:

> CPU is definitely the bottleneck.

Not necessarily.

Maybe the application is CPU-heavy but still responds quickly, while the database has:

```text
High latency
Connection queue
Slow queries
```

So:

> **Use performance data and request tracing, not just utilization percentages.**

---

# One architecture example

Imagine your system:

```text
                Users
                  ↓
            Load Balancer
                  ↓
          ┌───────┴───────┐
          ↓               ↓
       API 1            API 2
          \               /
           \             /
              Database
                  ↓
              External API
```

Request takes:

```text
Load Balancer = 5ms
API = 20ms
Database = 800ms
External API = 100ms
```

Total ≈ **925ms**

Where is the biggest bottleneck?

👉 **Database**

Adding API servers:

```text
2 API servers
     ↓
20 API servers
```

probably won't make the request significantly faster because:

```text
Database = 800ms ❌
```

---

# 🧠 Interview-ready answer

### ❓ "How do you identify a bottleneck in a system?"

Say:

> **"I would first monitor system and application metrics such as CPU, memory, network, disk I/O, request latency, throughput, error rates, database performance, and queue length. I would then use logs and distributed tracing to identify where the request is spending most of its time. Once the bottleneck is identified, I would optimize or scale that specific component rather than blindly adding resources."**

That's a solid **4-year-level answer**.

---

# One more important concept: Throughput vs Latency

You'll hear these constantly in System Design.

### Latency

**How long does one request take?**

```text
Request → 200 ms → Response
```

### Throughput

**How many requests can the system handle per second?**

```text
1000 requests / second
```

Example:

```text
Latency = 2 seconds ❌
Throughput = 10,000 req/sec ✅
```

A system can have high throughput but still have high latency, so you need to look at both.

We'll come back to this when we do **performance and load testing**.

---

# 🎯 Your mental model

When a system becomes slow:

```text
           SYSTEM IS SLOW
                 ↓
         DON'T SCALE BLINDLY
                 ↓
         MEASURE EVERYTHING
                 ↓
       Find the bottleneck
                 ↓
        ┌────────┴────────┐
        ↓                 ↓
     Optimize          Scale
        ↓                 ↓
     Code/Query       Up/Out
```

### Today's progress:

```text
1. Scale Up / Scale Out          ✅
2. Stateless / Stateful          ✅
3. Elasticity                    ✅
4. Auto Scaling                  ✅
5. Bottleneck Identification     ✅
6. High Availability vs Scaling  ⏭️
```

Next is **High Availability vs Scalability** — and bro, this one is **very important because interviewers love asking:**

> **"If I have 10 servers instead of 1, does that automatically mean my system has High Availability?"**

The answer is **not necessarily**. That's what we'll understand next.
-------
Absolutely bro 🔥 Last concept for today:

# 6. High Availability vs Scalability

This is **very important in interviews** because people often confuse these two.

---

## 1. What is Scalability?

Scalability means:

> **The system can handle increasing workload by adding resources.**

Example:

```text
1,000 users
    ↓
2 servers

Traffic increases
    ↓
100,000 users
    ↓
10 servers
```

The goal is:

> **Handle MORE traffic/load.**

---

# 2. What is High Availability?

High Availability (HA) means:

> **The system remains available and continues to provide service even when some components fail.**

The goal is:

> **Keep the system UP.**

Example:

```text
              Load Balancer
              /           \
             ↓             ↓
          Server 1       Server 2
             ✅             ✅
```

Server 1 crashes:

```text
              Load Balancer
              /           \
             ↓             ↓
          Server 1       Server 2
             ❌             ✅
                            ↑
                       Users continue
```

The application is still available.

---

# 3. The easiest difference

Remember this:

```text
SCALABILITY
     ↓
Can I handle MORE users?

HIGH AVAILABILITY
     ↓
Can I stay UP when something FAILS?
```

Or:

> **Scalability = MORE**

> **Availability = UP**

---

# 4. Does having multiple servers automatically give High Availability?

### ❌ No!

This is a great interview question.

Imagine:

```text
              Load Balancer
                   ↓
              ┌─────────┐
              │ Switch  │
              └────┬────┘
                   ↓
             ┌───────────┐
             │ Server 1  │
             └───────────┘
             ┌───────────┐
             │ Server 2  │
             └───────────┘
```

You have two servers.

Looks good, right?

But suppose both depend on **one database**:

```text
       Server 1 ──┐
                   ↓
               DATABASE
                   ❌
                   ↑
       Server 2 ──┘
```

Database fails.

Both servers become useless.

So:

> **Multiple servers ≠ automatically High Availability.**

---

# 5. High Availability requires eliminating Single Points of Failure

This is the important concept.

### Single Point of Failure (SPOF)

A component whose failure can bring down the entire system.

Example:

```text
Servers
 /    \
↓      ↓
  Database
      ❌
```

One database.

Database fails → entire application fails.

That's a **Single Point of Failure**.

---

# 6. How do we improve High Availability?

We introduce redundancy.

Instead of:

```text
       Database
           |
           ❌
```

we can have:

```text
       Database Primary
             |
             ↓
        Replica
```

Or multiple instances across failure zones:

```text
             Load Balancer
             /           \
            ↓             ↓
        Server 1       Server 2
        Zone A         Zone B
            \           /
             \         /
              Database
```

If Zone A goes down:

```text
             Load Balancer
                    |
                    ↓
                Server 2
                 Zone B
                    ✅
```

The system can continue operating.

---

# 7. Scalability and HA often work together

This is where System Design gets interesting.

Suppose we have:

```text
                 Users
                   ↓
             Load Balancer
              /         \
             ↓           ↓
          Server 1    Server 2
```

This gives us:

### Scalability

We can add:

```text
Server 3
Server 4
Server 5
```

### High Availability

If:

```text
Server 1 ❌
```

Server 2 can continue serving traffic.

So the **same architecture can provide both**.

But they're solving different problems.

---

# 8. Example: Traffic increases

Suppose:

```text
Current:

2 servers
CPU = 90%
```

We add servers:

```text
4 servers
CPU = 50%
```

That's **Scalability**.

---

# 9. Example: Server crashes

Suppose:

```text
Server 1 ❌
```

But:

```text
Server 2 ✅
Server 3 ✅
```

Users continue using the application.

That's **High Availability**.

---

# 10. Here's a very important scenario

Imagine you have:

```text
10 servers
```

But they are all running in the **same physical location**.

Then the entire data center loses power:

```text
Data Center ❌
   |
   ├── Server 1 ❌
   ├── Server 2 ❌
   ├── Server 3 ❌
   ├── ...
   └── Server 10 ❌
```

You had **10 servers**, so you had scalability.

But you didn't necessarily have good **fault tolerance / availability** against a data-center failure.

That's why production architectures often distribute resources across:

* Availability Zones
* Regions, when required
* Multiple database instances
* Multiple network paths

---

# 11. Another important distinction: Availability vs Reliability

You may hear both.

### Availability

> Is the system accessible when users need it?

### Reliability

> Does the system consistently perform correctly over time?

Very simplified:

```text
Availability
     ↓
"Is it UP?"

Reliability
     ↓
"Does it WORK CORRECTLY and consistently?"
```

We'll study reliability much deeper later.

---

# 12. Interview Question 🔥

### ❓ "Does horizontal scaling automatically provide high availability?"

### ⭐ Answer:

> **"Not necessarily. Horizontal scaling adds multiple instances primarily to increase capacity. It can also improve availability if those instances are independent and traffic can be redirected when one fails. However, we need to eliminate other single points of failure, such as the load balancer, database, network, or a single availability zone, to achieve true high availability."**

That's a strong answer.

---

# 13. Interview Question

### ❓ "Can a system be scalable but not highly available?"

### ✅ Yes.

Example:

```text
       10 Servers
           |
           ↓
      Single Database
           ❌
```

You can handle huge traffic with 10 servers.

But if the database goes down:

```text
10 Servers
    ↓
Database ❌
    ↓
Application DOWN
```

So:

> **Scalable ≠ Highly Available**

---

# 14. Can a system be highly available but not highly scalable?

### ✅ Yes.

Imagine:

```text
        Load Balancer
         /        \
        ↓          ↓
      S1           S2
```

Both servers are redundant.

If one fails, the other works.

That's some level of HA.

But suppose traffic grows massively and you can't add more capacity.

Then:

```text
Availability ✅
Scalability ❌
```

So again, they're independent properties.

---

# 🧠 Final comparison

|                   | Scalability           | High Availability                  |
| ----------------- | --------------------- | ---------------------------------- |
| Main goal         | Handle more load      | Stay available                     |
| Main question     | "Can we handle more?" | "Can we survive failures?"         |
| Typical technique | Scale Up / Scale Out  | Redundancy / Failover              |
| Load Balancer     | Helps                 | Helps                              |
| Multiple servers  | Helps                 | Helps                              |
| Replication       | Can help              | Very important                     |
| Multiple AZs      | Not required          | Often important                    |
| Removes SPOF      | Not necessarily       | Yes                                |
| Example           | 2 → 10 servers        | Server 1 fails, Server 2 continues |

---

# 🔥 One architecture showing BOTH

This is the kind of architecture you should start recognizing in interviews:

```text
                         USERS
                           |
                           ↓
                    ┌─────────────┐
                    │Load Balancer│
                    └──────┬──────┘
                           |
              ┌────────────┼────────────┐
              ↓            ↓            ↓
           Server 1     Server 2     Server 3
              |            |            |
              └────────────┼────────────┘
                           ↓
                     ┌──────────┐
                     │  Redis   │
                     └──────────┘
                           |
                           ↓
                  ┌────────────────┐
                  │    Database    │
                  │ Primary/Replica│
                  └────────────────┘
```

### Scalability:

```text
Server 1
Server 2
Server 3
    ↓
Add Server 4, 5, 6...
```

### High Availability:

```text
Server 1 ❌
    ↓
Server 2 / 3 continue

Database Primary ❌
    ↓
Replica takes over
```

---

# 🎯 Today's entire lesson

You now have the foundation:

```text
1. Scale Up / Scale Out
       ↓
2. Stateful / Stateless
       ↓
3. Elasticity
       ↓
4. Auto Scaling
       ↓
5. Bottleneck Identification
       ↓
6. High Availability vs Scalability
```

And the **one mental model** I'd keep:

```text
                 SYSTEM
                   |
       ┌───────────┼───────────┐
       ↓           ↓           ↓
   Scalability  Elasticity     HA
       ↓           ↓           ↓
   Handle MORE   Adjust       Stay UP
     LOAD       capacity     after failure
```

### ⭐ If you can explain these 6 concepts in your own words, you're ready for the next level:

**Distributed Systems → IPC → RPC → Networking → Load Balancer.**

And now when we reach Load Balancer, you'll understand **why it exists**, not just memorize what it does.

--------


---------

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






