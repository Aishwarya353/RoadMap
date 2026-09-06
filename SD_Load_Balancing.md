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

----

Exactly bro 😎. Let's continue with **Health Checks**, because this is the mechanism that makes the previous API2-crash scenario work.

# 2. Health Checks

### Simple definition

> **A health check is a periodic request made by the infrastructure to determine whether an application instance is healthy enough to receive traffic.**

Think:

```text
Load Balancer
     |
     | "Are you alive?"
     v
   API1 → 200 OK ✅
   API2 → 200 OK ✅
   API3 → 500 ❌
```

The load balancer then does:

```text
API1 ✅ ──┐
API2 ✅ ──┼── Receive traffic
API3 ❌ ──┘
```

---

# 3. How does this work in ASP.NET Core?

Your application can expose a health endpoint:

```http
GET /health
```

For example:

```csharp
builder.Services.AddHealthChecks();

var app = builder.Build();

app.MapHealthChecks("/health");
```

Now:

```text
https://my-api.com/health
```

might return:

```text
200 OK
```

when the application is healthy.

---

# 4. What does Azure do?

Suppose you have:

```text
                    Azure
                      |
              Load Balancing Layer
                /      |      \
               ↓       ↓       ↓
             API1    API2    API3
```

Azure periodically checks:

```text
/health
```

on the instances.

Example:

```text
API1 → /health → 200 ✅
API2 → /health → 200 ✅
API3 → /health → 500 ❌
```

After the configured failure threshold, API3 can be taken out of rotation.

So:

```text
             Traffic
                |
                v
          Load Balancer
            /        \
           v          v
         API1        API2

         API3 ❌
```

---

# 5. But what should `/health` actually check?

This is an important enterprise question.

A basic health check might only tell you:

> "Is my ASP.NET Core process running?"

But your application might be running while the database is unavailable.

For example:

```text
API3
 |
 +--> Application ✅
 |
 +--> Azure SQL ❌
```

If `/health` only checks the application process, it might still return:

```text
200 OK
```

even though requests will fail.

So enterprise applications often have different levels of health checks.

### Liveness

> **"Is my application alive?"**

```text
ASP.NET Core process
        ↓
       YES
        ↓
       200
```

### Readiness

> **"Am I ready to receive traffic?"**

It might check important dependencies:

```text
API
 |
 +--> Database
 +--> Redis
 +--> Required services
```

If a critical dependency is unavailable, the application may be considered **not ready** for certain workloads.

---

# 6. Don't make health checks too heavy 🚨

This is a common mistake.

Don't create:

```text
/health
   ↓
50 database queries
   ↓
10 external APIs
   ↓
Huge processing
```

because the infrastructure may call the health endpoint frequently.

You'd accidentally create:

```text
Load Balancer
    ↓
Health checks
    ↓
Database 🔥
```

Your health check itself becomes a bottleneck.

Keep health checks **fast and purposeful**.

---

# 7. Failure scenario

Let's say:

```text
API1 🟢
API2 🟢
API3 🟢
```

Traffic:

```text
Request 1 → API1
Request 2 → API2
Request 3 → API3
```

Now API2 crashes:

```text
API1 🟢
API2 💀
API3 🟢
```

Health check:

```text
API2 → /health
        ↓
      FAIL
        ↓
Load-balancing layer marks API2 unhealthy
```

New requests:

```text
Request
   ↓
Load Balancer
   ↓
API1 or API3
```

Existing requests that were already connected to API2 may still fail, depending on the failure and protocol.

---

# 8. What happens when API2 comes back?

Suppose Azure restarts/replaces it:

```text
API1 🟢
API2 🟡 Starting
API3 🟢
```

The platform shouldn't immediately send normal traffic to API2 just because the process started.

It should become healthy:

```text
API2
 ↓
/health
 ↓
200 OK
 ↓
Healthy
 ↓
Added back into rotation
```

Then:

```text
             Load Balancer
            /      |      \
           ↓       ↓       ↓
         API1    API2    API3
          🟢      🟢      🟢
```

---

# 🔥 Now connect this with Auto Scaling

This is where things become interesting.

Traffic increases:

```text
Traffic ↑
   ↓
Auto Scaling
   ↓
Add API4
```

But API4 is initially:

```text
API4 🟡 Starting
```

You don't want:

```text
Load Balancer
      ↓
API4
      ↓
Application still starting ❌
```

Instead:

```text
API4
 ↓
Startup
 ↓
Health check
 ↓
Healthy ✅
 ↓
Load Balancer starts sending traffic
```

So health checks help make **scale-out safer**.

---

# 🎯 Interview question

Suppose you have:

```text
             Load Balancer
             /     |     \
            ↓      ↓      ↓
          API1    API2    API3
```

API2's **ASP.NET Core process is running**, but its **Azure SQL connection is completely down**.

### Question:

Should `/health` return `200 OK` or mark API2 unhealthy?

And more importantly:

> **Would you put the database check inside the health endpoint used by the load balancer? Why or why not?**

Think about it and answer in your own words, bro. This is a **very realistic production/design question**.

----


### Question:

**What should happen to the traffic going to API2, and how does the Load Balancer know that API2 is unhealthy?**

Answer in your own words. Don't worry if it's not perfect — I'll correct it and then we'll go to **health checks**.

----

Yes bro. And your question about the DB check is actually an **important production-design decision**.

## 1. How does Azure perform health checks?

Azure doesn't magically know whether your ASP.NET Core API is healthy.

You give Azure a **health-check endpoint**, for example:

```text
GET /health
```

Then the Azure service periodically sends an HTTP request to that endpoint.

For **Azure App Service**, you enable Health Check and configure the path. App Service periodically pings that path on each instance. If an instance repeatedly fails the configured health criteria, App Service removes it from the load-balancing rotation and continues checking it so it can be added back when healthy. It also uses the health check when scaling out to verify new instances are ready. ([Microsoft Learn][1])

Think:

```text
                 Azure App Service
                       |
                Health Check
                       |
            GET https://API/health
                       |
          +------------+------------+
          |            |            |
          v            v            v
        API1         API2         API3
         200           200          500
          ✅            ✅            ❌
                                   |
                                   v
                            Remove API3
                            from traffic
```

For **Application Gateway**, Azure similarly uses health probes against backend instances and stops sending traffic to unhealthy backends. You can configure custom probes with things such as the URL path, interval, timeout, and acceptable status codes. ([Microsoft Learn][2])

For **Azure Front Door**, Front Door sends HTTP/HTTPS health probes to your configured origins and uses the results to determine which origins are healthy and eligible for routing. ([Microsoft Learn][3])

---

# 2. Should `/health` check the database?

### My answer: **It depends on what you're trying to prove.**

For a production API, I generally want **different health concepts**, rather than one giant `/health` endpoint that checks everything.

For example:

```text
/liveness
/readiness
```

### Liveness

Question:

> "Is my application process alive?"

```text
GET /health/live

ASP.NET Core running?
       |
       v
      YES
       |
      200
```

This should be **very lightweight**.

---

### Readiness

Question:

> **"Can this instance actually serve production requests?"**

Now you can check critical dependencies:

```text
GET /health/ready

          API
           |
     +-----+------+
     |            |
   Redis        Azure SQL
     |            |
    OK           OK
     \            /
      \          /
       v        v
        READY ✅
```

Microsoft's current App Service guidance specifically recommends that the health-check path can poll essential components such as the database, cache, or messaging service so the result represents whether the application is actually healthy. ([Microsoft Learn][4])

So **yes**, a readiness check can include a DB check.

---

# 3. But there's a catch 🚨

Don't do this:

```text
/health
   |
   +--> 20 SQL queries
   +--> Redis
   +--> 5 external APIs
   +--> complicated business logic
```

Because Azure is going to call your health endpoint repeatedly.

You could accidentally create:

```text
Azure
  |
  | Health checks
  ↓
API
  |
  | Health check SQL query
  ↓
SQL 🔥
```

Now your **health check itself is putting unnecessary load on SQL**.

Microsoft also recommends designing the health endpoint specifically for health monitoring and keeping probe load in mind; for Front Door, for example, HEAD probes can reduce origin traffic. ([Microsoft Learn][5])

---

# 4. What I'd do in our .NET application

I'd conceptually have:

```text
                 ASP.NET Core
                      |
          +-----------+-----------+
          |                       |
          v                       v
     /health/live            /health/ready
          |                       |
          v                       v
   App is running?          Critical dependencies?
                                  |
                         +--------+--------+
                         |        |        |
                        SQL     Redis    Messaging
```

### `/health/live`

Very cheap:

```text
Application process?
Configuration loaded?
Basic runtime OK?
```

### `/health/ready`

Checks the **critical dependencies needed to serve requests**.

For example:

```text
SQL        → Can I connect?
Redis      → Can I connect?
Messaging  → Is it available?
```

Not necessarily every external service your application knows about.

---

# 5. Why is this important for scaling?

Imagine Azure adds API4:

```text
API1 ✅
API2 ✅
API3 ✅
API4 🟡 Starting
```

Azure checks:

```text
API4
 ↓
/health/ready
 ↓
SQL ✅
Redis ✅
 ↓
200 OK
 ↓
API4 enters traffic
```

Now API4 is ready.

But suppose:

```text
API4
 |
 +--> Application ✅
 +--> SQL ❌
```

Readiness:

```text
/health/ready
      ↓
SQL unavailable
      ↓
503 ❌
```

Azure keeps API4 out of traffic until it becomes healthy.

That's **much safer than sending users to a broken instance**.

---

# 6. Now let's move forward: Load Balancing Algorithms

We've established:

```text
                 Load Balancer
                       |
              Health Checks
                       |
        +--------------+--------------+
        |              |              |
       API1           API2           API3
        ✅              ✅              ✅
```

The next question is:

> **"Okay, all three are healthy. A request arrives. Which one should receive it?"**

That's where **load-balancing algorithms** come in.

---

## Round Robin

The simplest idea:

```text
Request 1 → API1
Request 2 → API2
Request 3 → API3
Request 4 → API1
Request 5 → API2
Request 6 → API3
```

Like taking turns:

```text
       Load Balancer
            |
    +-------+-------+
    |       |       |
   API1    API2    API3

    1       2       3
    ↑               |
    +---------------+
```

### Why is it useful?

If your instances are roughly equal:

```text
API1 = same capacity
API2 = same capacity
API3 = same capacity
```

Round Robin is simple and effective.

---

## But here's the problem

Suppose:

```text
API1 → request takes 10 seconds
API2 → request takes 100 ms
API3 → request takes 100 ms
```

Round Robin doesn't necessarily understand that API1 is currently struggling.

You could get:

```text
API1 🔥🔥🔥
API2 😎
API3 😎
```

That's why other strategies exist.

We'll next cover:

### **Round Robin vs Least Connections vs IP Hash vs Session Affinity**

And this will connect directly to your earlier question:

> **"If the same user goes to different servers, how does the application remember them?"**

----

Ahhh yes bro — now I understand exactly what you're asking. 🔥

You're asking:

If /health fails → Azure removes the instance. But if a normal request like /api/employees fails with 500/503, does Azure automatically say "API2 is bad" and stop sending traffic to API2?

Short answer: Normally, NO.

A normal request failure is not automatically treated as a health-check failure.

That's a very important distinction.

Think of these as two separate channels
                    Load Balancer
                         |
             +-----------+-----------+
             |                       |
       Health Check              User Traffic
             |                       |
             ↓                       ↓
        /health                 /api/orders
             |                       |
             ↓                       ↓
          API2                    API2

Health check
GET /health
       ↓
    503 ❌
       ↓
Infrastructure says:
"API2 is unhealthy"
       ↓
Remove API2

Normal request
GET /api/orders
       ↓
    503 ❌
       ↓
Response returned to user
       ↓
API2 is NOT necessarily removed


The load balancer generally doesn't say:

"One request failed, therefore API2 is dead."

Because a request can fail for many reasons that have nothing to do with the instance being unhealthy.

Why wouldn't it remove API2?

Imagine:

API1 🟢
API2 🟢
API3 🟢


User sends:

GET /api/employees/999999


API2 returns:

404 Not Found


Should we remove API2?

Obviously not. 😄

The request failed, but:

API2 = perfectly healthy


Or:

POST /api/orders


returns:

400 Bad Request


Again:

API2 = healthy


Even:

GET /api/employees


might return:

500 Internal Server Error


because of a specific application bug/data problem, while other requests work perfectly.

So the load balancer cannot simply do:

Request failed
     ↓
Remove instance ❌

But what if API2 is REALLY broken?

This is where health checks come back into the picture.

Suppose API2 has a serious problem:

API2
 |
 +-- ASP.NET Core process 🟢
 +-- SQL connection 🔴
 +-- Most API requests failing 🔴


Requests start failing:

Request 1 → API2 → 503
Request 2 → API2 → 503
Request 3 → API2 → 503
Request 4 → API2 → 503


But the load balancer doesn't necessarily remove it just because those requests failed.

Eventually:

Health Check
     ↓
API2 /health/ready
     ↓
503 ❌
     ↓
API2 marked unhealthy
     ↓
Stop sending NEW traffic


So the mechanism is:

              Actual Requests
                    |
              failures happen
                    |
                    v
              Application
                    |
                    | dependency broken
                    v
              Health Check
                    |
                    v
                  FAIL
                    |
                    v
             Load Balancer
                    |
                    v
             Remove instance

Here's the key distinction
Request failure
/api/orders → 500


means:

"This particular request failed."

It does not necessarily mean:

"This server is broken."

Health failure
/health → 503


means:

"This instance should probably not receive traffic."

That's the signal the infrastructure uses for instance-level traffic removal.

What about 100% of requests failing?

Suppose:

API2

Request 1 → 500
Request 2 → 500
Request 3 → 500
Request 4 → 500
Request 5 → 500


Even then, don't assume the load balancer automatically removes API2 based on those responses.

Instead, you design your health/readiness signal so that the underlying problem eventually causes:

/health/ready → 503


Then:

API2
  ↓
Health check fails
  ↓
Load balancer detects unhealthy
  ↓
Remove API2 from rotation

One subtle thing: "stop traffic" doesn't mean kill existing connections

Suppose:

API1 🟢
API2 🔴
API3 🟢


API2 is removed from the load-balancing pool.

That generally means:

NEW requests
     ↓
API1 or API3


It doesn't necessarily mean:

Existing request already connected to API2
                    ↓
                  MAGICALLY
                  MOVED to API1


No.

An existing request/connection can still fail.

The infrastructure can't generally take:

Request currently executing on API2


and magically move its execution state to API1.

🔥 This is the mental model I want you to keep
                    LOAD BALANCER
                         |
              +----------+----------+
              |                     |
              ↓                     ↓
        Health checks          User requests
              |                     |
              ↓                     ↓
        "Is instance           "Process this
          healthy?"              request"
              |                     |
          FAIL?                   FAIL?
              |                     |
              ↓                     ↓
       Remove instance       Return error to user
       from NEW traffic


So:

Health-check failure → instance can be removed from new traffic.

Normal API request failure → normally just return the failure; it does not automatically remove the instance.

Then, if those request failures reflect a genuine instance/dependency problem, your health/readiness check should detect that condition, causing the instance to be removed.


That's where **sticky/session affinity** becomes very interesting.

[1]: https://learn.microsoft.com/he-il/azure/app-service/monitor-instances-health-check?utm_source=chatgpt.com "Monitor the Health of App Service Instances - Azure App Service | Microsoft Learn"
[2]: https://learn.microsoft.com/en-us/azure/application-gateway/application-gateway-components?utm_source=chatgpt.com "Application gateway components | Microsoft Learn"
[3]: https://learn.microsoft.com/en-us/azure/frontdoor/health-probes?utm_source=chatgpt.com "Health Probes - Azure Front Door | Microsoft Learn"
[4]: https://learn.microsoft.com/en-us/azure/well-architected/service-guides/app-service-web-apps?utm_source=chatgpt.com "Architecture Best Practices for Azure App Service (Web Apps) - Microsoft Azure Well-Architected Framework | Microsoft Learn"
[5]: https://learn.microsoft.com/en-us/azure/frontdoor/best-practices?utm_source=chatgpt.com "Best Practices - Azure Front Door | Microsoft Learn"


-----


😂 Bro, absolutely. And first: you don't have a dumb brain. Load balancing has a lot of small concepts that sound similar, so I'll explain it slowly, visually, and with real examples.

No jumping ahead. We'll build it piece by piece.

4. Load-Balancing Algorithms

We currently have:

                    Load Balancer
                         |
             +-----------+-----------+
             |           |           |
             ↓           ↓           ↓
           API 1       API 2       API 3
             🟢          🟢          🟢


All 3 APIs are healthy.

Now a request comes:

GET /api/employees


The load balancer has to answer one question:

"Which API should I send this request to?"

That's what a load-balancing algorithm decides.

Think of the algorithm as the rule used by the load balancer to choose a server.

4.1 Round Robin

Let's start with the easiest one.

Imagine you have 3 friends:

API1
API2
API3


And requests arrive one after another:

Request 1
Request 2
Request 3
Request 4
Request 5
Request 6


Round Robin simply says:

"Take turns."

So:

Request 1 → API1
Request 2 → API2
Request 3 → API3

Request 4 → API1
Request 5 → API2
Request 6 → API3


That's literally the basic idea.

Visual
                    Load Balancer
                         |
                         |
       R1 ──────────────→ API1
       R2 ──────────────→ API2
       R3 ──────────────→ API3
       R4 ──────────────→ API1
       R5 ──────────────→ API2
       R6 ──────────────→ API3


So the pattern is:

1 → 2 → 3 → 1 → 2 → 3 → 1 → 2 → 3


Very simple.

Why is it called "Round Robin"?

Imagine 3 people standing in a circle:

       API1
      /    \
     /      \
  API3 ---- API2


You give the first task to API1.

Then API2.

Then API3.

Then go back around:

API1 → API2 → API3 → API1 → API2 → API3


Hence:

Round Robin = take turns.

Now let's use a real example

Suppose Angular sends 6 requests:

Angular
   |
   | R1
   | R2
   | R3
   | R4
   | R5
   | R6
   ↓
Load Balancer


The load balancer does:

R1 → API1
R2 → API2
R3 → API3
R4 → API1
R5 → API2
R6 → API3


So roughly:

API1 → 2 requests
API2 → 2 requests
API3 → 2 requests


Seems great, right?

Usually yes, if the servers are similar and requests have similar workloads.

But here's where it gets interesting.

🚨 Problem with Round Robin

Imagine this:

API1 → powerful server 💪
API2 → medium server
API3 → weak server 🥲


Round Robin doesn't necessarily care.

It may still do:

R1 → API1
R2 → API2
R3 → API3
R4 → API1
R5 → API2
R6 → API3


Each gets roughly the same number of requests.

But that doesn't necessarily mean the same amount of work.

Another problem: requests can take different amounts of time

Imagine:

Request 1 → takes 10 seconds
Request 2 → takes 100 ms
Request 3 → takes 100 ms


Round Robin might send:

API1 ← Request 1 🔥 (10 sec)
API2 ← Request 2 😎
API3 ← Request 3 😎


Then more requests arrive:

R4 → API1
R5 → API2
R6 → API3


API1 might still be processing the huge request:

API1 🔥🔥🔥
   |
   └── R1 still running


but Round Robin doesn't necessarily say:

"Hmm, API1 is currently busy, let's give R4 to API2."

That's the weakness.

This leads us to the next algorithm
Least Connections

Instead of asking:

"Whose turn is it?"

we ask:

"Which server currently has the fewest active connections?"

For example:

API1 → 10 active connections
API2 → 3 active connections
API3 → 7 active connections


New request arrives:

                New Request
                     |
                     ↓
              Load Balancer
                     |
          Which has least?
                     |
              API2 = 3 ✅
                     |
                     ↓
                   API2


So:

Round Robin:
"Whose turn is it?"

Least Connections:
"Who is currently least busy?"


🔥 That difference is the important part.

Don't worry about memorizing yet

Just remember this:

Round Robin
Take turns.

API1 → API2 → API3 → API1 → API2 → API3

Least Connections
Look at current connections.

API1 = 10
API2 = 3   ← choose this
API3 = 7

One tiny interview question for you

Suppose we have:

API1 → 5 active connections
API2 → 2 active connections
API3 → 8 active connections


A new request arrives.

If we're using Least Connections, which API gets the request?

Just answer API1, API2, or API3. 😎
