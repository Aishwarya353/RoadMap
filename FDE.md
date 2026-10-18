# Roadmap: .NET + Angular Full-Stack Developer → Forward Deployed Engineer (FDE)

With 7 years of tech experience, your strategy should be different from that of a beginner learning AI. You already understand software engineering, application architecture, APIs, databases, debugging, and delivering features. Your goal is to combine those skills with AI engineering, customer-facing problem solving, and production deployment.

You do not need to spend months learning Python from scratch, mastering every ML algorithm, or training an LLM from the ground up before you can build useful AI systems.

You need to become the engineer who can walk into a customer's environment, understand their business problem, build an AI-powered solution, integrate it into their existing systems, and make it reliable enough for production.

## 1. What a Forward Deployed Engineer actually does

What Is a Forward Deployed Engineer? Complete 2026 Guide - Aced (formerly Exponent)

A Forward Deployed Engineer combines several roles:

- Software engineer: builds applications, integrations, APIs and production systems.
- AI engineer: implements LLMs, RAG, agents, evaluation and model integrations.
- Solutions engineer: translates customer requirements into technical designs.
- Product-minded engineer: discovers the actual business problem and ships the right solution.
- Production engineer: handles reliability, security, latency, monitoring and cost.

For your background, the biggest shift is from building predefined application features to solving ambiguous, real-world customer problems using software and AI.

### The skill transformation

Your existing strengths

.NET, C#, Angular, REST APIs, enterprise architecture, SQL, authentication, debugging, testing, delivery and integration.

Leverage immediately

Your highest-priority gaps

LLM fundamentals, Python for AI, RAG, tool calling, agent workflows, MCP, evaluation, guardrails and production AI observability.

Learn deeply

Your FDE differentiators

Customer discovery, workflow mapping, rapid prototyping, system integration, technical communication and measurable business outcomes.

Practice continuously

## 2. Priority framework: what to learn first

Don't treat every AI topic as equally important. For an FDE transition, I recommend this order.

### P0 — Must master

Core employability and first production projects

- LLM fundamentals, prompting and structured outputs
- Python essentials and LLM APIs
- RAG, embeddings, vector search and reranking
- Tool calling and deterministic agent workflows
- Evaluation, security and production deployment
- Customer discovery and end-to-end delivery

### P1 — Strong differentiators

Skills that make you effective on complex customer deployments

- Agent frameworks and graph-based orchestration
- MCP clients, servers, tools and security
- Multi-agent systems
- Advanced RAG, GraphRAG, MAG and CAG patterns
- Fine-tuning, LoRA and model selection
- LLMOps, tracing, cost and latency optimization

### P2 — Specialize after the foundations

Needed for certain FDE roles, not every role

- Training Transformers from scratch
- Distributed training and GPU kernel optimization
- Deep reinforcement learning research
- Advanced diffusion model training
- Novel model architecture research

Recommended allocation of study time: roughly 60% building projects, 25% learning concepts and 15% interview preparation and customer-facing practice. Your experience means practical execution should be the center of the transition.

## 3. Your complete 24-week FDE transition roadmap

Assuming you can dedicate around 12–15 hours per week alongside your job, use the following sequence. If you have more time, increase project depth rather than adding more frameworks.

Priority key: P0 = essential; P1 = important differentiator; P2 = specialization.

## Month 1 — AI foundations and LLM application engineering

### Week 1 — Python for an experienced software engineer

P0- Python syntax, collections, functions and type hints
- Classes, dataclasses, exceptions and modules
- Virtual environments, package management and configuration
- Async/await, HTTP clients, streaming and concurrency
- Pydantic, FastAPI, pytest and logging
- NumPy and Pandas essentials
- Python dependency management and project structure
  Deliverable: a tested FastAPI service that calls an LLM API and streams the response.

### Week 2 — LLM internals

P0- Tokens, tokenizers and context windows
- Embeddings and vector similarity
- Transformers, attention, positional encoding
- Next-token prediction and pretraining
- Instruction tuning and post-training
- Temperature, top-p and sampling
- Context management, hallucinations and model limitations
  Deliverable: compare three models on a fixed set of tasks for quality, latency and cost.

### Week 3 — Prompting and structured outputs

P0- System instructions and message hierarchy
- Zero-shot and few-shot prompting
- Prompt templates and context construction
- JSON Schema and structured responses
- Pydantic validation and retry strategies
- Tool/function calling fundamentals
- Prompt injection basics
  Deliverable: a business-document extraction API with schema validation and automated tests.

### Week 4 — Embeddings and retrieval foundations

P0- Embedding models and similarity metrics
- Document parsing and text chunking
- Dense vs. sparse retrieval
- BM25 and vector search
- Metadata filtering
- Introduction to FAISS or PostgreSQL with pgvector
- Build a retrieval evaluation dataset
  Deliverable: a searchable document index with measurable retrieval quality.

## Month 2 — Production-quality RAG

### Week 5 — Basic and advanced RAG

P0- Basic RAG architecture
- Ingestion, chunking, embedding and indexing
- Retrieval, context assembly and generation
- Query rewriting and multi-query retrieval
- Hybrid search and reciprocal rank fusion
- Reranking and top-k optimization
- Citation generation and evidence grounding
- Handling insufficient or conflicting evidence

### Week 6 — RAG evaluation and optimization

P0- Retrieval precision, recall, MRR and NDCG
- Answer relevance and faithfulness
- Context precision and context recall
- Golden datasets and synthetic test cases
- LLM-as-a-judge and human evaluation
- Chunking and embedding ablation tests
- Latency, token and cost measurements
- Regression tests for retrieval changes

Deliverable: a benchmark report comparing at least three retrieval configurations.

### Week 7 — Advanced RAG architectures

P1- Corrective RAG and self-reflective RAG
- Adaptive and agentic RAG
- Hierarchical and parent-child retrieval
- Query decomposition and multi-hop retrieval
- Knowledge graphs and GraphRAG
- Table-aware and multimodal RAG
- Temporal retrieval and metadata-aware search
- Access-controlled and multi-tenant RAG

### Week 8 — Enterprise RAG integration

P0- Integrate SQL databases and business APIs
- Handle document updates and deletions
- Enforce tenant and document-level permissions
- Use incremental ingestion and re-indexing
- Add caching, retries and observability
- Implement authentication and authorization
- Containerize and deploy the application
- Test failure cases and operational recovery

Deliverable: a deployed enterprise knowledge assistant with citations, access controls and an evaluation suite.

## Month 3 — Agents, Agentic AI and MCP

### Week 9 — Agent fundamentals

P0- What an agent is and when to use one
- LLM calls vs. tools vs. agent loops
- State, goals, actions and observations
- Function calling and tool schemas
- Tool argument validation
- Deterministic workflows vs. autonomous loops
- Planning, execution, stopping conditions
- Retry limits and failure recovery

### Week 10 — Agent orchestration

P0- LangGraph or an equivalent stateful orchestration framework
- Nodes, edges and conditional transitions
- State persistence and checkpointing
- Human-in-the-loop approvals
- Durable workflows and resumability
- Short-term and long-term memory
- ReAct and plan-execute patterns
- Timeouts, cancellation and idempotency

### Week 11 — MCP in depth

P0- MCP architecture and protocol concepts
- Hosts, clients and servers
- Tools, resources and prompts
- Tool discovery and invocation
- Local and remote transports
- Authentication and authorization
- Server lifecycle and capability negotiation
- Error handling and protocol validation
- Tool descriptions and schemas
- Untrusted tool outputs and prompt injection
- MCP security, permissions and audit logging
- Build an MCP server for an existing .NET API
- Connect an AI client to that server

Deliverable: expose selected business operations from a .NET backend through an MCP server and consume them from an AI application.

### Week 12 — Multi-agent systems

P1- Single-agent vs. multi-agent design
- Supervisor and worker patterns
- Planner, researcher and executor roles
- Handoffs and shared state
- Agent-to-agent communication
- Parallel execution and task delegation
- Coordination and conflict resolution
- Multi-agent memory and context isolation
- Budget, iteration and tool-use limits
- Tracing and end-to-end agent evaluation

Deliverable: a controlled multi-agent research or support workflow with a measurable success rate.

## Month 4 — Advanced context architectures, fine-tuning and multimodal AI

### Week 13 — RAG variants: GraphRAG, CAG, MAG and beyond

P1- GraphRAG and knowledge graph retrieval
- CAG (Cache-Augmented Generation)
- Memory-Augmented Generation
- MAG (an overloaded acronym; identify the specific architecture)
- Long-context generation and context selection
- Hybrid retrieval and generation pipelines
- Cache invalidation and freshness
- Retrieval vs. cache vs. model memory
- Architecture selection based on data and workload

### Week 14 — Fine-tuning and open-weight models

P1- Base vs. instruction-tuned models
- Supervised fine-tuning
- Dataset preparation and quality
- LoRA and QLoRA
- PEFT and adapter management
- Preference optimization: DPO and related methods
- Quantization and inference trade-offs
- Distillation and model selection
- When fine-tuning is better than prompting or RAG

### Week 15 — Multimodal AI

P1- Vision-language models
- Image understanding and OCR
- Document layout and table extraction
- Image generation and diffusion fundamentals
- Speech-to-text and text-to-speech
- Audio understanding and streaming
- Video summarization and retrieval
- Multimodal embeddings
- Multimodal RAG and tool use

### Week 16 — AI security and responsible deployment

P0- Direct and indirect prompt injection
- Data leakage and PII protection
- Model and tool authorization
- Least-privilege access
- Sandboxed code execution
- Human approvals for high-impact actions
- Output validation and content safety
- Tenant isolation and audit logs
- Threat modeling for agents and MCP
- Adversarial testing and incident response

## Month 5 — Production FDE engineering

### Week 17 — LLMOps and observability

P0- Trace complete LLM and agent workflows
- Record model, retrieval and tool spans
- Measure latency and token consumption
- Track model and prompt versions
- Monitor errors and quality regressions
- Build evaluation datasets from approved feedback
- Create dashboards and operational alerts
- Integrate evaluations into CI/CD

Production evaluation and tracing are core capabilities in modern AI platforms, including Microsoft Foundry.

Microsoft Learn

+2

### Week 18 — Scaling and optimization

P1- Async concurrency and batching
- Rate limits and backpressure
- Caching and deduplication
- Context and token-budget optimization
- Model routing and fallback
- Quantized and self-hosted inference
- GPU serving fundamentals
- Load testing and resilience
- Cost per successful task
- Latency-quality-cost trade-offs

### Week 19 — Cloud and enterprise deployment

P0- Docker and container registries
- Azure identity and managed identities
- Azure OpenAI / Microsoft Foundry concepts
- Key Vault and secret management
- Azure App Service or Container Apps
- Azure networking and private endpoints
- SQL, storage and enterprise data integration
- CI/CD, environment configuration and rollback
- Authentication, authorization and audit trails
- Production support and incident management

### Week 20 — Production readiness

P0- SLOs and SLIs
- Availability and degradation strategies
- Retry policies, circuit breakers and timeouts
- Failure isolation
- Backups and recovery
- Security reviews
- Evaluation acceptance thresholds
- Regression testing
- Release gates and rollback
- Operational documentation and runbooks

## Month 6 — FDE practice, capstone and interviews

### Week 21 — Customer discovery

P0- Stakeholder interviews
- Identify the actual business bottleneck
- Map current workflows and systems
- Define measurable business outcomes
- Discover data, security and integration constraints
- Separate requirements from proposed solutions
- Assess feasibility and failure costs
- Define a minimum viable deployment

### Week 22 — Solution design and rapid prototyping

P0- Architecture diagrams and design documents
- Build-vs-buy decisions
- Model and framework selection
- Data flow and permission design
- Proof of concept in a constrained environment
- Baseline and acceptance criteria
- Demo and stakeholder feedback
- Translate prototype learnings into production requirements

### Week 23 — Capstone production deployment

P0- Integrate with a realistic enterprise workflow
- Implement RAG and approved tool use
- Add authentication and authorization
- Create evaluation and regression suites
- Deploy the backend and user interface
- Add monitoring and cost tracking
- Run security and failure tests
- Write deployment and incident documentation

### Week 24 — Interview and portfolio readiness

P0- AI and LLM fundamentals
- RAG and retrieval debugging
- Agent and MCP architecture
- System design and trade-offs
- Coding and debugging exercises
- Customer scenario role-play
- Architecture presentation
- Demonstrate measurable project outcomes
- Prepare behavioral stories from your seven years of experience

## 4. The complete AI/GenAI topic map: what you must know beyond the 24 weeks

The 24-week plan is your execution schedule. This topic map is the broader reference syllabus for filling in gaps over time.

### A. LLM fundamentals and model internals

Priority: P0 fundamentals; P2 research-level implementation

- Model architecture: encoder-only, decoder-only, encoder-decoder, dense models, MoE.
- Tokenization: BPE, WordPiece, SentencePiece, special tokens, vocabulary design.
- Embeddings: word, sentence, document, multimodal, sparse and dense representations.
- Attention: self-attention, cross-attention, causal masks, GQA, MQA, RoPE, FlashAttention.
- Training: pretraining, supervised fine-tuning, preference optimization, RLHF, DPO, GRPO.
- Inference: prefill, decoding, KV cache, continuous batching, speculative decoding.
- Sampling: greedy decoding, temperature, top-k, top-p, repetition penalties.
- Model optimization: LoRA, QLoRA, quantization, distillation, pruning.
- Advanced topics: scaling laws, test-time compute, reasoning models, distributed training.

You need strong conceptual understanding and practical inference skills. Training foundation models at scale is not a prerequisite for most FDE roles.

### B. RAG, MAG, CAG and context engineering

Priority: P0 for RAG; P1 for specialized retrieval and context architectures

First, distinguish the terms carefully. RAG and CAG have recognizable meanings, but MAG is used for different concepts across papers and implementations. Confirm what a particular employer or framework means by MAG rather than assuming a universal definition.

| Architecture | Core idea | Learn when |
| --- | --- | --- |
| Basic RAG | Retrieve relevant documents for each query | P0 |
| Hybrid RAG | Combine keyword and vector retrieval | P0 |
| Advanced RAG | Query rewriting, reranking and retrieval optimization | P1 |
| GraphRAG | Use knowledge graphs and graph-based retrieval | P1 |
| Agentic RAG | An agent decides when and how to retrieve | P1 |
| CAG | Cache-Augmented Generation, using cached context or knowledge to reduce repeated retrieval or processing | P1 |
| MAG | Verify the intended expansion; often used for memory-augmented or other generation architectures | P1 |
| Long-context generation | Supply larger context directly, with careful selection and ordering | P1 |
| Multimodal RAG | Retrieve and ground answers in images, audio, video or mixed documents | P1 |
| Self-reflective RAG | Evaluate retrieval or generated answers and revise when needed | P1 |

For every architecture, learn these dimensions:

- Architecture and data flow.
- Indexing and storage requirements.
- Query processing and retrieval algorithms.
- Latency and inference costs.
- Knowledge freshness and cache invalidation.
- Evaluation methodology.
- Security, access control and data isolation.
- Failure modes and recovery.
- When a simpler architecture is sufficient.

The most important practical ability is to explain why one architecture is appropriate for a particular workload—not merely to reproduce a tutorial.

### C. Agentic AI and multi-agent systems

Priority: P0 for reliable single-agent workflows; P1 for multi-agent specialization

- Agent fundamentals and autonomy boundaries.
- Tool calling, function schemas and tool result handling.
- ReAct, plan-and-execute and graph-based workflows.
- State machines, checkpointing and durable execution.
- Short-term memory, long-term memory and retrieval-backed memory.
- Human approval and human-in-the-loop execution.
- Supervisor-worker, planner-executor and specialist-agent patterns.
- Parallel execution, handoffs and agent communication.
- Multi-agent state management and conflict resolution.
- Tool security, sandboxing and permission boundaries.
- Timeouts, retry limits, idempotency and termination conditions.
- Agent evaluation, traces and task-completion measurement.

Important: Multi-agent systems are not automatically better than single-agent systems. Start with deterministic workflows and one agent. Add multiple agents only when task decomposition or independent specialization provides measurable value.

### D. MCP and enterprise integrations

Priority: P0

- MCP architecture, hosts, clients and servers.
- Tool discovery, invocation and result schemas.
- Resources, prompts and server capabilities.
- Local and remote transports.
- Authentication, authorization and transport security.
- Server deployment and lifecycle management.
- Error handling, retries and timeouts.
- Tool permissions and least-privilege access.
- Audit logging and observability.
- Building MCP servers over existing .NET services.
- Consuming MCP servers from an AI application.
- Integrating MCP with databases, internal APIs and enterprise applications.

Your .NET background is especially useful here: you can expose established business capabilities through carefully scoped tools without rewriting the entire enterprise backend.

### E. Evaluation, security and production reliability

Priority: P0

- Model evaluation and benchmark design.
- RAG retrieval and groundedness evaluation.
- Agent task completion and tool-call evaluation.
- Golden datasets and regression tests.
- LLM-as-a-judge limitations and human review.
- Prompt injection and jailbreak testing.
- PII protection and sensitive-data controls.
- Tenant isolation and authorization.
- Tracing, logs, metrics and alerts.
- Latency, token usage and cost tracking.
- Model and prompt versioning.
- Load testing, fallbacks and incident recovery.
- CI/CD gates for model and prompt changes.

Microsoft's current AI evaluation guidance is a useful reference for evaluating models, individual turns, full agent conversations and existing traces.

Microsoft Learn

+1

## 5. Your recommended technology stack

You do not need to learn every framework in the ecosystem. Build depth in one stack and learn to evaluate alternatives.

Python logo Icons, Logos, Symbols – Free Download PNG, SVG

AI development

P0Python, FastAPI, Pydantic, pytest, async/await and HTTP clients.

Intro to PyTorch: Part 1. A brief introduction to the PyTorch… | by Tony Flores | TDS Archive | Medium

Model and embedding ecosystem

P0PyTorch fundamentals, Hugging Face Transformers, Sentence Transformers and hosted LLM APIs.

Demystifying Agentic AI: Why LangGraph Outshines LangChain for Complex AI Workflows

RAG and agent orchestration

P0Learn LangGraph or an equivalent workflow framework, plus direct tool calling without a framework.

Homepage | DAO Systems Latino América

Data and retrieval

P0PostgreSQL, pgvector, full-text search and Redis basics. Add a dedicated vector database when the use case requires it.

Data Platform: Building An Azure DataHub | PTR

Cloud and enterprise integration

P0Azure identity, Azure OpenAI/Microsoft Foundry, managed secrets, containers, networking and CI/CD.

docker Logo PNG Vector (SVG) Free Download

Deployment and observability

P0Docker, OpenTelemetry concepts, structured logging, distributed tracing, automated evaluation and performance testing.

### Should you abandon .NET?

No. Keep .NET and Angular as strengths.

Use Python for AI experimentation and the surrounding ecosystem where it provides advantages. Use C#/.NET for established enterprise services, domain logic, integrations and systems where your team already has mature infrastructure. Both can coexist in one solution.

For example:

Angular frontend

Chat, document upload, approvals and monitoring UI

.NET business API

Identity, permissions, transactions and enterprise rules

Python AI service

LLM calls, RAG, orchestration, evaluations and model routing

PostgreSQL

Business data and vectors

LLM provider

Generation and embeddings

This architecture is a practical starting point, not a requirement. A single .NET application or a single Python service may be simpler for smaller workloads.

## 6. The three portfolio projects that matter most

Avoid building ten shallow chatbots. Build three substantial projects that prove you can solve enterprise problems end to end.

Enterprise Search & RAG Services

Project 1 — Enterprise knowledge intelligence platform

Must have- Ingest PDFs, knowledge articles and structured records.
- Implement hybrid RAG, reranking and citations.
- Enforce document-level permissions.
- Evaluate retrieval and answer quality.
- Add ingestion monitoring and source freshness.

Proves: RAG, data engineering, evaluation and production integration.

AI & Automation | Kinso Labs

Project 2 — Business workflow agent

Must have- Integrate with a mock CRM, ticketing system or order service.
- Let an agent retrieve context and call approved tools.
- Expose selected operations through MCP.
- Require human approval before sensitive changes.
- Add state persistence, audit logs and recovery.

Proves: agents, MCP, enterprise APIs and safe automation.

Example - Tracing and Evaluation for the OpenAI-Agents SDK - Langfuse

Project 3 — Production AI operations platform

Strong differentiator- Compare models and prompts using a fixed evaluation suite.
- Trace RAG and agent executions.
- Measure latency, token consumption and cost.
- Add retries, fallbacks, rate limits and regression gates.
- Deploy with authentication, monitoring and documentation.

Proves: you can move beyond a demo to a reliable production deployment.

For each project, publish an architecture diagram, README, demo, test results, evaluation report, security considerations and a short explanation of the business outcome. Do not publish real customer data, credentials or confidential company code.

## 7. How to prepare for FDE interviews

Expect more than coding questions. The exact interview process varies by employer, but prepare across these dimensions.

| Interview area | What you should be able to demonstrate |
| --- | --- |
| Coding | Python, APIs, data manipulation, debugging and tests |
| AI fundamentals | LLMs, embeddings, context windows, inference and model limitations |
| RAG system design | Ingestion, retrieval, reranking, grounding and evaluation |
| Agent design | Tools, state, workflow orchestration, safety and recovery |
| Enterprise architecture | Authentication, databases, APIs, permissions and integration |
| Production engineering | Monitoring, latency, cost, reliability and deployment |
| Customer problem-solving | Requirements discovery, ambiguity, prioritization and trade-offs |
| Communication | Explain a technical solution to engineers and nontechnical stakeholders |

### Practice these scenarios

1. A customer says their internal chatbot gives incorrect answers. How would you diagnose the issue?
2. When would you choose RAG over fine-tuning or long-context prompting?
3. How would you give an AI agent access to a customer's CRM without allowing unauthorized changes?
4. How would you evaluate an agent that performs a ten-step business workflow?
5. How would you reduce inference cost without degrading answer quality?
6. When should you use one agent, multiple agents, or a deterministic workflow?
7. How would you integrate an AI system with an existing .NET monolith?
8. What would you do if the prototype works but production accuracy is unacceptable?
9. How would you scope a two-week customer proof of concept?
10. How would you measure whether an AI deployment actually saves the customer time or money?

A strong answer should include requirements, assumptions, architecture, alternatives, failure modes, measurable acceptance criteria and a deployment plan.

## 8. Progress tracker for your transition

Use this checklist to track actual competence rather than just course completion.

## FDE readiness checklist

### 0/21

P0 — Foundations and core AI

[ ]Build a tested Python API with streaming LLM responses

[ ]Explain tokens, embeddings, attention and inference

[ ]Implement structured outputs and tool calling

[ ]Build a hybrid RAG system with citations

[ ]Create retrieval and answer evaluation datasets

[ ]Implement a safe single-agent workflow

[ ]Build and consume an MCP server

[ ]Deploy a secured AI application

P1 — Advanced GenAI engineering

[ ]Implement reranking and advanced RAG

[ ]Build a graph-based agent workflow

[ ]Create a bounded multi-agent workflow

[ ]Compare RAG, GraphRAG, CAG and memory-based approaches

[ ]Fine-tune a model with LoRA

[ ]Build a multimodal use case

[ ]Implement tracing, quality monitoring and cost controls

FDE readiness

[ ]Conduct a mock customer discovery session

[ ]Write an architecture decision record

[ ]Define business and technical success metrics

[ ]Demo an end-to-end enterprise use case

[ ]Document security and operational failure modes

[ ]Practice coding, system design and customer scenarios

 Reset progress

## 9. Learning resources — prioritize official documentation

- [Hugging Face Learn](<https://huggingface.co/learn?utm_source=chatgpt.com>) — Transformers, LLMs and fine-tuning.
- [PyTorch Tutorials](<https://pytorch.org/tutorials/?utm_source=chatgpt.com>) — neural networks and model implementation.
- [LangGraph Documentation](<https://docs.langchain.com/oss/python/langgraph/overview?utm_source=chatgpt.com>) — stateful agent workflows.
- [Model Context Protocol](<https://modelcontextprotocol.io/?utm_source=chatgpt.com>) — MCP architecture and implementation.
- [Microsoft Foundry documentation](<https://learn.microsoft.com/en-us/azure/ai-foundry/?utm_source=chatgpt.com>) — Azure-oriented AI application development.
- [Microsoft Foundry evaluation guide](<https://learn.microsoft.com/en-us/azure/ai-studio/how-to/evaluate-generative-ai-app?utm_source=chatgpt.com>) — model and application evaluation.
- [FastAPI documentation](<https://fastapi.tiangolo.com/?utm_source=chatgpt.com>) — Python API development.
- [OpenTelemetry documentation](<https://opentelemetry.io/docs/?utm_source=chatgpt.com>) — traces, metrics and logs.

## 10. Let's tailor this roadmap to your exact situation

I have assumed that you want an applied, production-focused FDE role rather than an ML research position. Three details will help me turn this into a much more specific study plan for you.

1. How much time can you dedicate weekly?

5–7 hours

12–15 hours/week 12–15 hours

20+ hours

2. Which cloud and enterprise stack do you use most?

Azure Azure / Microsoft ecosystem

AWS

Google Cloud

Mixed cloud or on-premises

3. Which role are you targeting?

AI Forward Deployed Engineer AI Forward Deployed Engineer at an AI product company

Enterprise AI / Solutions Engineer

AI Engineer building production applications

FDE at a frontier AI company

Python experience

No Python experience

Basic Python Basic Python

Comfortable with Python

 Build my personalized roadmap

[aced.io](<https://www.aced.io/blog/what-is-a-forward-deployed-engineer?utm_source=chatgpt.com>)
