1. **What is Load Balancing?**
2. **Why do we need it?**
3. **How does a Load Balancer actually work?**
4. **Load-balancing algorithms**

   * Round Robin
   * Least Connections
   * IP Hash
5. **Health Checks**
6. **Session Affinity / Sticky Sessions**
7. **Layer 4 vs Layer 7**
8. **Azure Load Balancer vs Application Gateway vs Front Door**
9. **How Angular → Azure → ASP.NET Core actually flows**
10. **What happens when an API instance crashes?**
11. **How load balancing works with horizontal scaling**
12. **Interview questions + failure scenarios**

Yesss bro 🔥 Let's start **Load Balancing** from zero, but with our enterprise .NET/Azure application in mind.

# 1. What is Load Balancing?

Very simply:

> **A Load Balancer is a component that receives incoming requests and decides which server/instance should handle each request.**

Suppose we have scaled our ASP.NET Core API to 3 instances:

```text
                 Users
                   |
                   |
                   v
             Load Balancer
              /     |     \
             /      |      \
            v       v       v
          API 1   API 2   API 3
```

The user doesn't normally need to know:

```text
"Should I call API1?"
"Should I call API2?"
"Should I call API3?"
```

Instead:

```text
User
  |
  | HTTP Request
  v
Load Balancer
  |
  +----> API 1
  |
  +----> API 2
  |
  +----> API 3
```

The **Load Balancer makes that decision**.

---

# 2. Why do we need it?

This connects directly to **Scale Out**.

Remember:

```text
Scale Out
   ↓
Add more instances
   ↓
API1
API2
API3
```

Now we have a problem:

> **Who distributes the traffic among these instances?**

That's the job of the Load Balancer.

Without one:

```text
Users
  |
  +----------> API1 🔥
  |
  +----------> API1 🔥
  |
  +----------> API1 🔥
  
API2 ─────────> 😴
API3 ─────────> 😴
```

We have 3 servers, but we're not using them properly.

With a load balancer:

```text
                  Users
                    |
                    v
              Load Balancer
              /      |      \
             v       v       v
           API1     API2     API3
```

Traffic can be distributed across them.

---

# 3. Real-world analogy

Imagine a restaurant with **3 counters**.

```text
                 Customers
                     |
                     v
               Receptionist
              /      |      \
             v       v       v
         Counter1 Counter2 Counter3
```

The receptionist says:

> "Counter 1 is busy. Go to Counter 2."

The receptionist is basically acting like a **load balancer**.

The customers don't need to understand how the counters work.

---

# 4. What actually happens to an HTTP request?

Let's say your Angular application calls:

```http
GET /api/employees
```

The flow could be:

```text
Angular
   |
   | HTTPS
   v
Load Balancer
   |
   | decides destination
   v
API 2
   |
   v
ASP.NET Core
   |
   v
Azure SQL
```

The response comes back:

```text
Azure SQL
    |
    v
ASP.NET Core API 2
    |
    v
Load Balancer
    |
    v
Angular
```

The user doesn't necessarily know that **API2** processed the request.

---

# 5. How does the Load Balancer decide?

This is where **load-balancing algorithms** come in.

For example, **Round Robin**:

```text
Request 1 → API1
Request 2 → API2
Request 3 → API3
Request 4 → API1
Request 5 → API2
Request 6 → API3
```

Conceptually:

```text
             Load Balancer
                   |
       +-----------+-----------+
       |           |           |
      API1        API2        API3

R1 → API1
R2 → API2
R3 → API3
R4 → API1
...
```

But real systems can be more sophisticated.

We'll learn:

* Round Robin
* Least Connections
* IP Hash
* Health-based routing
* Session affinity

---

# 6. The REALLY important part: Health Checks

Imagine:

```text
API1 🟢
API2 🟢
API3 🔴
```

API3 has crashed.

If the load balancer blindly distributes traffic:

```text
Request
   ↓
Load Balancer
   ↓
API3 ❌
```

Users start getting failures.

So the load balancer/platform performs **health checks**.

For example, your ASP.NET Core application can expose:

```http
GET /health
```

Response:

```http
200 OK
```

The infrastructure checks:

```text
Load Balancer
     |
     +---- API1 → /health → 200 ✅
     |
     +---- API2 → /health → 200 ✅
     |
     +---- API3 → /health → ❌
```

Then:

```text
API3 ❌
   ↓
Remove API3 from traffic
```

Traffic becomes:

```text
             Load Balancer
              /          \
             v            v
           API1          API2
```

This is where **Load Balancing + High Availability** connect.

---

# 7. Now connect everything we've learned

Our system is becoming:

```text
                         USERS
                           |
                           v
                    Load Balancer
                           |
             +-------------+-------------+
             |             |             |
             v             v             v
           API 1         API 2         API 3
             |             |             |
             +-------------+-------------+
                           |
                 ASP.NET Core Application
                           |
              +------------+------------+
              |                         |
              v                         v
           Redis                    Azure SQL
```

And around the system:

```text
                   Monitoring
                       |
                       v
              Application Insights
```

Traffic increases:

```text
Traffic ↑
   ↓
Auto Scaling
   ↓
API1 → API2 → API3 → API4
   ↓
Load Balancer automatically
distributes traffic
```

API2 crashes:

```text
API1 🟢
API2 🔴
API3 🟢
   ↓
Health Check
   ↓
Load Balancer stops
sending traffic to API2
```

That's the actual enterprise picture.

---

# 🎯 Interview definition

If the interviewer asks:

### "What is a Load Balancer?"

Don't give a huge answer.

Say:

> **"A load balancer distributes incoming network or HTTP traffic across multiple healthy application instances. It helps us use horizontally scaled instances efficiently, improve availability, and prevent a single instance from becoming a bottleneck."**

That's a solid answer.

---

# 🧠 One distinction you MUST understand

**Load Balancer ≠ Auto Scaling**

They work together, but they're different.

### Auto Scaling

Answers:

> **"How many instances should I have?"**

```text
2 → 3 → 4 → 5
```

### Load Balancer

Answers:

> **"Which instance should handle this request?"**

```text
Request
   ↓
API1 / API2 / API3
```

So:

```text
Traffic increases
       ↓
Auto Scaling
       ↓
Add API4
       ↓
Load Balancer
       ↓
Start sending traffic to API4
```

🔥 **This relationship is extremely important for your System Design interviews.**

---

## Your first interview question, bro 👇

Suppose we have:

```text
                 Load Balancer
                /      |      \
               v       v       v
             API1    API2    API3
```

**API2 suddenly crashes.**

### Question:

**What should happen to the traffic going to API2, and how does the Load Balancer know that API2 is unhealthy?**

Answer in your own words. Don't worry if it's not perfect — I'll correct it and then we'll go to **health checks**.
