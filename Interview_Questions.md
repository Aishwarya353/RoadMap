Absolutely bro. These are the **exact practical questions** you should understand. I'll keep each one simple and connect them together.

---

# 1. What is Failover?

**Failover = when the primary component fails, traffic/data processing moves to another healthy component.**

Example:

```text
              Users
                |
                v
          Primary Region
                |
             API 1 ❌
                |
             FAILS
                |
                v
          Secondary Region
                |
             API 2 ✅
```

The user should still be able to use the application.

### Interview answer

> **Failover is the mechanism of switching traffic or processing from a failed primary component to a healthy secondary component to maintain availability.**

For Azure Front Door, for example, health-based routing can send traffic to another healthy origin/region. ([Microsoft Learn][1])

---

# 2. Is Azure Front Door the same as AWS Application Gateway?

**No bro.** This is an important distinction.

Actually, AWS has **Application Load Balancer (ALB)** and **AWS WAF**, while Azure has **Application Gateway**.

The closest conceptual comparison is:

| Azure                         | AWS                                                | Scope    |
| ----------------------------- | -------------------------------------------------- | -------- |
| **Azure Front Door**          | CloudFront + ALB-style global routing capabilities | Global   |
| **Azure Application Gateway** | Application Load Balancer                          | Regional |
| **Azure WAF**                 | AWS WAF                                            | Security |

Azure's own documentation describes Front Door as **global**, while Application Gateway is **regional**. ([Microsoft Learn][2])

So don't memorize:

> Front Door = Application Gateway ❌

Instead:

> **Front Door = global HTTP/S entry/routing**
> **Application Gateway = regional HTTP/S ingress/load balancing**

---

# 3. What does "Ingress" mean?

Easy definition:

> **Ingress is the entry point through which external traffic enters your application/system.**

Imagine your office:

```text
                     Public
                       |
                       v
                  Main Gate
                       |
                       v
                    Office
```

Main Gate = **Ingress**

In Azure:

```text
Internet
   |
   v
Front Door / Application Gateway
   |
   v
Your application
```

So when someone says:

> "Configure the ingress"

they generally mean:

> **Configure how incoming traffic gets into your application.**

Azure specifically describes Front Door and Application Gateway as common HTTP/S ingress services. ([Microsoft Learn][3])

---

# 4. What is CDN?

**CDN = Content Delivery Network.**

Simple example.

Your Angular application has:

```text
main.js
styles.css
logo.png
```

Without CDN:

```text
User in India
      |
      v
Your Azure server in Europe
      |
      v
main.js
```

Every user travels to your origin server.

With CDN:

```text
                  Origin
                    |
                 main.js
                    |
          +---------+---------+
          |                   |
          v                   v
     CDN India            CDN USA
          |                   |
          v                   v
      Indian user         US user
```

The CDN stores/cache static content closer to users.

So:

> **CDN improves performance by serving cacheable content from locations closer to users and reduces load on the origin.**

Azure Front Door itself provides CDN capabilities and can cache content at edge locations. ([Microsoft Learn][4])

For your Angular application, things like:

```text
.js
.css
.png
.jpg
fonts
```

are good candidates for CDN caching.

---

# 5. What is WAF?

**WAF = Web Application Firewall.**

Think of it as a security guard sitting before your application.

```text
Internet
    |
    v
   WAF
    |
    |---- ❌ Malicious request
    |
    v
Application
```

It can help protect against common web attacks such as:

```text
SQL Injection
XSS
malicious HTTP requests
certain bot/abuse patterns
```

Azure WAF can be deployed with both **Application Gateway and Front Door**. ([Microsoft Learn][5])

### Interview answer

> **WAF is a security layer that inspects HTTP/HTTPS traffic and blocks requests matching known malicious patterns before they reach the application.**

Important:

**WAF is not a replacement for application-level security.**

You still need:

```text
Authentication
Authorization
Input validation
Secure coding
```

---

# 6. "Stored Procedure improves performance, then why optimize it?"

🔥 Very good question.

A Stored Procedure can be efficient.

But:

> **Stored Procedure ≠ automatically optimized query.**

Suppose:

```sql
CREATE PROCEDURE GetEmployees
AS
SELECT *
FROM Employee
WHERE DepartmentId = @DepartmentId
```

It might become slow because of:

### Bad/missing indexes

```text
10 million rows
       |
       v
Full table scan 😱
```

### Poor query

```sql
SELECT *
```

when you only need:

```sql
SELECT Id, Name, Department
```

### Blocking

Another transaction may be holding locks.

### Deadlock

Two transactions waiting for each other.

### Parameter sniffing

SQL Server may choose a poor execution plan for certain parameter values.

### Growing data

Maybe:

```text
2024 → 1 million rows
2025 → 5 million
2026 → 20 million
```

A query that was 100 ms before might become 5 seconds.

So:

> **A Stored Procedure is only a container for SQL logic. The SQL inside it still needs optimization.**

---

# 7. Auto Scaling has a delay. What happens during that delay?

🔥 This is a **real production problem**.

Suppose:

```text
Current instances = 2

Traffic suddenly explodes

       ↓

CPU = 90%

       ↓

Autoscale detects it

       ↓

New instance needs to start

       ↓

Instance 3 becomes ready
```

There can be a period where:

```text
Traffic = 🔥🔥🔥🔥🔥
Instances = 2
```

### How do enterprises handle it?

## 1. Keep minimum instances

Instead of:

```text
Min = 1
Max = 10
```

use something like:

```text
Min = 3
Max = 10
```

So you're never starting from zero.

---

## 2. Pre-warmed instances

Azure App Service automatic scaling supports **prewarmed instances**, which act as a buffer so new capacity can be brought into service more smoothly. ([Microsoft Learn][6])

Conceptually:

```text
Running:
API1 API2

Pre-warmed:
API3

Traffic spike
    ↓
API3 quickly becomes available
```

---

## 3. Scale before the traffic arrives

Suppose:

```text
9 AM → traffic increases every day
```

You can schedule:

```text
8:30 AM → 5 instances
```

instead of waiting for CPU to hit 80%.

Azure autoscale supports schedule-based scaling as well as metric-based scaling. ([Microsoft Learn][7])

---

## 4. Use caching

If 100,000 users request the same data:

```text
100,000 requests
       |
       v
      SQL
```

bad.

Instead:

```text
100,000 requests
       |
       v
     Redis
       |
       v
      SQL
```

You reduce pressure on the backend.

---

# 8. What metrics are used for Auto Scaling?

Common ones:

### CPU

```text
CPU > 70%
    ↓
Scale out
```

### Memory

```text
Memory > 80%
    ↓
Scale out
```

### Request count / HTTP traffic

```text
Requests ↑
    ↓
Scale out
```

### Queue length

Very useful for background processing:

```text
Service Bus Queue

100 messages
       ↓
500
       ↓
5000 🚨
       ↓
Scale workers
```

### Custom metrics

For example:

```text
Orders waiting
SRNs waiting
Jobs waiting
Messages/sec
```

Azure Monitor autoscale supports metrics such as CPU, memory, queue length and custom metrics. ([Microsoft Learn][8])

---

# 9. What decides Scale Up vs Scale Out?

This is more of an **architecture decision** than Azure automatically deciding.

### Scale Up

You make **one instance bigger**.

```text
2 CPU / 4 GB

      ↓

8 CPU / 16 GB
```

Use it when:

* the application needs more resources per instance
* the workload doesn't benefit easily from multiple instances
* you have a temporary/simple capacity requirement

---

### Scale Out

You make **more instances**.

```text
       API
    /   |   \
   /    |    \
 API1 API2 API3
```

Usually preferred for highly available web applications because it also provides redundancy.

### Interview answer

> **Scale up increases the capacity of an individual instance, while scale out increases the number of instances. For stateless web APIs, scale out is generally preferred because it provides both additional capacity and redundancy.**

---

# 10. How long does Scale Up vs Scale Out take?

There is **no universal fixed time**.

It depends on:

* Azure service/SKU
* region/capacity
* application size
* container/image size
* startup time
* networking
* configuration
* whether instances are pre-warmed
* current platform conditions

So **don't say "scale out takes exactly 2 minutes" in an interview.**

Conceptually:

### Scale Up

```text
Change SKU
   ↓
Azure provisions larger capacity
   ↓
Application becomes available
```

Potentially requires a resource transition/restart depending on the operation.

### Scale Out

```text
2 instances
     ↓
Azure provisions additional workers
     ↓
New instance starts
     ↓
Application initializes
     ↓
Health checks
     ↓
Traffic can reach it
```

Azure notes that App Service scaling can involve the platform making additional instances available, and automatic scaling can use prewarmed capacity to reduce delays. ([Microsoft Learn][9])

**Interview-safe answer:**

> "I wouldn't assume a fixed duration. I would measure the actual provisioning and application startup time for our Azure SKU and workload. For sudden spikes, I would keep sufficient minimum capacity and use pre-warming or scheduled scaling where appropriate."

That's a **senior-style answer**.

---

# 11. Distributed vs In-Memory

This is important for your Stateful/Stateless understanding.

### In-memory

Data is stored inside the individual application's memory.

```text
API 1
 |
 RAM
 |
UserSession
```

If API1 dies:

```text
API1 ❌
 |
Session ❌
```

Or:

```text
API1 → User state
API2 → Different memory
```

They don't automatically share that memory.

---

### Distributed

State is stored in a **separate shared system** that multiple servers can access.

For example Redis:

```text
API1 ──┐
API2 ──┼──> Redis
API3 ──┘
```

Now:

```text
API1 → Redis → User state
API3 → Redis → Same user state
```

That's distributed/shared state.

---

# 12. Can the same Redis be used across multiple servers?

**Absolutely. That's one of the main reasons you use Redis.**

Example:

```text
             Azure Redis
                 |
       +---------+---------+
       |         |         |
       v         v         v
     API1      API2      API3
```

All three applications connect to the **same Redis resource**.

For example:

```text
API1
Connection String
      |
      v
redis-prod.company.com

API2
Connection String
      |
      v
redis-prod.company.com

API3
Connection String
      |
      v
redis-prod.company.com
```

Then:

```text
API1 → SET User:123 = Nikhil

API3 → GET User:123

Result → Nikhil
```

That's why Redis is useful for distributed session/cache scenarios.

One important distinction:

> **Redis is shared/distributed storage; the ASP.NET Core process memory is local to that particular instance.**

---

# 13. Finally — How do YOU Scale Up / Scale Out your Azure project?

Let's make this **dead simple**.

Assume your project is:

```text
Angular
   |
   v
ASP.NET Core API
   |
   v
Azure SQL
```

and your API is hosted in **Azure App Service**.

## Scale UP

Go to:

```text
Azure Portal
    ↓
App Service
    ↓
Your App
    ↓
App Service Plan
    ↓
Scale up
```

Choose a larger SKU.

Conceptually:

```text
BEFORE

2 CPU
4 GB
1 Instance


        ↓ SCALE UP


AFTER

4 CPU
8 GB
1 Instance
```

You're making the **individual compute instance bigger**. Azure documents scale-up as changing the App Service Plan pricing tier to obtain more CPU/memory/disk/features. ([Microsoft Learn][10])

---

# Scale OUT

Go:

```text
Azure Portal
    ↓
App Service
    ↓
Scale out
```

Change:

```text
Instance count

1 → 3
```

Now:

```text
              App Service
                   |
          +--------+--------+
          |        |        |
          v        v        v
        API1     API2     API3
```

Your code is essentially the **same application**, running three times.

Azure App Service supports increasing the number of VM instances running your application; the available maximum depends on the plan/tier. ([Microsoft Learn][10])

---

# 🧠 What you need to check BEFORE scaling out

This is the part I want you to remember for interviews:

```text
              SCALE OUT
                  |
      +-----------+-----------+
      |           |           |
      v           v           v
  Stateless   Shared data   No local files
      |           |           |
      v           v           v
    JWT        Redis/SQL    Blob Storage
```

Also check:

```text
Database capacity
     ↓
Connection pooling
     ↓
External API limits
     ↓
Health checks
     ↓
Logging/monitoring
```

Because this is possible:

```text
API1 ──┐
API2 ──┤
API3 ──┤
API4 ──┤
API5 ──┤
API6 ──┤
       ↓
    Azure SQL
       🔥
```

You successfully scaled your API...

**but your database became the bottleneck.** 😄

---

## 🔥 Your mental model from now on

Remember this:

```text
SCALE UP
"Make ONE machine stronger"

        API
        ↓
   Bigger machine


SCALE OUT
"Add MORE machines"

        API
       / | \
      /  |  \
    API1 API2 API3


STATELESS
"Don't depend on THIS machine's memory"


REDIS
"Shared place for data that multiple
 application instances need"


FAILOVER
"If this one dies → use another"


INGRESS
"Where traffic enters"


CDN
"Serve cacheable content closer to users"


WAF
"Security guard before the application"


AUTOSCALE
"Azure automatically changes instance count
based on rules/metrics"
```

And **one very important correction to keep in your head**:

```text
Front Door
    ≠
Application Gateway
```

Both can participate in HTTP/S traffic entry, but **Front Door is global** and **Application Gateway is regional**. ([Microsoft Learn][2])

---

### 🎯 Next interview question for you, bro

Your application currently has:

```text
1 ASP.NET Core instance
        |
        v
     Azure SQL
```

Tomorrow you change it to:

```text
3 ASP.NET Core instances
        |
        v
     Azure SQL
```

**Question:**

> A user logs in through API1. The next request goes to API3. What problems can happen, and how would you solve them?

 
 ------


Yes bro. These 5 are worth understanding because they connect **SQL performance + Azure scaling**. Let's do them in easy English.

---

# 1. Why do people say Stored Procedures improve performance?

The common statement is:

> **"Stored procedures are faster than normal queries."**

That's **partly true, but oversimplified**.

A stored procedure can improve performance for several reasons.

### A. SQL Server can reuse execution plans

When SQL Server executes a query, it generally needs to determine an **execution plan**:

```text
SQL Query
   ↓
Parse
   ↓
Optimize
   ↓
Execution Plan
   ↓
Execute
```

For a stored procedure:

```sql
CREATE PROCEDURE GetEmployee
    @EmployeeId INT
AS
BEGIN
    SELECT Id, Name, Department
    FROM Employee
    WHERE Id = @EmployeeId
END
```

SQL Server can cache and reuse an execution plan when appropriate.

So repeated execution can avoid some of the compilation/optimization work.

---

### B. Less network traffic

Suppose your application needs to perform:

```sql
SELECT ...
UPDATE ...
INSERT ...
SELECT ...
```

Instead of sending multiple commands from .NET:

```text
.NET
 ↓
SQL
 ↓
.NET
 ↓
SQL
 ↓
.NET
 ↓
SQL
```

you can sometimes encapsulate the operation:

```text
.NET
  |
  | Execute GetEmployeeDetails
  ↓
SQL Server
  |
  +-- SELECT
  +-- UPDATE
  +-- other operations
  |
  ↓
Result
```

This can reduce application/database round trips.

---

### C. Complex processing can happen close to the data

Instead of:

```text
SQL → lots of data → .NET
                         ↓
                    process data
```

you can sometimes do:

```text
SQL Server
   ↓
Filter / Join / Aggregate
   ↓
Only required data
   ↓
.NET
```

Less data transferred = potentially better performance.

---

### But bro, remember this!

A stored procedure **doesn't automatically make SQL fast**.

This:

```sql
SELECT *
FROM Employee
```

inside a stored procedure can still be terrible if the table has 50 million rows and the query is poorly designed.

So in interviews:

> **Stored procedures can improve performance through execution-plan reuse, reduced round trips, and processing close to the data, but actual performance depends on the SQL, indexes, execution plan, data volume, and workload.**

That's a much better answer.

---

# 2. What is Precompilation and why is it useful?

Think of compilation like this.

Normally:

```text
Source Code
    ↓
Compile
    ↓
Executable
    ↓
Run
```

**Precompilation means doing some compilation work before the application actually needs to run it.**

In .NET, this concept appears in different forms depending on what we're talking about—JIT, ReadyToRun, Native AOT, Angular production builds, etc.

For your **ASP.NET Core application**, don't confuse these concepts.

### Normal .NET execution

Your C# code is compiled into IL:

```text
C#
 ↓
.NET build
 ↓
IL
 ↓
JIT compilation
 ↓
Machine code
 ↓
CPU
```

JIT = **Just-In-Time compilation**.

Some code gets compiled when it is needed.

---

### ReadyToRun

With ReadyToRun, .NET can precompile assemblies to reduce the amount of JIT work needed during startup.

Conceptually:

```text
Normal:

Application starts
      ↓
JIT compilation
      ↓
Application ready


ReadyToRun:

Build time
   ↓
Precompile
   ↓
Deploy
   ↓
Less JIT work at startup
```

### Why useful for scaling?

Remember our autoscaling scenario:

```text
Traffic spike
    ↓
Azure adds API instance
    ↓
New instance starts
    ↓
Application initializes
    ↓
Instance becomes ready
```

If startup takes 30 seconds:

```text
Traffic 🔥
    |
    |---- Instance 3 starting
    |
    |---- Instance 4 starting
```

You have a capacity delay.

Reducing startup/JIT overhead can help new instances become ready faster.

### Interview answer

> **Precompilation moves some compilation work from application startup to build/deployment time, which can reduce startup time and improve cold-start performance.**

But don't say:

> "Precompilation makes every request faster."

Its biggest benefit here is often **startup/cold-start performance**, not magically making all business logic faster.

---

# 3. What is Parameter Sniffing?

This one is **very important for SQL Server interviews**.

Suppose you have:

```sql
CREATE PROCEDURE GetOrders
    @CustomerId INT
AS
SELECT *
FROM Orders
WHERE CustomerId = @CustomerId;
```

Imagine:

```text
Customer 1 → 1,000,000 orders

Customer 999 → 5 orders
```

Huge difference.

When SQL Server first compiles the procedure, it sees a particular parameter value.

For example:

```text
First execution:

@CustomerId = 1

1,000,000 rows
```

SQL Server creates an execution plan optimized for that situation.

```text
@CustomerId = 1
      ↓
Execution Plan A
```

SQL Server may reuse that plan later.

But then:

```text
@CustomerId = 999
      ↓
Only 5 rows
```

The previously cached plan may not be ideal for this very different data distribution.

That's **parameter sniffing**.

### Simple definition

> **Parameter sniffing is when SQL Server uses the parameter values from compilation to create an execution plan, and that cached plan may perform poorly for later executions with different parameter values.**

---

# How do we handle parameter sniffing?

There isn't one universal solution.

Depending on the situation, options include:

### `OPTION (RECOMPILE)`

```sql
SELECT ...
FROM Orders
WHERE CustomerId = @CustomerId
OPTION (RECOMPILE);
```

SQL Server creates a fresh plan for that execution.

Good when parameter values vary dramatically, but compilation has a cost.

---

### `OPTIMIZE FOR`

You can tell SQL Server to optimize for a particular value or behavior.

---

### Rewrite the query

Sometimes the actual problem is poor query design.

---

### Improve indexes/statistics

Sometimes the execution plan is bad because SQL Server doesn't have good information or indexes.

---

### Important interview point

Don't say:

> "Parameter sniffing is always bad."

It isn't.

Parameter sniffing can actually be **good** because SQL Server can create a plan tailored to the parameter values.

The problem occurs when:

```text
Plan optimized for Customer A
          ↓
Reused for Customer B
          ↓
Performance problem
```

---

# 4. How do we handle Prewarmed Instances?

Now back to Azure.

Suppose:

```text
Running instances:

API1
API2
```

Traffic suddenly increases.

Azure needs another instance:

```text
API3
```

But creating and initializing API3 takes time.

A **prewarmed instance** gives the platform additional prepared capacity so that scaling can happen more quickly.

Conceptually:

```text
Running
+----------------+
| API1 | API2    |
+----------------+

Prewarmed
+----------------+
| API3           |
+----------------+
```

Traffic increases:

```text
API1 API2
   ↓
Traffic spike
   ↓
API3 brought into active service
```

This helps reduce the gap between:

```text
"Azure decided to scale"

and

"new instance is ready to serve traffic."
```

### How do YOU configure it?

If you're using **Azure App Service automatic scaling**, you configure automatic scaling settings in Azure rather than writing something like:

```csharp
EnablePreWarmedInstance();
```

There is no normal C# code you add for this.

You configure it at the **App Service/platform level**.

Azure's automatic scaling feature supports prewarmed instances and minimum instance settings to help handle bursts.

### Developer responsibility

You should make your application:

```text
Fast startup
   +
Stateless
   +
Health-checkable
   +
Externalize state
```

Then Azure can safely add instances.

---

# 5. What is SKU?

This word you'll hear **ALL THE TIME in Azure**.

**SKU = Stock Keeping Unit.**

In Azure, practically think:

> **SKU = the specific service tier/size/capacity option you're choosing.**

For example, an Azure App Service can have different tiers.

Conceptually:

```text
App Service Plan

B1
S1
P1v3
P2v3
...
```

These represent different capabilities/resources/pricing levels.

Think of buying a laptop:

```text
Laptop
 |
 +-- Basic
 |    4 GB RAM
 |
 +-- Pro
 |    16 GB RAM
 |
 +-- Ultra
      32 GB RAM
```

SKU is roughly the Azure equivalent of selecting the **tier/size/configuration**.

---

# SKU and Scale Up

This is where your previous question connects.

Suppose:

```text
Current:

SKU = P1v3
```

and you move to:

```text
SKU = P2v3
```

You're changing the resources/capabilities available to the App Service Plan.

Conceptually:

```text
P1v3
  |
  | SCALE UP
  ↓
P2v3
```

That's **vertical scaling**.

---

# SKU and Scale Out

Scale out is different.

You keep:

```text
SKU = P1v3
```

but increase instances:

```text
1 instance
     ↓
3 instances
```

```text
P1v3
 |
 +---- API1
 +---- API2
 +---- API3
```

That's **horizontal scaling**.

---

# 🔥 Put everything together

Now look at this scenario:

```text
              Traffic
                 |
                 v
           Azure App Service
                 |
        +--------+--------+
        |        |        |
        v        v        v
      API1     API2     API3
```

### Scale Up

```text
P1v3
 ↓
P2v3
```

Make each instance more powerful.

### Scale Out

```text
1 instance
 ↓
3 instances
```

Add more instances.

### Auto Scaling

```text
CPU / Requests / Queue
          ↓
    Autoscale rule
          ↓
1 → 2 → 3 → 4 instances
```

### Prewarmed

```text
Running:
API1 API2

Prepared capacity:
API3

Traffic spike
     ↓
API3 becomes active faster
```

### Stateless

```text
API1 ──┐
API2 ──┼──> Redis
API3 ──┘
```

### Database bottleneck

```text
API1 ──┐
API2 ──┤
API3 ──┤
API4 ──┤
       ↓
    Azure SQL
       🔥
```

And then you investigate:

```text
Application Insights
        ↓
SQL dependency = 3 seconds
        ↓
Find slow SP
        ↓
Execution plan
        ↓
Indexes / query / parameter sniffing
        ↓
Optimize
```

**That's the system-design thinking I want you to develop:** scaling the API isn't the end. You follow the bottleneck through the entire system.

------

Yes bro. These are connected, so let's take them one by one.

---

# 1. User logs in through API1 → next request goes to API3

This is the classic **stateful vs stateless** problem.

Suppose:

```text
Login
  |
  v
API1
  |
  +--> Creates session in API1 memory
       User = Nikhil
```

Next request:

```text
Request
   |
   v
API3
   |
   +--> "Who is Nikhil?" ❌
```

Because API3 has its **own memory**.

```text
API1 RAM              API3 RAM
--------              --------
Nikhil session        Nothing
```

### How do we solve it?

### Option 1 — JWT

For APIs, this is often the preferred approach.

```text
Login
  |
  v
API1
  |
  v
JWT
  |
  v
Angular
```

Angular sends the JWT every time:

```text
Request → API1 → validate JWT
Request → API3 → validate JWT
Request → API2 → validate JWT
```

No server needs to remember the login session.

```text
API1 ─┐
API2 ─┼── Stateless
API3 ─┘
```

### Option 2 — Shared Redis session

If your application genuinely needs server-side session:

```text
API1 ──┐
API2 ──┼──> Redis
API3 ──┘
```

API1 stores:

```text
SessionId = ABC123
User = Nikhil
```

API3 can retrieve the same information.

### Option 3 — Sticky sessions

You can configure the load-balancing layer so that the same user tends to return to the same instance.

```text
Nikhil
  |
  +----> API1
          ↑
          |
       always/tends
```

But this is generally **not the preferred solution for designing a truly horizontally scalable application**, because if API1 dies, the user's local state is still lost and traffic can't freely move between instances.

---

# 2. How do we diagnose Parameter Sniffing?

This is where SQL Server troubleshooting becomes interesting.

Imagine:

```sql
CREATE PROCEDURE GetOrders
    @CustomerId INT
AS
BEGIN
    SELECT *
    FROM Orders
    WHERE CustomerId = @CustomerId;
END
```

Customer 1:

```text
1,000,000 rows
```

Customer 999:

```text
5 rows
```

You notice:

```text
Customer 999 → 5 seconds ❌
Customer 1   → 100 ms
```

You start investigating.

---

## Step 1 — Check whether the query is actually slow

Use:

```sql
SET STATISTICS TIME ON;
SET STATISTICS IO ON;

EXEC GetOrders @CustomerId = 999;
```

Look at:

```text
logical reads
CPU time
elapsed time
```

If one parameter behaves very differently from another, that's a clue.

---

## Step 2 — Compare different parameter values

Run:

```sql
EXEC GetOrders @CustomerId = 1;

EXEC GetOrders @CustomerId = 999;
```

If you see a huge difference, investigate further.

---

## Step 3 — Look at the Actual Execution Plan

In SSMS:

```text
Query
  ↓
Include Actual Execution Plan
  ↓
Execute
```

Shortcut:

```text
Ctrl + M
```

Then execute the query.

Look for things like:

```text
Index Seek
Index Scan
Table Scan
Estimated Rows
Actual Rows
```

### Very important clue

Suppose SQL Server estimated:

```text
Estimated rows = 5
Actual rows = 1,000,000
```

That's a huge mismatch.

Or:

```text
Estimated rows = 1,000,000
Actual rows = 5
```

That can lead to a poor plan.

---

# 3. How do you know it's specifically Parameter Sniffing?

You don't simply see:

> "Query is slow → parameter sniffing."

You investigate.

A common pattern is:

```text
Same stored procedure
       |
       +---- Parameter A → Fast
       |
       +---- Parameter B → Slow
```

Then:

```text
Execution plan
      ↓
Plan is good for A
      ↓
Same cached plan reused for B
      ↓
B performs badly
```

You can inspect cached plans and Query Store as well.

### Query Store is especially useful

For production systems, **Query Store** helps you compare query performance and execution plans over time.

You might discover:

```text
Query
 ↓
Plan 1 → 100 ms
Plan 2 → 8 seconds
```

That tells you the query's performance changed with the plan.

---

# 4. What are `OPTION (RECOMPILE)` and `OPTIMIZE FOR`?

Don't worry bro — **you don't manually type these every time you execute the stored procedure.**

They're **query hints that you put into the SQL code when you decide that a particular query needs them.**

---

## `OPTION (RECOMPILE)`

Normally:

```sql
SELECT *
FROM Orders
WHERE CustomerId = @CustomerId;
```

You can say:

```sql
SELECT *
FROM Orders
WHERE CustomerId = @CustomerId
OPTION (RECOMPILE);
```

You're basically telling SQL Server:

> **"For this execution, create a fresh execution plan based on the current parameter value."**

So:

```text
Customer 1
    ↓
Compile specifically for Customer 1
    ↓
Execute


Customer 999
    ↓
Compile specifically for Customer 999
    ↓
Execute
```

This can solve parameter-sniffing problems where different parameter values need very different plans.

### But what's the downside?

Compilation itself costs CPU/time.

If this runs:

```text
5 times/day
```

probably not a big deal.

If this runs:

```text
50,000 times/second
```

constantly recompiling could be expensive.

So don't blindly add `RECOMPILE`.

---

# 5. What is `OPTIMIZE FOR`?

Another option is telling SQL Server:

> "Optimize this query assuming a particular parameter value."

Example:

```sql
SELECT *
FROM Orders
WHERE CustomerId = @CustomerId
OPTION (OPTIMIZE FOR (@CustomerId = 999));
```

Now SQL Server creates a plan optimized around that value.

Conceptually:

```text
Many parameter values
       ↓
Choose representative value
       ↓
Create plan
       ↓
Reuse plan
```

There are also other approaches, including `OPTIMIZE FOR UNKNOWN`, query/index changes, updated statistics, or rewriting the query.

The **correct solution depends on why the plan is bad**.

---

# 6. Why is Parameter Sniffing sometimes GOOD?

This is the most important part.

Imagine:

```text
Customer A → 1,000,000 records
Customer B → 5 records
```

SQL Server has two possible strategies.

### Strategy A — Index Seek

Excellent for:

```text
5 records
```

### Strategy B — Scan

Potentially better for:

```text
1,000,000 records
```

Now suppose SQL Server sees:

```text
@CustomerId = B
```

during compilation.

It can say:

> "Only 5 rows. I'll use an index seek."

```text
Customer B
    ↓
5 rows
    ↓
Index Seek
    ↓
FAST ⚡
```

That's parameter sniffing working **in your favor**.

Without using the parameter information intelligently, SQL Server might have to use a more generic plan that isn't ideal for that particular value.

---

# 7. Then where does the problem happen?

The problem is **data distribution**.

Imagine:

```text
First execution:

Customer B
5 rows
   ↓
SQL creates Index Seek plan
```

Then:

```text
Next execution:

Customer A
1,000,000 rows
   ↓
SQL reuses Index Seek plan
   ↓
Potentially terrible performance ❌
```

So:

> **Parameter sniffing itself isn't the enemy. The problem is when a cached execution plan optimized for one parameter value performs poorly for other parameter values.**

That's the interview-quality answer.

---

# 🔥 Think of it like this

Imagine you're a delivery driver.

You get:

```text
Customer A
1,000,000 packages
```

You choose:

```text
Truck 🚚
```

Then someone says:

```text
Customer B
5 packages
```

You could use:

```text
Bike 🚲
```

But if you blindly reuse the truck strategy for every customer, it may be inefficient.

That's essentially the problem.

---

# 8. What should YOU say in an interview?

If they ask:

### "What is parameter sniffing?"

Say:

> **"Parameter sniffing is a SQL Server optimization behavior where the optimizer uses the parameter values from compilation to generate an execution plan, which may then be reused for later executions. It's beneficial when that plan works well for different parameter values, but can cause performance issues when data distributions vary significantly."**

If they ask:

### "How would you diagnose it?"

Say:

> **"I would compare performance for different parameter values, inspect the actual execution plan and estimated-versus-actual rows, check Query Store for plan changes and regressions, and determine whether a cached plan is inappropriate for certain parameter values."**

If they ask:

### "How would you fix it?"

Say:

> **"Depending on the scenario, I might use RECOMPILE, OPTIMIZE FOR, improve indexes/statistics, or rewrite the query. I wouldn't blindly use RECOMPILE because recompilation has its own CPU cost."**

That's a **very solid 4-year .NET developer answer**.

---

## One more thing to connect to your System Design learning

Notice what just happened:

```text
API Scaling
     ↓
More API instances
     ↓
More requests to SQL
     ↓
SQL becomes bottleneck
     ↓
Slow Stored Procedure
     ↓
Execution Plan
     ↓
Parameter Sniffing
     ↓
SQL optimization
```

This is exactly why I don't want you learning System Design as isolated definitions.

**One architecture decision can expose a completely different bottleneck downstream.**

------

Yes bro. Let's **forget the complicated terminology for a minute**. The confusion is mainly because `RECOMPILE`, `OPTIMIZE FOR`, and parameter sniffing are all related.

I'll explain them with **one simple example**.

---

# First: What should we do instead of blindly using `RECOMPILE`?

When a stored procedure is slow, **don't immediately assume parameter sniffing**.

Follow this process:

```text
Stored Procedure is slow
        ↓
Check execution time
        ↓
Check Actual Execution Plan
        ↓
Check Estimated vs Actual rows
        ↓
Check indexes / statistics
        ↓
Check Query Store
        ↓
Is parameter sniffing actually the problem?
        ↓
YES
        ↓
Choose appropriate solution
```

Possible solutions:

```text
             Parameter Sniffing
                    |
       +------------+-------------+
       |            |             |
       v            v             v
  RECOMPILE    OPTIMIZE FOR    Rewrite query
       |
       |
   Sometimes
   appropriate
```

You choose based on the situation.

---

# Now let's REALLY understand 4, 5 and 6

We'll use this example throughout.

Suppose we have:

```sql
CREATE PROCEDURE GetOrders
    @CustomerId INT
AS
BEGIN

    SELECT *
    FROM Orders
    WHERE CustomerId = @CustomerId;

END
```

And our database contains:

```text
Customer 1
---------
1,000,000 orders


Customer 999
------------
5 orders
```

This difference is important.

---

# 4. RECOMPILE

Normally SQL Server does something like:

```text
First execution
      ↓
Look at parameter
      ↓
Create execution plan
      ↓
Save/cache plan
      ↓
Reuse it later
```

Suppose the first request is:

```sql
EXEC GetOrders @CustomerId = 999;
```

SQL Server sees:

```text
Customer 999
     ↓
Only 5 rows
     ↓
"Index Seek looks good"
     ↓
Create Plan A
```

Then later:

```sql
EXEC GetOrders @CustomerId = 1;
```

There are:

```text
1,000,000 rows
```

But SQL Server may reuse the existing plan.

That's where we can get a problem.

---

## RECOMPILE says:

> **"Don't reuse the old plan. Make a new plan for this execution."**

```sql
SELECT *
FROM Orders
WHERE CustomerId = @CustomerId
OPTION (RECOMPILE);
```

Now:

```text
Customer 999
     ↓
Create plan specifically for 999
     ↓
Execute


Customer 1
     ↓
Create plan specifically for 1
     ↓
Execute
```

So every execution gets a chance to choose an appropriate plan.

---

## Why don't we ALWAYS use RECOMPILE?

Because creating a plan costs CPU.

Imagine this runs:

```text
5 times/day
```

No big deal.

But imagine:

```text
100,000 times/second
```

Then you're saying:

```text
100,000 requests
      ↓
100,000 plan compilations 😵
```

That's wasteful.

So:

> **RECOMPILE is useful when parameter values produce very different optimal plans, but we don't use it blindly because recompilation itself has a cost.**

---

# 5. OPTIMIZE FOR

This one is easier if you think of it as:

> **"SQL Server, create the plan assuming this type of parameter value."**

Suppose most of your customers have around:

```text
100 orders
```

but occasionally one customer has:

```text
1,000,000 orders
```

You might tell SQL Server:

```sql
OPTION (OPTIMIZE FOR (@CustomerId = 999))
```

You're basically saying:

> "When you create the plan, use Customer 999 as your example."

Conceptually:

```text
                    Query
                      |
                      v
              OPTIMIZE FOR 999
                      |
                      v
              Create execution plan
                      |
                      v
                Reuse the plan
```

Unlike `RECOMPILE`:

```text
RECOMPILE

Request 1 → New plan
Request 2 → New plan
Request 3 → New plan
```

`OPTIMIZE FOR`:

```text
Request 1 ─┐
Request 2 ─┤
Request 3 ─┼──> Same cached plan
Request 4 ─┘
```

So:

### RECOMPILE

> "Create a new plan for each execution."

### OPTIMIZE FOR

> "Create a plan based on this chosen parameter value and reuse it."

---

# 6. Why can Parameter Sniffing actually be GOOD?

This is where I think you're getting stuck.

Forget the word **sniffing**.

Think:

> **SQL Server looks at the actual parameter and uses that information to make a better plan.**

That's useful!

---

## Example

Suppose:

```text
Customer 999
    ↓
5 orders
```

SQL Server sees:

```text
@CustomerId = 999
```

It realizes:

> "Only 5 rows. I don't need to scan the entire table."

So it might choose:

```text
Index Seek
```

That's good.

```text
5 rows
  ↓
Index Seek
  ↓
FAST ⚡
```

That's parameter sniffing helping us.

---

# Where does it become BAD?

Now suppose:

```text
Customer 1
    ↓
1,000,000 orders
```

But the cached plan was created when SQL Server saw:

```text
Customer 999
    ↓
5 rows
    ↓
Index Seek
```

Then:

```text
Customer 1
    ↓
1,000,000 rows
    ↓
Reuse Index Seek plan
    ↓
Could be inefficient ❌
```

The problem is:

```text
Plan was created for A
        ↓
Plan reused for B
        ↓
B needs a different strategy
```

---

# 🚨 The easiest way to remember this

Imagine you have two roads.

```text
Road A = small road
Road B = highway
```

For a small amount of traffic:

```text
5 cars
 ↓
Small road 🚗
```

Perfect.

For huge traffic:

```text
1,000,000 cars
 ↓
Highway 🚗🚗🚗🚗🚗
```

Better.

Now imagine the system chooses the small road because the **first traffic it saw was only 5 cars**.

Later:

```text
1,000,000 cars
       ↓
Small road
       ↓
TRAFFIC JAM 🚨
```

That's the basic parameter-sniffing problem.

---

# So what should we actually do?

Let's say production reports:

> "This stored procedure is sometimes fast and sometimes extremely slow."

You don't immediately write:

```sql
OPTION (RECOMPILE)
```

Instead:

### Step 1

Test different parameter values.

```sql
EXEC GetOrders 999;

EXEC GetOrders 1;
```

### Step 2

Look at the **Actual Execution Plan**.

Check:

```text
Estimated Rows
Actual Rows
Index Seek
Index Scan
Table Scan
```

### Step 3

Check Query Store.

You might discover:

```text
Same query
   |
   +--> Plan A → 100 ms
   |
   +--> Plan B → 8 seconds
```

### Step 4

Then decide.

Maybe the problem is:

```text
Missing index
```

Then add/fix the index.

Maybe:

```text
Outdated statistics
```

Then address statistics.

Maybe:

```text
Parameter sniffing
```

Then consider:

```text
RECOMPILE
OPTIMIZE FOR
query rewrite
other plan-management approaches
```

---

# One important thing: You don't normally add these from .NET

You asked earlier:

> "Will I be giving the syntax every time?"

**No.**

If you're using a stored procedure:

```text
.NET
 |
 | EXEC GetOrders
 v
SQL Server
 |
 v
Stored Procedure
```

The DBA/developer changes the SQL code **inside the stored procedure** if that's the chosen solution.

For example:

```sql
CREATE PROCEDURE GetOrders
    @CustomerId INT
AS
BEGIN

    SELECT *
    FROM Orders
    WHERE CustomerId = @CustomerId
    OPTION (RECOMPILE);

END
```

Then your C# code remains:

```csharp
await connection.QueryAsync<Order>(
    "GetOrders",
    new { CustomerId = customerId },
    commandType: CommandType.StoredProcedure);
```

You don't change your C# code for every execution.

---

# 🧠 Final cheat sheet

| Concept                | Easy meaning                                                     |
| ---------------------- | ---------------------------------------------------------------- |
| **Parameter sniffing** | SQL Server uses parameter values when creating an execution plan |
| **Why good?**          | It can create a plan suited to the actual data                   |
| **Why bad?**           | A plan good for one parameter may be bad for another             |
| **RECOMPILE**          | Create a fresh plan for this execution                           |
| **OPTIMIZE FOR**       | Create the plan assuming a particular parameter/value            |
| **Index/statistics**   | Often should be checked before using hints                       |
| **Query Store**        | Helps identify plan/performance problems                         |

### The most important distinction:

```text
RECOMPILE
"Forget the old plan.
Create a new plan NOW."
```

vs.

```text
OPTIMIZE FOR
"Create the plan assuming THIS kind of value."
```

vs.

```text
Parameter Sniffing
"SQL Server looked at the parameter
when creating the plan."
```

And bro, **parameter sniffing isn't a feature you turn on/off**. It's a SQL Server optimization behavior. The question is whether the resulting cached plan is appropriate for your workload.


Answer this in your own words. Don't worry if it's imperfect — **I'll correct it like an interviewer.**
