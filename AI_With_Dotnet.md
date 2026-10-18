# Agentic AI Roadmap Using .NET and C#

If you want to learn Agentic AI using .NET and C#, you can follow the same AI engineering principles while building everything in the Microsoft ecosystem. You do not need to switch to Python to become an Agentic AI developer.

My recommendation is to learn C# → LLM APIs → tool calling → RAG → AI agents → multi-agent workflows → production deployment with ASP.NET Core.

This roadmap is especially suitable if you already work with .NET or want to build your career as a .NET AI Engineer.

​微软 AI Agent三剑客：AutoGen、Semantic Kernel与MEAI的协同演进 - 「圣杰」 - 博客园

## 1. Your .NET Agentic AI technology stack

Grow Programming Proficiency: C# | Go1

C# and .NET

Your core language, async programming, dependency injection, LINQ, and configuration.

Semantic Kernel AI - Develop AI agents in your code

Semantic Kernel

An SDK for connecting AI models with C# functions, plugins, and orchestration.

Microsoft Agent Framework: Building the Next Generation of AI-Powered Agents - Nanddeep Nachan Blogs

Microsoft Agent Framework

A framework to investigate for building agents, workflows, and multi-agent applications in .NET.

ASP.NET Core logo by columan | Redbubble

ASP.NET Core

Build Web APIs and expose your agent to web applications and other services.

Azure AI Foundry - Création d’applications d’IA générative

LLM provider and deployment

Use Azure OpenAI, compatible model APIs, or other providers. Add Azure services when your project needs them.

Official documentation to bookmark:

- [Microsoft Agent Framework](<https://learn.microsoft.com/en-us/agent-framework/overview/?utm_source=chatgpt.com>)
- [Semantic Kernel for .NET](<https://learn.microsoft.com/en-us/semantic-kernel/overview/?utm_source=chatgpt.com>)
- [Microsoft.Extensions.AI](<https://learn.microsoft.com/en-us/dotnet/ai/microsoft-extensions-ai?utm_source=chatgpt.com>)
- [ASP.NET Core documentation](<https://learn.microsoft.com/en-us/aspnet/core/?utm_source=chatgpt.com>)
- [Azure AI Foundry](<https://learn.microsoft.com/en-us/azure/ai-foundry/?utm_source=chatgpt.com>)

The Microsoft AI ecosystem is evolving, so learn the underlying concepts alongside the SDKs. Semantic Kernel and Microsoft Agent Framework are related but distinct; check their current documentation before choosing a framework for a new project.

## 2. Complete 16-week roadmap for Agentic AI in .NET

Assumption: you know basic programming concepts. If you are new to C#, spend an extra 2–4 weeks on the fundamentals.

Recommended pace: 1–2 hours daily, with a working project at the end of each phase.

Weeks 1–2: C# and .NET fundamentals

Learn:

- Classes, interfaces, records, and generics.
- LINQ, collections, and exception handling.
- `async`/`await`, `Task`, and `CancellationToken`.
- Dependency injection and configuration.
- HTTP clients, JSON serialization, and NuGet.

Project: Build a C# console application that calls a public API, processes JSON, and produces a summary.

Weeks 3–4: LLM integration

Learn:

- LLM fundamentals, prompts, and context windows.
- Model API authentication and configuration.
- Chat messages, conversation history, and streaming.
- Structured output and JSON validation.
- `Microsoft.Extensions.AI` and `IChatClient`.

Project: Build a C# console chatbot that summarizes documents and returns structured JSON.

Resource: [Build AI apps with .NET](<https://learn.microsoft.com/en-us/dotnet/ai/?utm_source=chatgpt.com>).

Weeks 5–6: Function calling and tools

Learn:

- Define C# methods as AI-callable functions.
- `AIFunctionFactory` and function invocation.
- Connect APIs, business logic, and databases.
- Validate arguments and handle failures.
- Limit tool permissions and require approval for sensitive actions.

Project: Build a customer-support assistant that looks up orders and checks delivery status.

Resource: [AI tool calling in .NET](<https://learn.microsoft.com/en-us/dotnet/ai/conceptual/calling-tools?utm_source=chatgpt.com>).

Microsoft Learn

Weeks 7–8: RAG and knowledge retrieval

Learn:

- PDF and document processing.
- Chunking, embeddings, and vector search.
- Retrieval-Augmented Generation.
- Metadata filtering and source citations.
- Connecting your own SQL or document data.
- Evaluating retrieval relevance.

Project: Build an internal company-document assistant that answers questions using relevant documents.

Resource: [Microsoft .NET AI documentation](<https://learn.microsoft.com/en-us/dotnet/ai/?utm_source=chatgpt.com>).

Weeks 9–10: Agent development

Learn:

- Agent instructions and tool selection.
- Observe–decide–act loops.
- Planning and task decomposition.
- Memory, conversation state, and stopping rules.
- Microsoft Agent Framework fundamentals.
- Retries, timeouts, and error recovery.

Project: Build a research agent that searches approved sources, gathers evidence, and generates a report.

Resource: [Microsoft Agent Framework documentation](<https://learn.microsoft.com/en-us/agent-framework/?utm_source=chatgpt.com>).

Microsoft Learn

Weeks 11–12: Workflows and multi-agent systems

Learn:

- Workflow graphs and conditional routing.
- Supervisor and specialist agents.
- Delegation, handoffs, and shared state.
- Human-in-the-loop workflows.
- MCP for connecting external tools and context.
- Checkpoints and resumable execution.

Project: Build a research workflow with researcher, analyst, and reviewer agents.

Weeks 13–14: Production engineering

Learn:

- ASP.NET Core Web APIs.
- Dependency injection and configuration.
- Logging, tracing, and evaluation.
- Prompt injection and tool security.
- Authentication, authorization, and secret management.
- Unit tests, integration tests, and failure handling.

Project: Expose your agent through a secured ASP.NET Core API and add automated tests.

Weeks 15–16: Deployment and portfolio

Learn:

- Docker fundamentals.
- Cloud deployment, such as Azure App Service or Container Apps.
- Persistent storage and background jobs.
- Cost tracking and performance monitoring.
- README files, architecture diagrams, and demonstrations.

Project: Deploy an end-to-end Agentic AI application with a web API, tools, retrieval, and evaluation.

## 3. Start coding: your first .NET AI application

Before learning an agent framework, understand how to connect a C# application to an LLM.

A useful starting point is `Microsoft.Extensions.AI`, which provides common abstractions for chat and tool calling across supported model providers.

Microsoft Learn

+1

Create a console project:

bash
```
dotnet new console -n AgenticAIStarter
cd AgenticAIStarter
dotnet add package Microsoft.Extensions.AI
```

You will also need the integration package for your chosen model provider. For example, if you use the OpenAI .NET SDK, add its `Microsoft.Extensions.AI` integration package and configure your API key securely.

Your first milestone is simple:

1. Send a prompt to an LLM.
2. Receive a response.
3. Display the result in the console.
4. Add conversation history.
5. Add one C# function the model can call.
6. Turn the console app into an ASP.NET Core API.

Don't worry about autonomous planning or multi-agent orchestration yet. Get the basic model integration working first.

## 4. Which .NET AI framework should you choose?

This is an important decision because the Microsoft ecosystem has been changing.

| Technology | When to use it |
| --- | --- |
| `Microsoft.Extensions.AI` | Start with model-provider abstractions, chat, and tool calling. |
| Microsoft Agent Framework | Recommended starting point for new Microsoft-stack agent and workflow projects. |
| Semantic Kernel | Useful for understanding existing applications and the Microsoft AI ecosystem; consider it when maintaining existing systems. |
| ASP.NET Core | Build and host your application's APIs. |
| Entity Framework Core | Access relational business data when needed. |

Microsoft Agent Framework reached version 1.0 in April 2026 and is the successor to Semantic Kernel and AutoGen. For a new project, I'd start with Agent Framework after learning basic model calls and tools.

Microsoft Agent Framework

+1

Official starting point: [Microsoft Agent Framework — C# documentation](<https://learn.microsoft.com/en-us/agent-framework/?utm_source=chatgpt.com>).

## 5. Your portfolio project: an enterprise AI support agent

Once you finish the fundamentals, build one project that demonstrates the entire stack.

Solvi: Help Desk Ticketing System Asp.Net Core Mvc C# with OpenAI API

## AI Customer Support Agent

Example request: "Check order 1052, explain the return policy, and draft a response to the customer."

Suggested architecture

ASP.NET Core Web API

Request validation and authentication

AI agent

Interprets request and selects tools

Order lookup

SQL / business APIs

Policy search

RAG / documents

Validated response

Draft answer, citations, and approval when required

What this project demonstrates

- C# and .NET API development.
- LLM integration and tool calling.
- RAG and database integration.
- Agent orchestration and state.
- Security, testing, and deployment.

Keep order data read-only initially. Require explicit authorization and human confirmation before any real refund, cancellation, or other consequential action.

## 6. Your first week

Here is a concrete plan you can begin today.

- Day 1: Review C# classes, interfaces, and dependency injection.
- Day 2: Practice `async`/`await`, `HttpClient`, and JSON serialization.
- Day 3: Create a console application that calls an LLM.
- Day 4: Experiment with system prompts and structured output.
- Day 5: Add conversation history and error handling.
- Day 6: Create a C# method that retrieves sample business data.
- Day 7: Connect the method as an AI tool and test whether the model uses it appropriately.

By the end of the week, your goal is a small working AI application—not a complicated autonomous agent.

One question so I can adjust the roadmap properly: How much .NET experience do you already have?

Your current .NET experience

Beginner — learning C# now

intermediate Intermediate — C#, ASP.NET Core, APIs, SQL

Advanced — experienced .NET developer

What would you like to build first?

agent-framework AI agents using Microsoft Agent Framework

RAG chatbot over PDFs and company documents

Enterprise AI agents with ASP.NET Core and SQL

Job-ready Agentic AI developer portfolio

 Build my .NET learning plan

[cnblogs.com](<https://www.cnblogs.com/sheng-jie/p/18924852?utm_source=chatgpt.com>)

[auratheme.gumroad.com](<https://auratheme.gumroad.com/l/solvi-ticket-helpdesk-asp-net-mvc?utm_source=chatgpt.com>)
