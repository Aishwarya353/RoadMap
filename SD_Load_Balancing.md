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

-----

Absolutely bro 😎. Let's go **deep on Least Connections**, but keep it practical for our **ASP.NET Core + Azure** architecture.

 # Least Connections

 We already know Round Robin:

```
Request 1 → API1
Request 2 → API2
Request 3 → API3
Request 4 → API1
```

 It basically asks:

 > **"Whose turn is it?"**

 Least Connections asks a different question:

 > **"Which server currently has the fewest active connections?"**

---

 ## 1\. Basic idea

 Suppose we have:

```
                 Load Balancer
                /      |      \
               ↓       ↓       ↓
             API1    API2    API3
```

 Current connections:

```
API1 → 10 connections
API2 →  3 connections
API3 →  7 connections
```

 A new request arrives:

```
             New Request
                  |
                  ↓
           Load Balancer
                  |
        Check active connections
                  |
       +----------+----------+
       |          |          |
      10          3          7
      API1       API2       API3
                  ↑
                least
```

 So:

```
New Request → API2
```

 Because:

```
3 < 7 < 10
```

 That's the entire basic concept.

---

 # 2\. Let's see it step by step

 Initially:

```
API1 → 2 connections
API2 → 5 connections
API3 → 3 connections
```

 New request arrives.

 Least:

```
API1 = 2 ← lowest
```

 Therefore:

```
Request → API1
```

 Now connections become:

```
API1 → 3
API2 → 5
API3 → 3
```

 Another request arrives.

 Now:

```
API1 → 3
API2 → 5
API3 → 3
```

 There is a tie between API1 and API3.

 The actual tie-breaking behavior depends on the implementation.

 Conceptually, the load balancer chooses one of the least-loaded candidates.

 For example:

```
Request → API3
```

 Now:

```
API1 → 3
API2 → 5
API3 → 4
```

 Next request:

```
API1 → 3 ← lowest
```

 So:

```
Request → API1
```

---

 # 3\. Why is this better than Round Robin sometimes?

 This is where it becomes interesting.

 Imagine:

```
API1 → 1 active request
API2 → 8 active requests
API3 → 2 active requests
```

 Round Robin doesn't necessarily care.

 It might say:

```
Next turn → API2
```

 So:

```
API2 🔥🔥🔥🔥🔥🔥🔥🔥
```

 Least Connections says:

```
API1 = 1
API2 = 8
API3 = 2

Choose API1
```

 That's useful when requests have **different processing times**.

---

 # 4\. Real-world ASP.NET Core example

 Suppose Angular is calling:

```
GET /api/reports/monthly
```

 This request is expensive.

 It takes:

```
10 seconds
```

 Meanwhile:

```
GET /api/employees
```

 takes:

```
50 ms
```

 Imagine:

```
API1
 └── /api/reports/monthly
      running for 10 sec 🔥

API2
 └── idle 😎

API3
 └── idle 😎
```

 If another request arrives, Least Connections can favor the less-connected instances rather than simply following a fixed rotation.

 This can help distribute **concurrent workload** more effectively.

---

 # 5\. Important: Connection ≠ request

 🔥 **This is a very important distinction.**

 People often say:

 > "Least Connections sends the request to the server with the fewest requests."

 That's not necessarily accurate.

 It's generally about **active connections**, depending on the load-balancing implementation and protocol.

 For example:

```
API1 → 10 active connections
API2 → 2 active connections
API3 → 7 active connections
```

 The algorithm sees roughly:

```
API1 = 10
API2 = 2 ← choose
API3 = 7
```

 It isn't simply maintaining:

```
API1 processed 100 requests
API2 processed 80 requests
API3 processed 120 requests
```

 Those are historical request counts, which are a different thing.

---

 # 6\. What is an "active connection"?

 At a simplified level, think:

```
Client
   |
   | connection
   ↓
API1
```

 If the connection remains active, it contributes to the connection count.

 For example:

```
API1

Client A ───────┐
Client B ───────┤
Client C ───────┤
Client D ───────┘

4 active connections
```

 So:

```
API1 = 4
```

 Another server:

```
API2

Client E ───────┐
Client F ───────┘

2 active connections
```

 Therefore:

```
New connection → API2
```

---

 # 7\. Why connection duration matters

 Imagine two APIs:

```
API1 → requests finish very quickly
API2 → requests take a long time
```

 Suppose:

```
API1 → 2 active connections
API2 → 5 active connections
```

 Least Connections will tend to favor API1.

 As API2's long-running requests finish:

```
API2
5
↓
4
↓
3
↓
2
```

 Its connection count changes dynamically.

 That's why Least Connections can adapt to changing workload.

 Round Robin doesn't have that information.

---

 # 8\. Let's compare them directly

 Suppose:

```
API1 → 2 active connections
API2 → 10 active connections
API3 → 5 active connections
```

 ### Round Robin

 It might simply follow:

```
API1 → API2 → API3 → API1 → ...
```

 It doesn't inherently choose based on current connection count.

 ### Least Connections

 It looks at:

```
API1 = 2
API2 = 10
API3 = 5
```

 and chooses:

```
API1
```

 So the mental difference is:

```
Round Robin
      ↓
Fixed turn-taking

Least Connections
      ↓
Current connection count
```

---

 # 9\. But Least Connections is NOT magic

 This is another important interview point.

 Suppose:

```
API1 → 2 connections
API2 → 2 connections
API3 → 2 connections
```

 All equal.

 Least Connections doesn't magically know:

```
API1 CPU = 20%
API2 CPU = 90%
API3 CPU = 30%
```

 unless the specific load-balancing mechanism has additional load information.

 It is primarily using its defined connection-based metric.

 So:

```
2 connections ≠ automatically "least CPU"
```

 For example:

```
API1
2 connections
but each is doing huge work 🔥

API2
5 connections
but each is tiny 😎
```

 A pure connection-count algorithm might still prefer API1.

---

 # 10\. What if one server is more powerful?

 Suppose:

```
API1 → 8 CPU cores
API2 → 4 CPU cores
API3 → 2 CPU cores
```

 But the load balancer sees:

```
API1 → 5 connections
API2 → 5 connections
API3 → 5 connections
```

 Pure Least Connections sees:

```
5 = 5 = 5
```

 It doesn't automatically understand that API1 is twice as powerful as API3.

 That's why production load balancing can involve things like:

 - weights
- health status
- connection counts
- latency
- capacity
- routing policies

 depending on the technology.

---

 # 11\. What happens when an instance becomes unhealthy?

 This connects to what we already learned.

 Suppose:

```
API1 🟢 → 2 connections
API2 🟢 → 5 connections
API3 🔴 → 1 connection
```

 Someone might say:

 > "API3 has the fewest connections, so send traffic there!"

 No.

 Health status comes first.

 Conceptually:

```
             Load Balancer
                  |
          Is instance healthy?
                  |
        +---------+---------+
        |         |         |
       API1      API2      API3
        🟢        🟢        🔴
        |         |
        +---------+
              |
        Least Connections
              |
       API1 vs API2
```

 So:

```
API3 = unhealthy
       ↓
excluded from eligible pool
       ↓
Least Connections chooses among
healthy instances
```

 This is a very important mental model:

 > **The algorithm chooses among eligible/healthy backends; an unhealthy backend isn't normally a candidate simply because it has fewer connections.**

---

 # 12\. What happens when API2 crashes?

 Suppose:

```
API1 🟢
API2 🔴
API3 🟢
```

 Health check detects:

```
API2 → /health → failure
```

 Then:

```
API2
 ↓
unhealthy
 ↓
removed from eligible traffic
```

 Now Least Connections operates on:

```
API1
API3
```

 For example:

```
API1 → 8 connections
API3 → 3 connections
```

 New request:

```
             New Request
                  ↓
           Load Balancer
                  ↓
       API1 = 8    API3 = 3
                         ↑
                       choose
```

 So:

```
New Request → API3
```

---

 # 13\. What about a new instance?

 This becomes very important with **horizontal scaling**.

 Suppose we have:

```
API1 → 10 connections
API2 → 8 connections
API3 → 7 connections
```

 Azure scales out:

```
API4 🟡 Starting
```

 While API4 is starting:

```
API4 → not ready
```

 It shouldn't immediately receive normal traffic.

 After:

```
API4
 ↓
startup
 ↓
health/readiness check
 ↓
healthy
```

 it becomes eligible.

 Then:

```
API1 → 10
API2 → 8
API3 → 7
API4 → 0
```

 If Least Connections is being used, API4 may receive new connections because:

```
0 < 7 < 8 < 10
```

 That's actually one reason health/readiness and load balancing work together so nicely.

---

 # 14\. Now let's hit an important limitation

 Imagine:

```
API1 → 2 connections
API2 → 10 connections
```

 But API1's two connections are:

```
2 huge 30-minute operations 🔥🔥
```

 and API2's ten connections are:

```
10 tiny operations 😎
```

 Least Connections sees:

```
API1 = 2
API2 = 10
```

 and may choose API1.

 So:

 > **Least Connections is better than simple Round Robin for some workloads, but it is still only a proxy for "load."**

 That's an excellent interview insight.

---

 # 15\. Now let's connect this to HTTP/1.1 and HTTP/2

 This gets slightly more advanced, but it's worth understanding.

 With modern HTTP, one network connection can potentially carry multiple requests.

 For example, HTTP/2 supports multiplexing:

```
Client
  |
  | one connection
  |
  +---- Request A
  +---- Request B
  +---- Request C
  +---- Request D
  |
 API
```

 So:

```
1 connection
≠
1 request
```

 This is why you should be careful when casually saying:

 > "Least Connections means the server with the fewest requests."

 It doesn't.

 The exact behavior depends on the layer and implementation.

---

 # 16\. The big mental model

 I want you to remember this picture:

```
                    New Request
                         |
                         ↓
                  Load Balancer
                         |
                Remove unhealthy
                   instances
                         |
                         ↓
             +-----------+-----------+
             |           |           |
            API1        API2        API3
             🟢          🟢          🟢
             |           |           |
             8           3           6
          connections
             |
             +-----------+
                         |
                         ↓
                 Choose lowest
                         |
                         ↓
                       API2
```

 So the process is roughly:

```
Request arrives
      ↓
Which backends are healthy?
      ↓
Remove unhealthy ones
      ↓
Look at connection count
      ↓
Choose least-connected backend
      ↓
Forward traffic
```

---

 # 17\. Interview answer

 If they ask:

 ### "What is Least Connections?"

 You can say:

 > **"Least Connections is a load-balancing strategy that directs a new connection toward the eligible backend with the fewest active connections. It's useful when requests or connections have varying durations because it can adapt to the current distribution of concurrent connections, unlike basic Round Robin."**

 That's a strong answer.

 If they ask:

 ### "Is Least Connections always better than Round Robin?"

 Say:

 > **"No. It depends on the workload and implementation. Round Robin is simple and works well when instances have similar capacity and request durations. Least Connections can be more suitable when connection durations vary significantly, but connection count is still only an approximation of actual server load."**

 🔥 That's the level I'd want you to reach for interviews.

---

 ## One last scenario before we move on

 Suppose:

```
API1 → 2 connections
API2 → 5 connections
API3 → 8 connections
```

 A new request arrives.

 **Least Connections chooses API1.**

 But immediately after that:

```
API1 → 3
API2 → 5
API3 → 8
```

 Then another request arrives.

 **Which API would Least Connections prefer now?**

 And here's the slightly harder part:

 > If API1's 3 connections are extremely expensive database/reporting operations, while API2's 5 connections are tiny requests, is Least Connections guaranteed to choose the truly "least busy" server?

 Answer those two, and then we'll move to **IP Hash**.


 --------

 Exactly bro 🔥 — **API1 is still the preferred one** in that simplified example because:

```
API1 = 3 connections
API2 = 5 connections
API3 = 8 connections

3 < 5 < 8
```

 And your second point is also important:

 > **No, Least Connections is NOT guaranteed to choose the server that is actually doing the least work.**

 It only knows the metric it's designed to use: **connection count**.

 Now let's clear up your HTTP/1.1, HTTP/2, multiplexing, and HTTPS confusion before moving to IP Hash.

 # 1\. First: HTTP vs HTTPS

 This is actually very simple.

 **HTTP** and **HTTPS** are not competing versions.

 Think:

```
HTTP = application protocol
HTTPS = HTTP + TLS encryption
```

 So these are possible:

```
HTTP/1.1
HTTPS using HTTP/1.1

HTTP/2
HTTPS using HTTP/2

HTTP/3
HTTPS using HTTP/3
```

 The `S` in HTTPS basically means the HTTP communication is protected by **TLS**.

 So when I said:

```
HTTP/1.1
HTTP/2
```

 I was talking about **versions of HTTP**, not saying you should use unencrypted HTTP.

 In your enterprise Angular + Azure application, you'll normally see:

```
Angular
   |
   | HTTPS
   ↓
Azure
   |
   | HTTPS
   ↓
ASP.NET Core
```

 The underlying HTTP version could be HTTP/1.1 or HTTP/2 depending on the connection and configuration.

---

 # 2\. What is HTTP/1.1?

 Let's start from the old/simple model.

 Imagine Angular needs to make requests:

```
GET /api/employees
GET /api/departments
GET /api/orders
```

 Conceptually, with a connection:

```
Client
  |
  | Request 1
  ↓
Server
  |
  | Response 1
  ↓
Client
  |
  | Request 2
  ↓
Server
  |
  | Response 2
```

 A connection can be reused with HTTP/1.1, so it's **not correct** to think "every request always creates a brand-new TCP connection."

 But HTTP/1.1 has an important limitation compared with HTTP/2:

 ### HTTP/1.1 does not multiplex multiple HTTP requests concurrently over the same connection in the same way HTTP/2 does.

 You can use multiple connections:

```
Client
  |
  +---- Connection 1 ----> Server
  |
  +---- Connection 2 ----> Server
  |
  +---- Connection 3 ----> Server
```

 Browsers commonly use multiple connections to improve parallelism.

---

 # 3\. Then HTTP/2 comes along

 HTTP/2 introduced **multiplexing**.

 This is the important word.

 ## Multiplexing = multiple requests/responses can share one connection concurrently.

 Imagine one highway.

 ### Without multiplexing

 You have:

```
Connection
    |
    +---- Request A
    |
    +---- Response A
    |
    +---- Request B
    |
    +---- Response B
```

 ### With HTTP/2 multiplexing

 You can have:

```
                 ONE connection
                       |
        +--------------+--------------+
        |              |              |
     Request A      Request B      Request C
        |              |              |
     Response A     Response B     Response C
```

 All of them travel through the **same underlying connection**.

 That's multiplexing.

---

 # 4\. Real-world analogy

 Imagine a road.

 ### HTTP/1.1-ish mental model

```
ONE LANE

🚗 Request A
🚗 Response A
🚗 Request B
🚗 Response B
🚗 Request C
🚗 Response C
```

 ### HTTP/2

```
MULTIPLE LANES INSIDE ONE HIGHWAY CONNECTION

🚗 Request A ────────┐
🚙 Request B ────────┼── ONE connection
🚕 Request C ────────┤
🚌 Request D ────────┘
```

 They're logically separate streams but share the underlying connection.

---

 # 5\. Why does this matter for Least Connections?

 🔥 **This is the important connection to our previous discussion.**

 Suppose:

```
API1 → 1 connection
API2 → 5 connections
```

 With HTTP/2, that single connection to API1 could potentially be carrying:

```
API1
 |
 +-- Request A
 +-- Request B
 +-- Request C
 +-- Request D
 +-- Request E
```

 So:

```
API1 = 1 connection
```

 does **not necessarily mean**:

```
API1 = 1 request
```

 It could be:

```
API1 = 1 connection
      ↓
      20 concurrent streams
```

 That's why I told you:

 > Don't interpret "Least Connections" as "fewest requests."

 Connection count and application workload are different things.

---

 # 6\. What is a stream?

 HTTP/2 gives you the concept of a **stream**.

 Very simplified:

```
TCP connection
       |
       +---- Stream 1 → GET /employees
       |
       +---- Stream 2 → GET /orders
       |
       +---- Stream 3 → GET /products
```

 Each HTTP request/response exchange can be associated with a stream.

 So:

```
1 TCP connection
       ↓
multiple HTTP/2 streams
```

 That's multiplexing.

---

 # 7\. Where does HTTPS fit?

 Here's the full picture.

 For a normal secure web application:

```
Angular
   |
   | HTTPS
   |
   | HTTP/2
   ↓
Azure
```

 You can think of the layers approximately like:

```
HTTP/2
  ↓
TLS
  ↓
TCP
  ↓
IP
```

 The TLS layer encrypts the HTTP communication.

 So:

```
HTTPS + HTTP/2
```

 is completely normal.

 In fact, when you browse a modern website, you're very commonly using secure HTTP over TLS.

---

 # 8\. One terminology correction

 It's better to say:

 > **HTTP/2 over TLS**

 rather than thinking:

 > "HTTP/2 versus HTTPS."

 Because they answer different questions.

```
HTTP/1.1 / HTTP/2 / HTTP/3
          ↓
      HTTP version

HTTP vs HTTPS
     ↓
Is the HTTP communication protected with TLS?
```

 So:

```
HTTP/1.1 + TLS = HTTPS using HTTP/1.1
HTTP/2 + TLS   = HTTPS using HTTP/2
```

---

 # 9\. Now let's return to Load Balancing 🔥

 We currently know:

 ### Round Robin

```
API1 → API2 → API3 → API1 → API2 → API3
```

 ### Least Connections

```
Look at current connections.

API1 = 2
API2 = 5
API3 = 8

Choose API1.
```

 But we discovered an important limitation:

```
Connections ≠ actual workload
```

 And now:

 # 10\. IP Hash

 This one is interesting because it changes the question again.

 Round Robin asks:

 > **"Whose turn is it?"**

 Least Connections asks:

 > **"Who has the fewest connections?"**

 IP Hash asks:

 > **"Which backend does this client's IP map to?"**

 Imagine:

```
User A
IP = 10.1.1.50
```

 The load balancer calculates some hash based on the IP:

```
10.1.1.50
     ↓
   HASH
     ↓
   API2
```

 So:

```
User A → API2
```

 Then that user sends another request:

```
User A
   ↓
10.1.1.50
   ↓
 HASH
   ↓
API2
```

 Again:

```
User A → API2
```

 And again:

```
User A → API2
```

 So the basic idea is:

```
              Load Balancer
                   |
              Hash client IP
                   |
       +-----------+-----------+
       |           |           |
      API1        API2        API3
                   ↑
              User A maps here
```

 This can provide a form of **consistent routing** for clients.

---

 # 11\. Why would we want that?

 Suppose your application stores something **locally on API2**:

```
API2
 |
 +-- User session
 +-- In-memory state
```

 If User A always goes to API2:

```
User A
  |
  +---- Request 1 → API2
  |
  +---- Request 2 → API2
  |
  +---- Request 3 → API2
```

 then API2 can find that local state.

 But now we're entering the world of:

 # **Sticky Sessions / Session Affinity**

 And this is a VERY important topic for your ASP.NET Core architecture.

 Because we need to ask:

 > **Should we actually depend on a user always going to the same API instance?**

 The modern answer is often:

 > **Prefer stateless APIs when possible.**

 Instead of:

```
API2
 |
 └── User session stored in RAM
```

 we can use shared storage:

```
             API1
              |
             API2
              |
             API3
              |
              ↓
            Redis
              |
              ↓
        Shared state
```

 Then:

```
User A → API1
User A → API3
User A → API2
```

 and all instances can access the same shared state.

 🔥 **That is the bridge from IP Hash → Sticky Sessions → Stateless ASP.NET Core → Redis.**

 We'll go there next, but first I want you to be 100% clear on one thing:

```
HTTP/1.1
HTTP/2
HTTPS
Multiplexing
```

 ### Your mental model should now be:

```
                 HTTPS
                   |
             HTTP/1.1 or HTTP/2
                   |
            -----------------
            |               |
        HTTP/1.1          HTTP/2
                            |
                      Multiplexing
                            |
                 Multiple streams
                 over one connection
```

 And therefore:

 > **1 connection does not necessarily mean 1 request.**

 That's why **Least Connections ≠ Least Requests ≠ Least CPU**.

---

 ## Next

 We'll now go **deep into IP Hash** with a concrete example:

```
User A → API2
User B → API1
User C → API3

Then API2 crashes...

Where does User A go?
Does the hash change?
What happens to their session?
Why does this lead to Sticky Sessions?
And why do modern stateless APIs often avoid depending on it?
```

 That's the perfect next step. 🚀


 -------

 Exactly bro 🔥 — you've got the key limitation right:

 > **Least Connections is based on active connections, not simply the number of requests.**

 And because **1 connection can carry multiple requests** (especially with HTTP/2), connection count is only an approximation of actual workload.

 Now let's tackle your three questions carefully.

 # 1\. Is IP Hash the same as Consistent Hashing?

 **No. They're related ideas, but they are not the same thing.**

 ### IP Hash

 The basic idea is:

```
Client IP
   ↓
Hash function
   ↓
Backend selection
```

 For example:

```
10.1.1.10 → hash → API1
10.1.1.20 → hash → API3
10.1.1.30 → hash → API2
```

 The goal is basically:

 > **"Clients with the same IP should tend to map to the same backend."**

---

 ### Consistent Hashing

 Consistent hashing is a broader hashing technique designed to make it possible to add/remove nodes while minimizing how much existing data/key-to-node mapping changes.

 Imagine:

```
              Hash Ring

           API1
        /         \
      /             \
   API3             API2
      \             /
        \         /
```

 Keys are hashed onto the ring:

```
UserA → hash → position → API2
UserB → hash → position → API3
UserC → hash → position → API1
```

 If you add another server:

```
API4
```

 consistent hashing tries to minimize remapping.

 So:

```
IP Hash
    ↓
Hash the client IP to choose backend

Consistent Hashing
    ↓
A hashing strategy designed to minimize
remapping when nodes change
```

 They can be used together conceptually, but **IP Hash ≠ Consistent Hashing**.

---

 # 2\. And YES bro — client IP can absolutely differ! 😂

 This is actually a **very important issue**.

 You asked:

 > "Client IP can differ right?"

 **Yes.**

 The IP the load balancer sees may not necessarily be the actual user's device IP.

 Let's say:

```
Your Laptop
IP: 192.168.1.50
       |
       ↓
Home Router
       |
       ↓
Internet
       |
       ↓
Azure
```

 Your laptop's private IP:

```
192.168.1.50
```

 is not normally what the public internet sees.

 Your router performs **NAT**.

 So the server might see a public IP such as:

```
203.x.x.x
```

---

 # 3\. Even more interesting: corporate networks

 Imagine 500 employees:

```
Employee 1 ──┐
Employee 2 ──┤
Employee 3 ──┤
Employee 4 ──┤
              ↓
        Corporate NAT
              ↓
        Public IP
              ↓
           Azure
```

 The load balancer might see:

```
203.100.50.10
```

 for many of those users.

 So:

```
500 users
    ↓
same public IP
    ↓
same hash input
```

 Potentially, many clients could map to the same backend.

 That's one limitation of IP-based routing.

---

 # 4\. Mobile users make this even more interesting

 Suppose:

```
User
  |
  | Wi-Fi
  ↓
Network A
  ↓
Public IP = X
```

 Then they leave home:

```
User
  |
  | Mobile network
  ↓
Network B
  ↓
Public IP = Y
```

 Now:

```
Before:

Hash(X) → API2

After:

Hash(Y) → API1
```

 The user's mapped backend can change.

 So IP-based routing is **not a perfect way of identifying a user**.

---

 # 5\. Proxies/CDNs/load balancers

 Your request may pass through several layers:

```
Browser
   ↓
Corporate Proxy
   ↓
CDN
   ↓
Azure Front Door
   ↓
Application Gateway
   ↓
ASP.NET Core
```

 The backend doesn't simply have one obvious "client IP."

 There can be forwarded client-IP information through headers/proxy mechanisms, but you must understand and correctly configure which proxy is trusted before using such information for security or routing.

 So don't think:

 > "The API always directly sees my laptop's IP."

 It often doesn't.

---

 # 6\. Now let's get to Sticky Sessions 🔥

 This is where the previous concepts connect.

 Suppose:

```
                Load Balancer
               /      |      \
              ↓       ↓       ↓
            API1    API2    API3
```

 User A logs in.

 The first request goes:

```
User A
   ↓
Load Balancer
   ↓
API2
```

 Suppose API2 stores something in its own memory:

```
API2 memory

User A
  |
  +-- Session
  +-- Cart
  +-- Some state
```

 Then User A sends another request.

 If the load balancer sends it to API1:

```
User A
   ↓
Load Balancer
   ↓
API1
```

 API1 says:

 > "Who is User A? I don't have that session in my memory." 😭

 That's the problem sticky sessions solve.

---

 # 7\. What is Session Affinity?

 **Session Affinity** means:

 > **Try to keep requests from the same client/session going to the same backend instance.**

 So:

```
User A
   ↓
Load Balancer
   ↓
API2
```

 Then subsequent requests:

```
User A → API2
User A → API2
User A → API2
```

 rather than:

```
User A → API1
User A → API3
User A → API2
User A → API1
```

 The system tries to maintain the association:

```
User A
   ↕
API2
```

---

 # 8\. Sticky Session = Session Affinity?

 In most conversations, **yes, people use these terms almost interchangeably.**

 You can think:

```
Session Affinity
       =
Sticky Sessions
```

 The idea is:

 > **"Stick this client/session to the same backend."**

---

 # 9\. How does it actually "stick"?

 This is where implementation matters.

 One common mechanism is a **cookie**.

 Imagine the server/load-balancing infrastructure gives the browser something like:

```
Set-Cookie:
    Affinity=API2
```

 Browser stores it:

```
Browser
 |
 +-- Cookie: Affinity=API2
```

 Next request:

```
Browser
   |
   | Cookie: Affinity=API2
   ↓
Load Balancer
   |
   ↓
API2
```

 So the load balancer can use that affinity information to keep routing the client toward API2.

 The exact cookie name and mechanism depend on the Azure service/configuration.

---

 # 10\. IP Hash vs Sticky Session

 This is an important distinction.

 ### IP Hash

 Uses something like:

```
Client IP
   ↓
Hash
   ↓
API2
```

 ### Sticky Session

 Uses an affinity mechanism, commonly:

```
Browser
   ↓
Affinity cookie
   ↓
Load Balancer
   ↓
API2
```

 So:

```
IP Hash
    ↓
Network identity

Sticky Session
    ↓
Session/client affinity
```

 They are **not the same mechanism**.

---

 # 11\. Why would we need sticky sessions?

 Suppose we build a badly designed application:

```
API1
 |
 └── User session stored in RAM

API2
 |
 └── User session stored in RAM

API3
 |
 └── User session stored in RAM
```

 Then:

```
User A → API1
```

 API1 knows the session.

 Next request:

```
User A → API3
```

 API3 doesn't know it.

 So we say:

 > "Let's make User A stick to API1."

 That's session affinity.

---

 # 12\. But here's the BIG enterprise lesson 🚨

 In modern distributed systems, we'd often prefer:

 > **Don't depend on local server memory for important user state.**

 Instead:

```
                API1
                  |
                API2
                  |
                API3
                  |
                  ↓
                Redis
                  |
             Shared State
```

 Now:

```
User A → API1
User A → API3
User A → API2
```

 All instances can access shared state.

 This is much better for horizontal scaling.

---

 # 13\. What about authentication?

 Here's where people sometimes get confused.

 Suppose you're using JWT authentication.

 The token might be:

```
Authorization: Bearer eyJ...
```

 The API can validate the token on **any instance**:

```
User
 |
 +----> API1 → validate token ✅
 |
 +----> API2 → validate token ✅
 |
 +----> API3 → validate token ✅
```

 You don't necessarily need sticky sessions for that.

 That's one reason **stateless authentication** works nicely with load-balanced APIs.

---

 # 14\. Imagine our Angular application

 Our architecture:

```
Angular
   |
   | HTTPS
   ↓
Azure
   |
   ↓
Load Balancer / Routing Layer
   |
   +--------+--------+
   |        |        |
   ↓        ↓        ↓
 API1     API2     API3
   |        |        |
   +--------+--------+
            |
          Redis
```

 Angular sends:

```
GET /api/employees
Authorization: Bearer <token>
```

 Request 1:

```
Angular → API1
```

 Request 2:

```
Angular → API3
```

 Request 3:

```
Angular → API2
```

 That's perfectly fine **if the API is designed to be stateless**.

---

 # 15\. Why sticky sessions can become a problem

 Suppose:

```
API1 🟢
API2 🟢
API3 🟢
```

 User A is stuck to API2:

```
User A → API2
```

 Now API2 crashes:

```
API1 🟢
API2 💀
API3 🟢
```

 What happens?

 The affinity relationship pointing to API2 can't magically keep working.

 The infrastructure needs to route the client to another healthy backend, depending on the service's behavior/configuration.

 And any state that existed **only in API2's memory is gone**.

 That's the fundamental weakness:

```
Sticky session
      +
Local memory state
      ↓
Instance failure
      ↓
State can disappear
```

---

 # 16\. The architecture we generally want

 Instead of:

```
User
  ↓
API2
  ↓
Local RAM
  ↓
Session
```

 we prefer:

```
User
  ↓
Load Balancer
  ↓
Any healthy API
  ↓
Shared state store
  ↓
Redis
```

 Then:

```
Request 1 → API1 → Redis
Request 2 → API3 → Redis
Request 3 → API2 → Redis
```

 The user doesn't care which instance receives the request.

 🔥 That's the beauty of **stateless APIs**.

---

 # 17\. One very important distinction

 Don't confuse:

```
HTTP connection
```

 with:

```
Application session
```

 They're different.

 A user can have:

```
Browser
   |
   | HTTP connection
   ↓
API1
```

 while their application/session state might live in:

```
Redis
```

 And the next request could go:

```
Browser
   |
   ↓
API3
```

 The application session can still exist because it isn't tied to API1's RAM.

---

 # 🎯 Interview answer

 If they ask:

 ### "What is session affinity?"

 Say:

 > **"Session affinity, also called sticky sessions, is a load-balancing mechanism that attempts to route requests from the same client or session to the same backend instance. It's useful for applications that maintain session state locally, but it can reduce flexibility during scaling or instance failures. For horizontally scaled APIs, I generally prefer keeping important state in shared storage such as Redis so requests can be handled by any healthy instance."**

 That's a **very solid enterprise answer**.

---

 # 🔥 And now the flow is becoming clear

```
Least Connections
       ↓
"Choose least-connected backend"
       ↓
IP Hash
       ↓
"Map client identity/IP to backend"
       ↓
Sticky Sessions
       ↓
"Keep this client/session with a backend"
       ↓
Stateless API
       ↓
"Don't depend on a particular backend"
       ↓
Redis / shared storage
       ↓
"Any healthy instance can serve the request"
```

 And **this is exactly why I wanted you to understand these concepts in this order.**

 ### Next in your original list:

 **#7 — Layer 4 vs Layer 7 Load Balancing**

 That's where we'll finally understand things like:

```
TCP
HTTP
HTTPS
IP
Port
URL
Host
Path

Layer 4 → what can it see?
Layer 7 → what can it see?
```

 And then we'll map that directly to:

 **Azure Load Balancer vs Application Gateway vs Front Door.** 🔥
