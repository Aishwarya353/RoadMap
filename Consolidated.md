Part 2 — Generative AI, Transformers, LLMs and RAG
This is the transition from general AI knowledge to the core skills used in modern GenAI engineering.
Phase 6. Generative AI fundamentals
6.1 Understanding Generative AI
	• Definition and scope of GenAI
	• Generative vs. discriminative AI
	• Traditional AI vs. generative AI
	• Foundation models
	• Pretrained models
	• General-purpose vs. domain-specific models
	• Open-weight vs. closed-weight models
	• Hosted APIs vs. self-hosted inference
	• Training vs. inference
	• Capabilities and limitations of generative models
6.2 Types of generative models
	• Autoregressive models
	• Transformer-based language models
	• Variational autoencoders
	• Generative adversarial networks
	• Diffusion models
	• Normalizing flows
	• Energy-based models
	• Flow matching
	• Multimodal generative models
6.3 Common GenAI tasks
	• Text generation
	• Question answering
	• Summarization
	• Translation
	• Rewriting and editing
	• Information extraction
	• Classification using LLMs
	• Code generation
	• Conversational AI
	• Retrieval-grounded generation
	• Image generation and editing
	• Speech synthesis
	• Audio understanding
	• Video generation
	• Structured output generation
6.4 Core limitations
	• Hallucinations
	• Stale or missing knowledge
	• Context-window limitations
	• Non-deterministic outputs
	• Sensitivity to prompts
	• Bias and harmful outputs
	• Inconsistent reasoning
	• Computational and monetary cost
	• Privacy and security risks
Phase 7. Natural language processing (NLP)
7.1 Text preprocessing
	• Unicode and text encoding
	• Sentence segmentation
	• Word tokenization
	• Subword tokenization
	• Character tokenization
	• Normalization
	• Special tokens
	• Padding and truncation
	• Attention masks
	• Vocabulary construction
7.2 Traditional NLP
	• Bag of words
	• N-grams
	• TF-IDF
	• Word2Vec
	• GloVe
	• FastText
	• Named entity recognition
	• Part-of-speech tagging
	• Dependency parsing
	• Semantic similarity
	• Text classification
	• Information extraction
7.3 Tokenization for LLMs
	• Byte Pair Encoding (BPE)
	• WordPiece
	• SentencePiece
	• Unigram tokenization
	• Byte-level tokenization
	• Vocabulary size
	• Token IDs
	• Special tokens and delimiters
	• Token count and context limits
	• Tokenization effects on multilingual text
	• Token-level loss and perplexity
7.4 Embeddings
	• One-hot representations
	• Static word embeddings
	• Contextual embeddings
	• Sentence embeddings
	• Document embeddings
	• Dense vectors
	• Sparse vectors
	• Embedding dimensions
	• Cosine similarity
	• Dot-product similarity
	• Euclidean distance
	• Embedding normalization
	• Embedding model selection
	• Domain-specific embeddings
	• Multilingual embeddings
	• Embedding evaluation and drift
Tools to learn: Hugging Face Tokenizers, Sentence Transformers and embedding APIs.
Phase 8. Transformers and attention mechanisms
This is one of the most important phases in the entire roadmap.
8.1 Transformer architecture
	• Why recurrent architectures have limitations
	• Attention as a sequence-modeling mechanism
	• Encoder-only Transformers
	• Decoder-only Transformers
	• Encoder-decoder Transformers
	• Transformer blocks
	• Residual connections
	• Layer normalization
	• Feedforward network layers
	• Attention masks
	• Positional information
8.2 Attention mechanisms
	• Query, key and value vectors
	• Scaled dot-product attention
	• Self-attention
	• Cross-attention
	• Causal attention
	• Multi-head attention
	• Attention masks
	• Padding masks
	• Attention score matrices
	• Computational complexity of attention
	• Memory requirements
	• Attention implementation in PyTorch

From <https://github.com/Aishwarya353/RoadMap/blob/main/AI_RoadMap.md#part-2--generative-ai-transformers-llms-and-rag> 

Phase 9. Large language models (LLMs)
9.1 LLM architecture families
	• Encoder-only models
	• Decoder-only models
	• Encoder-decoder models
	• Dense models
	• Mixture-of-Experts models
	• Base models
	• Instruction-tuned models
	• Reasoning-oriented models
	• Multilingual models
	• Long-context models
	• Code-focused models
9.2 LLM pretraining
	• Training corpus preparation
	• Data filtering and deduplication
	• Data contamination
	• Tokenization and token IDs
	• Next-token prediction
	• Causal language modeling
	• Cross-entropy loss
	• Teacher-forced training
	• Batch construction
	• Sequence packing
	• Learning rate schedules
	• Warm-up and decay
	• Checkpointing
	• Distributed training
	• Compute and memory requirements
	• Training instability
	• Scaling laws and compute allocation
9.3 LLM post-training
	• Supervised fine-tuning (SFT)
	• Instruction tuning
	• Chat templates
	• Conversational datasets
	• Preference datasets
	• Human feedback
	• AI-generated preference feedback
	• Reward modeling
	• Reinforcement learning from human feedback (RLHF)
	• Direct Preference Optimization (DPO)
	• Proximal Policy Optimization (PPO)
	• Group Relative Policy Optimization (GRPO)
	• Rejection sampling
	• Distillation
	• Alignment and behavioral tuning
Note: These methods are related but not interchangeable. The appropriate approach depends on the training objective, model, data and available compute.
9.4 LLM inference
	• Prompt construction
	• Tokenization and decoding
	• Prefill and decode stages
	• Autoregressive generation
	• Greedy decoding
	• Beam search
	• Temperature
	• Top-k sampling
	• Top-p (nucleus) sampling
	• Repetition penalties
	• Stop sequences
	• Maximum output tokens
	• KV cache
	• Continuous batching
	• Speculative decoding
	• Quantized inference
	• Time to first token (TTFT)
	• Inter-token latency
	• Throughput and concurrency
9.5 LLM evaluation
	• Perplexity
	• Exact match
	• Accuracy and F1
	• BLEU and ROUGE
	• Semantic similarity
	• Benchmark-based evaluation
	• Human evaluation
	• Pairwise preference evaluation
	• LLM-as-a-judge
	• Calibration
	• Factuality
	• Instruction following
	• Tool-use accuracy
	• Reasoning evaluation
	• Robustness testing
	• Contamination and benchmark leakage
9.6 Working with pretrained models
	• Hugging Face Transformers
	• Hugging Face Hub
	• Model cards and configuration files
	• Tokenizers and chat templates
	• Loading pretrained models
	• Running inference pipelines
	• Text generation
	• Embedding extraction
	• Quantized model loading
	• GPU and CPU inference
	• Model licenses and usage restrictions
Project: Compare several pretrained models on the same question-answering and summarization tasks. Evaluate quality, latency, token usage and cost.
Phase 10. Prompt engineering and structured outputs
10.1 Prompt engineering fundamentals
	• System, developer and user instructions
	• Role and task specification
	• Context provision
	• Instruction hierarchy
	• Constraints and output requirements
	• Delimiters and structured prompt sections
	• Positive and negative instructions
	• Prompt clarity and ambiguity reduction
	• Few-shot examples
	• Zero-shot prompting
	• One-shot prompting
	• Few-shot prompting
	• Example selection and ordering
10.2 Advanced prompting techniques
	• Chain-of-thought prompting concepts
	• Self-consistency
	• Least-to-most prompting
	• Decomposition prompting
	• ReAct-style prompting
	• Plan-and-execute patterns
	• Reflection and critique loops
	• Retrieval-grounded prompting
	• Contextual prompting
	• Prompt chaining
	• Prompt templates
	• Dynamic prompt construction
	• Prompt compression
	• Prompt versioning and testing
These techniques are not universally beneficial. Evaluate them against a baseline, especially for reasoning tasks.
10.3 Structured generation
	• JSON outputs
	• JSON Schema
	• Structured Outputs APIs
	• Function and tool schemas
	• Pydantic models
	• Output validation
	• Parsing and serialization
	• Constrained decoding
	• Enum and field constraints
	• Schema evolution
	• Error recovery
	• Handling malformed responses
10.4 Prompt injection and robustness
	• Direct prompt injection
	• Indirect prompt injection
	• Untrusted input boundaries
	• Instruction conflicts
	• Data exfiltration risks
	• Prompt leakage
	• Jailbreak testing
	• Adversarial inputs
	• Input and output validation
	• Refusal handling
	• Prompt security testing
Project: Build an information-extraction application that converts unstructured text into validated JSON and measures extraction accuracy.
Phase 11. LLM APIs and application development
11.1 Model providers and interfaces
	• Hosted model APIs
	• Open-weight model serving
	• Chat completion interfaces
	• Responses-style interfaces
	• Text generation endpoints
	• Embedding endpoints
	• Image and audio endpoints
	• Streaming APIs
	• Authentication and secrets management
	• Model selection and fallback strategies
11.2 API engineering
	• HTTP requests and responses
	• SDK usage
	• Timeouts and retries
	• Exponential backoff
	• Rate limits
	• Token limits
	• Concurrent requests
	• Async inference
	• Streaming token output
	• Error handling
	• Idempotency
	• Request tracing
	• Usage and cost tracking
11.3 Application architecture
	• Python backend with FastAPI
	• REST endpoints
	• Request validation
	• Authentication and authorization
	• Frontend integration
	• Session management
	• Conversation persistence
	• Database integration
	• Background jobs
	• Caching
	• File uploads
	• Streaming user interfaces
	• Graceful failure and recovery
11.4 Model abstraction and routing
	• Provider-independent interfaces
	• Model registries
	• Model routing
	• Task-based model selection
	• Cost-based routing
	• Latency-based routing
	• Fallback models
	• Open-weight vs. hosted model trade-offs
	• Provider migration strategies
Project: Build a chat application with streaming responses, conversation history, authentication, rate limits and usage tracking.
Phase 12. Retrieval-Augmented Generation (RAG)
RAG is a major GenAI engineering skill. It combines a language model with external information so that responses can be grounded in retrieved documents.
12.1 RAG fundamentals
	• Why RAG is needed
	• LLM knowledge limitations
	• RAG vs. fine-tuning
	• RAG vs. long-context prompting
	• Basic RAG architecture
	• Retrieval, augmentation and generation
	• Grounded answers
	• Citations and source attribution
	• Knowledge freshness
	• RAG failure modes
12.2 Document ingestion
	• PDF processing
	• Word documents
	• HTML and web pages
	• Markdown and text
	• CSV and spreadsheets
	• Email and knowledge bases
	• OCR for scanned documents
	• Layout-aware parsing
	• Tables and figures
	• Metadata extraction
	• Document identifiers
	• Version tracking
	• Access-control metadata
12.3 Text chunking
	• Fixed-size chunking
	• Token-based chunking
	• Sentence-based chunking
	• Paragraph-based chunking
	• Recursive character splitting
	• Semantic chunking
	• Overlapping chunks
	• Parent-child chunking
	• Hierarchical chunking
	• Document structure-aware chunking
	• Chunk size and overlap tuning
	• Chunk quality evaluation
12.4 Embedding generation
	• Embedding model selection
	• Document embeddings
	• Query embeddings
	• Embedding normalization
	• Vector dimensions
	• Batch embedding
	• API and local embedding models
	• Multilingual embeddings
	• Embedding model versioning
	• Re-embedding strategies
12.5 Vector databases
	• Vector indexes
	• Similarity search
	• Approximate nearest neighbors
	• HNSW
	• IVF indexes
	• Product quantization
	• Metadata filtering
	• Namespace and collection design
	• Upserts and deletions
	• Persistence
	• Index tuning
	• Multi-tenant isolation
Technologies to explore include FAISS, pgvector, Qdrant, Milvus, Weaviate and Pinecone. Select one or two to learn deeply before exploring the rest.
12.6 Retrieval strategies
	• Dense vector retrieval
	• Sparse retrieval
	• BM25
	• Keyword search
	• Hybrid retrieval
	• Metadata filtering
	• Query rewriting
	• Query expansion
	• Multi-query retrieval
	• Hypothetical Document Embeddings (HyDE)
	• Maximum Marginal Relevance (MMR)
	• Parent-document retrieval
	• Multi-hop retrieval
	• Temporal and metadata-aware retrieval
12.7 Reranking
	• Cross-encoder rerankers
	• Bi-encoder retrieval
	• Retrieve-then-rerank
	• Candidate generation
	• Relevance scoring
	• Top-k selection
	• Diversity and redundancy reduction
	• Latency-quality trade-offs
12.8 Generation and grounding
	• Context assembly
	• Context ordering
	• Prompt construction
	• Source citations
	• Evidence-based responses
	• Abstention when evidence is insufficient
	• Conflicting document handling
	• Context-window budgeting
	• Source freshness
	• Permission-aware retrieval
12.9 Advanced RAG
	• Corrective RAG
	• Self-reflective RAG
	• Adaptive RAG
	• Agentic RAG
	• Graph RAG
	• Knowledge graph retrieval
	• Hierarchical retrieval
	• Multi-modal RAG
	• Table-aware RAG
	• Long-document retrieval
	• Temporal RAG
	• Multi-tenant enterprise RAG
12.10 RAG evaluation
	• Retrieval precision and recall
	• Hit rate
	• Mean Reciprocal Rank (MRR)
	• Normalized Discounted Cumulative Gain (NDCG)
	• Context relevance
	• Context recall
	• Faithfulness
	• Answer relevance
	• Citation correctness
	• Answer completeness
	• End-to-end latency
	• Cost per query
	• Retrieval ablation testing
Project: Build a document question-answering system with PDF ingestion, hybrid retrieval, reranking, citations and an evaluation dataset.
Phase 13. AI agents and tool use
13.1 Agent fundamentals
	• LLM applications vs. agents
	• Tools and actions
	• Agent state
	• Goals and constraints
	• Planning and execution
	• Observation and feedback
	• Agent loops
	• Stopping conditions
	• Deterministic workflows vs. autonomous agents
	• Human-in-the-loop systems
13.2 Tool calling
	• Function calling
	• Tool schemas
	• Tool selection
	• Argument generation
	• Input validation
	• Tool execution
	• Tool result messages
	• Multi-step tool calls
	• Parallel tool execution
	• Tool error handling
	• Tool permissions
	• Sandboxed execution
13.3 Agent reasoning and planning
	• ReAct patterns
	• Plan-and-execute
	• Task decomposition
	• Subgoal generation
	• State transitions
	• Reflection
	• Self-correction
	• Retry policies
	• Workflow graphs
	• Conditional routing
	• Checkpointing
	• Termination and loop prevention
13.4 Agent memory
	• Short-term conversation state
	• Long-term memory
	• Episodic memory
	• Semantic memory
	• Working memory
	• User preferences
	• Memory retrieval
	• Memory summarization
	• Memory updates and deletion
	• Privacy-aware memory
	• Avoiding stale or contradictory memory
13.5 Multi-agent systems
	• Supervisor-worker architecture
	• Planner-executor architecture
	• Specialized agents
	• Agent delegation
	• Message passing
	• Shared state
	• Agent coordination
	• Consensus and conflict resolution
	• Parallel agent execution
	• Agent communication protocols
	• Multi-agent evaluation
	• Cost and reliability management
13.6 Agent frameworks and protocols
	• Direct tool calling without a framework
	• LangGraph
	• LangChain
	• LlamaIndex workflows
	• Semantic Kernel
	• AutoGen-style multi-agent systems
	• Model Context Protocol (MCP)
	• MCP clients and servers
	• Tools, resources and prompts in MCP
	• Authentication and authorization
	• Protocol security and trust boundaries
13.7 Production agents
	• Approval gates for sensitive actions
	• Human review
	• Idempotent operations
	• Transaction safety
	• Tool access control
	• Audit logs
	• Rate limits
	• Budget limits
	• Maximum iteration counts
	• Recovery and resume
	• Agent traces
	• Deterministic test environments
Project: Create an agent that searches an approved knowledge base, calls external tools, produces a structured report and requests human approval before performing sensitive actions.
Phase 14. Fine-tuning and customization
14.1 When to fine-tune
	• Prompting vs. RAG vs. fine-tuning
	• Domain adaptation
	• Instruction following
	• Style and format consistency
	• Task-specific behavior
	• Data availability
	• Training and inference costs
	• Model licensing constraints
	• Fine-tuning success criteria
14.2 Fine-tuning data
	• Instruction-response pairs
	• Chat conversation formats
	• System and user messages
	• Input-output examples
	• Dataset filtering
	• Data deduplication
	• Quality scoring
	• Train-validation splits
	• Synthetic training data
	• Data contamination
	• Dataset balance
	• Data privacy
14.3 Supervised fine-tuning
	• Full-parameter fine-tuning
	• Training objectives
	• Loss masking
	• Sequence packing
	• Learning rate selection
	• Batch size and gradient accumulation
	• Training schedules
	• Checkpoint selection
	• Validation loss
	• Catastrophic forgetting
	• Overfitting detection
14.4 Parameter-efficient fine-tuning
	• Adapter methods
	• Low-Rank Adaptation (LoRA)
	• Quantized LoRA (QLoRA)
	• Rank and alpha parameters
	• Target module selection
	• Adapter training
	• Adapter merging
	• Multiple adapters
	• Memory and compute trade-offs
14.5 Preference optimization
	• Preference pairs
	• Reward models
	• RLHF
	• DPO
	• PPO
	• GRPO
	• Rejection sampling
	• Preference-data quality
	• Reward hacking
	• Alignment evaluation
14.6 Distillation and compression
	• Teacher-student learning
	• Logit distillation
	• Response distillation
	• Synthetic data distillation
	• Model pruning
	• Quantization
	• Weight-only quantization
	• Activation quantization
	• Quantization-aware training
	• Quality and speed trade-offs
14.7 Training tools
	• Hugging Face Transformers
	• TRL
	• PEFT
	• Accelerate
	• DeepSpeed
	• FSDP
	• Experiment tracking
	• Training checkpoints
	• GPU memory profiling
Project: Fine-tune a small open-weight model with LoRA on a high-quality task-specific dataset. Compare it with the original model on a held-out evaluation set.
Phase 15. Multimodal AI and generative media
15.1 Vision-language models
	• Image encoders
	• Vision Transformers
	• Image patch embeddings
	• Vision-language alignment
	• Contrastive learning
	• Image-text embeddings
	• Image question answering
	• Visual reasoning
	• OCR and document understanding
	• Object recognition
	• Image captioning
	• Video understanding
15.2 Image generation
	• Diffusion model fundamentals
	• Forward noise process
	• Reverse denoising process
	• Denoising objectives
	• Latent diffusion
	• Text encoders
	• Conditioning
	• Classifier-free guidance
	• Sampling schedulers
	• Image-to-image generation
	• Inpainting and outpainting
	• ControlNet-style conditioning
	• Personalization and fine-tuning
	• Image evaluation
15.3 Audio and speech
	• Digital audio basics
	• Sampling rates
	• Waveforms and spectrograms
	• Audio tokenization
	• Speech recognition (ASR)
	• Text-to-speech (TTS)
	• Speech-to-speech systems
	• Speaker diarization
	• Voice activity detection
	• Audio captioning
	• Music generation
	• Audio-language models
	• Streaming speech interfaces
	• Speech latency and turn-taking
15.4 Video generation and understanding
	• Video frame sampling
	• Temporal representations
	• Video-language models
	• Text-to-video generation
	• Image-to-video generation
	• Temporal consistency
	• Motion conditioning
	• Video summarization
	• Video retrieval
	• Audio-video synchronization
	• Evaluation of generated video
15.5 Multimodal RAG and agents
	• Image and document retrieval
	• Video retrieval
	• Audio search
	• Cross-modal embeddings
	• Multimodal document chunking
	• Visual tool use
	• Real-time multimodal agents
	• Combining vision, audio and text
	• Modality-specific evaluation
Project: Build a multimodal assistant that accepts documents and images, answers questions with evidence, and supports speech input or output.
Phase 16. Evaluation, safety and responsible AI
16.1 Evaluation methodology
	• Define task-specific success metrics
	• Create representative test sets
	• Golden datasets
	• Offline evaluation
	• Online evaluation
	• Human preference studies
	• Pairwise comparisons
	• Regression tests
	• Model and prompt comparisons
	• Statistical significance
	• Evaluation reproducibility
16.2 LLM evaluation
	• Instruction-following accuracy
	• Factuality
	• Faithfulness
	• Hallucination rates
	• Reasoning benchmarks
	• Code generation tests
	• Tool-use success
	• Context adherence
	• Citation verification
	• Structured-output validity
	• Refusal accuracy
	• Robustness under paraphrasing
16.3 RAG and agent evaluation
	• Retrieval recall
	• Retrieval precision
	• Evidence quality
	• Answer correctness
	• Tool-selection accuracy
	• Tool-argument correctness
	• Task completion rate
	• Recovery from tool failures
	• Multi-step execution accuracy
	• Human intervention rate
	• Cost per completed task
16.4 Safety and security
	• Prompt injection
	• Jailbreak resistance
	• Sensitive-data leakage
	• Personally identifiable information
	• Training-data privacy
	• Model access controls
	• Tool permission boundaries
	• Malicious document handling
	• Unsafe tool execution
	• Output validation
	• Adversarial testing
	• Abuse monitoring
16.5 Responsible AI and governance
	• Bias and fairness
	• Explainability and transparency
	• Data provenance
	• Copyright and licensing
	• Privacy requirements
	• Human oversight
	• Auditability
	• Model documentation
	• Risk assessment
	• Regulatory compliance
	• Content provenance
	• Incident response
Phase 17. Production deployment and LLMOps
17.1 Backend and serving
	• FastAPI
	• Async request handling
	• Streaming responses
	• Background tasks
	• Request validation
	• Authentication
	• Authorization
	• Database connections
	• Caching
	• API gateways
	• Load balancing
17.2 Deployment infrastructure
	• Docker
	• Container registries
	• Kubernetes fundamentals
	• Cloud deployment
	• GPU instances
	• Secrets management
	• CI/CD pipelines
	• Infrastructure as code
	• Autoscaling
	• Blue-green and canary deployments
	• Rollbacks
	• Disaster recovery
17.3 Model serving
	• Hosted inference APIs
	• vLLM
	• Hugging Face TGI
	• llama.cpp
	• ONNX Runtime
	• TensorRT-LLM
	• Batching
	• Continuous batching
	• KV cache optimization
	• Quantized inference
	• GPU utilization
	• Model parallelism
	• Distributed inference
17.4 Monitoring and observability
	• Request and response traces
	• Latency monitoring
	• Token usage
	• Cost tracking
	• Error rates
	• Time to first token
	• Throughput
	• Model quality monitoring
	• Retrieval quality monitoring
	• Data drift
	• Model drift
	• Prompt and model versioning
	• Alerts and incident handling
17.5 Performance and cost optimization
	• Model selection
	• Prompt shortening
	• Context reduction
	• Response caching
	• Semantic caching
	• Batch inference
	• Quantization
	• Smaller-model routing
	• Output-token limits
	• Retrieval optimization
	• Concurrency control
	• Cost per request
	• Quality-cost trade-offs
17.6 LLMOps and MLOps
	• Experiment tracking
	• Model registries
	• Dataset versioning
	• Evaluation pipelines
	• Automated regression tests
	• Deployment gates
	• Prompt registries
	• Model version management
	• Rollback procedures
	• Production feedback loops
Project: Deploy a RAG application with authentication, Docker, automated tests, tracing, evaluation, monitoring and cost tracking.
Phase 18. Advanced GenAI and research topics
These topics are useful for specialization, advanced engineering roles or research-oriented work.
18.1 Advanced LLM architecture
	• Sparse and conditional computation
	• Mixture of Experts
	• Long-context architectures
	• Advanced attention mechanisms
	• Recurrent and hybrid architectures
	• State-space models
	• Memory-augmented models
	• Retrieval-enhanced language models
	• Multimodal foundation models
	• Architecture scaling trade-offs
18.2 Advanced reasoning
	• Reasoning-oriented model training
	• Process supervision
	• Outcome supervision
	• Search-based reasoning
	• Tree search
	• Self-consistency
	• Verifier models
	• Reward models
	• Test-time compute
	• Tool-augmented reasoning
	• Limits of benchmark-based reasoning evaluation
18.3 Advanced training systems
	• Distributed data parallelism
	• Tensor parallelism
	• Pipeline parallelism
	• Expert parallelism
	• Sequence parallelism
	• FSDP and ZeRO
	• Memory optimization
	• Checkpoint sharding
	• Fault-tolerant training
	• Large-scale data pipelines
	• Training throughput profiling
18.4 Advanced retrieval and knowledge systems
	• Knowledge graph construction
	• Graph-based retrieval
	• Entity linking
	• Graph traversal
	• Hybrid graph-vector retrieval
	• Temporal knowledge
	• Multi-hop question answering
	• Structured database querying
	• Text-to-SQL
	• Enterprise permissions and data governance
18.5 Research skills
	• Reading research papers
	• Reproducing baselines
	• Identifying assumptions
	• Designing controlled experiments
	• Ablation studies
	• Benchmark selection
	• Statistical uncertainty
	• Research code organization
	• Reproducibility
	• Writing technical reports
	• Tracking emerging architectures and methods
18.6 Specialized application domains
	• AI coding assistants
	• Enterprise knowledge assistants
	• Customer support automation
	• Finance and document intelligence
	• Healthcare information systems
	• Legal document analysis
	• Education and tutoring
	• Scientific discovery
	• Robotics and embodied AI
	• Synthetic data generation
	• Creative tools
Domain-specific deployments require additional validation, privacy safeguards and expert oversight where appropriate.
Phase 19. Projects to complete the roadmap
Build projects in increasing order of difficulty rather than attempting a large autonomous agent immediately.
Running Your Own AI is Easier Than You Think: A Beginner’s Guide | by Amar Chetri, PhD | Write A Catalyst | Feb, 2026 | Medium
Project 1 — LLM chatbot
BeginnerBuild a chatbot with an LLM API, conversation history, streaming responses and configurable model settings.
Building RAG Chatbots: Bridging LLMs with Private Data | Rahul K B | Staff Machine Learning Engineer
Project 2 — Document RAG assistant
IntermediateIngest PDFs, chunk text, generate embeddings, retrieve relevant passages, rerank results and return cited answers.
AI Agent Architecture: How Agents Think, Remember, and Act
Project 3 — Tool-using AI agent
IntermediateCreate an agent that calls APIs, validates tool inputs, manages state and requests approval for sensitive actions.
Project 4 — Fine-tuned LLM
AdvancedFine-tune an open-weight model using LoRA, compare it with the base model and report held-out evaluation results.
Splunk Observability Cloud | Splunk
Project 5 — Production GenAI platform
AdvancedDeploy a secure application with automated evaluation, observability, caching, model routing and cost controls.
Phase 20. Recommended learning resources
Use official documentation and practical exercises as your primary sources.
	• Python: Python — Official tutorial
	• Machine learning: scikit-learn — User guide
	• Deep learning: PyTorch — Official tutorials
	• Transformers and LLMs: Hugging Face — Learning courses
	• LLM application development: LangChain — Documentation
	• Retrieval and indexing: LlamaIndex — Documentation
	• Agent protocols: Model Context Protocol — Official documentation
	• Model training and fine-tuning: Hugging Face TRL — Documentation
	• Production inference: vLLM — Documentation
Phase 21. Suggested study timeline
A realistic timeline depends on your existing knowledge and how much time you can spend building projects.
Learning stage	Estimated time
Python and software foundations	2–4 weeks
Mathematics and data foundations	3–6 weeks
Machine learning and deep learning	4–8 weeks
Transformers and LLM fundamentals	3–5 weeks
Prompting, APIs and structured outputs	1–3 weeks
RAG and retrieval systems	3–5 weeks
Agents and tool use	2–4 weeks
Fine-tuning and multimodal AI	4–8 weeks
Deployment, evaluation and LLMOps	3–6 weeks
Advanced topics and portfolio projects	Ongoing

These estimates overlap when topics are learned together. A focused learner with prior programming experience might develop practical GenAI engineering skills in several months; mastering model training, multimodal systems and advanced research takes substantially longer.
Final checklist
Track your progress
0/20
Foundations
[ ]Python and software engineering
[ ]Linear algebra, calculus and probability
[ ]Data preparation and SQL
[ ]Machine learning and evaluation
[ ]Deep learning and PyTorch
Core GenAI
[ ]Tokenization and embeddings
[ ]Transformer architecture and attention
[ ]LLM pretraining and post-training
[ ]Prompt engineering and structured outputs
[ ]LLM APIs and inference
Application engineering
[ ]RAG and vector databases
[ ]Hybrid retrieval and reranking
[ ]Agents, tools and MCP
[ ]Fine-tuning and quantization
[ ]Multimodal AI
Production readiness
[ ]Evaluation and regression testing
[ ]Security, privacy and safety
[ ]Deployment and model serving
[ ]Monitoring, tracing and cost control
[ ]Portfolio projects and documentation

From <https://github.com/Aishwarya353/RoadMap/blob/main/AI_RoadMap.md#part-2--generative-ai-transformers-llms-and-rag> 

Complete 16-week roadmap for Agentic AI in .NET
Assumption: you know basic programming concepts. If you are new to C#, spend an extra 2–4 weeks on the fundamentals.
Recommended pace: 1–2 hours daily, with a working project at the end of each phase.
Weeks 1–2: C# and .NET fundamentals
Learn:
	• Classes, interfaces, records, and generics.
	• LINQ, collections, and exception handling.
	• async/await, Task, and CancellationToken.
	• Dependency injection and configuration.
	• HTTP clients, JSON serialization, and NuGet.
Project: Build a C# console application that calls a public API, processes JSON, and produces a summary.
Weeks 3–4: LLM integration
Learn:
	• LLM fundamentals, prompts, and context windows.
	• Model API authentication and configuration.
	• Chat messages, conversation history, and streaming.
	• Structured output and JSON validation.
	• Microsoft.Extensions.AI and IChatClient.
Project: Build a C# console chatbot that summarizes documents and returns structured JSON.
Resource: Build AI apps with .NET.
Weeks 5–6: Function calling and tools
Learn:
	• Define C# methods as AI-callable functions.
	• AIFunctionFactory and function invocation.
	• Connect APIs, business logic, and databases.
	• Validate arguments and handle failures.
	• Limit tool permissions and require approval for sensitive actions.
Project: Build a customer-support assistant that looks up orders and checks delivery status.
Resource: AI tool calling in .NET.
Microsoft Learn
Weeks 7–8: RAG and knowledge retrieval
Learn:
	• PDF and document processing.
	• Chunking, embeddings, and vector search.
	• Retrieval-Augmented Generation.
	• Metadata filtering and source citations.
	• Connecting your own SQL or document data.
	• Evaluating retrieval relevance.
Project: Build an internal company-document assistant that answers questions using relevant documents.
Resource: Microsoft .NET AI documentation.
Weeks 9–10: Agent development
Learn:
	• Agent instructions and tool selection.
	• Observe–decide–act loops.
	• Planning and task decomposition.
	• Memory, conversation state, and stopping rules.
	• Microsoft Agent Framework fundamentals.
	• Retries, timeouts, and error recovery.
Project: Build a research agent that searches approved sources, gathers evidence, and generates a report.
Resource: Microsoft Agent Framework documentation.
Microsoft Learn
Weeks 11–12: Workflows and multi-agent systems
Learn:
	• Workflow graphs and conditional routing.
	• Supervisor and specialist agents.
	• Delegation, handoffs, and shared state.
	• Human-in-the-loop workflows.
	• MCP for connecting external tools and context.
	• Checkpoints and resumable execution.
Project: Build a research workflow with researcher, analyst, and reviewer agents.
Weeks 13–14: Production engineering
Learn:
	• ASP.NET Core Web APIs.
	• Dependency injection and configuration.
	• Logging, tracing, and evaluation.
	• Prompt injection and tool security.
	• Authentication, authorization, and secret management.
	• Unit tests, integration tests, and failure handling.
Project: Expose your agent through a secured ASP.NET Core API and add automated tests.
Weeks 15–16: Deployment and portfolio
Learn:
	• Docker fundamentals.
	• Cloud deployment, such as Azure App Service or Container Apps.
	• Persistent storage and background jobs.
	• Cost tracking and performance monitoring.
	• README files, architecture diagrams, and demonstrations.
Project: Deploy an end-to-end Agentic AI application with a web API, tools, retrieval, and evaluation.

From <https://github.com/Aishwarya353/RoadMap/blob/main/AI_RoadMap.md#part-2--generative-ai-transformers-llms-and-rag> 

Is this roadmap enough for an FDE transformation?
Yes — this is a strong foundation for becoming an AI-focused Forward Deployed Engineer (FDE), but it is not sufficient on its own. It covers GenAI theory, LLMs, RAG, agents, fine-tuning, evaluation, and deployment in impressive depth.
The main gap is that it is closer to a comprehensive GenAI engineer and AI specialist roadmap than a complete FDE roadmap.
An FDE needs to do more than build an AI application. They must understand a customer's business problem, integrate AI with existing systems, handle messy real-world data, deploy reliably, and demonstrate measurable business value.
You don't need to master every topic in Phases 6–21 before becoming job-ready. You need to prioritize the skills that enable you to build, integrate, debug, and ship real solutions.
1. How well does your roadmap cover FDE skills?
GenAI, LLMs and transformers
Excellent coverage across Phases 6–10 and 14–15.
Strong
RAG and agent engineering
Excellent breadth; prioritize reliable workflows over complex autonomous agents.
Strong
Backend and software engineering
Good coverage, but needs deeper practice with testing, databases, APIs and debugging.
Strengthen
Production and infrastructure
Good topics listed; practical cloud, networking, observability and incident handling are essential.
Strengthen
Customer-facing engineering
Needs an explicit focus on discovery, integrations, stakeholder communication and business outcomes.
Add
These are qualitative assessments of the roadmap, not measured scores.
2. The six missing areas you should add
These are the changes I would make before following the roadmap.
1. Customer discovery and solution engineering
This is the biggest difference between a conventional GenAI developer and an FDE.
Learn to:
	• Translate vague customer requests into technical requirements.
	• Conduct discovery calls and ask the right questions.
	• Map business workflows and identify automation opportunities.
	• Define success metrics, such as reduced handling time, fewer errors or increased conversion.
	• Identify data sources, system owners, access restrictions and integration constraints.
	• Build proofs of concept quickly and validate them with users.
	• Explain technical trade-offs to nontechnical stakeholders.
Practice project: A company asks, "Can you build an AI assistant for our support team?" Interview a hypothetical stakeholder, map the current workflow, define success metrics and produce a solution design before writing code.
2. Strong software engineering and systems integration
Your roadmap mentions FastAPI, databases and APIs, but an FDE must be able to integrate with systems that already exist.
Add these topics:
	• Python proficiency, type hints, classes, modules and packaging.
	• Git, GitHub, branching, code reviews and conflict resolution.
	• SQL, PostgreSQL, joins, indexes, transactions and migrations.
	• REST APIs, webhooks, OAuth 2.0, API keys and pagination.
	• Authentication, authorization, RBAC and tenant isolation.
	• Unit tests, integration tests, mocks and end-to-end testing.
	• Async programming, concurrency, retries, timeouts and idempotency.
	• Reading unfamiliar codebases, debugging stack traces and diagnosing production failures.
Practice project: Build an AI support assistant that connects to a mock CRM and ticketing API, retrieves customer information, creates tickets and logs every action.
3. Data engineering and enterprise data integration
RAG quality depends heavily on the quality, freshness and permissions of the underlying data.
Add:
	• SQL and relational data modeling.
	• ETL/ELT pipelines and scheduled synchronization.
	• Data validation, deduplication and normalization.
	• CSV, JSON, PDFs, spreadsheets and APIs.
	• Incremental ingestion and change-data processing.
	• Data lineage, provenance and document versioning.
	• Enterprise permissions and row-level or document-level access control.
	• Handling deleted, stale, duplicated and conflicting records.
Practice project: Build a knowledge assistant that syncs documents from a source system, detects updates and deletions, enforces access permissions and cites the current source.
4. Cloud, networking and production operations
Phase 17 is a good starting point, but listing infrastructure tools isn't the same as being able to operate a deployed application.
Focus on:
	• Linux and command-line debugging.
	• DNS, HTTP/HTTPS, TLS, ports, proxies and firewalls.
	• Docker images, containers, volumes and networking.
	• One cloud platform: Azure, AWS or GCP.
	• Cloud identity and access management, secret storage and private networking.
	• CI/CD, automated deployment, rollback and environment configuration.
	• Logs, metrics, traces, dashboards and alerts.
	• Incident investigation, root-cause analysis and reliability.
	• Cost estimation, load testing and capacity planning.
You don't need to master Kubernetes immediately. Learn Docker and deploy to a managed cloud service first, then learn Kubernetes if your target roles require it.
5. AI evaluation, security and reliability
Your roadmap already covers these topics well conceptually. The missing element is applying them systematically to real applications.
Learn to:
	• Create a representative evaluation dataset before tuning prompts.
	• Compare baseline and improved implementations.
	• Measure retrieval quality separately from answer quality.
	• Test hallucinations, citation accuracy and unsupported claims.
	• Test prompt injection through retrieved documents.
	• Prevent unauthorized tool calls and cross-tenant data leakage.
	• Use deterministic workflows and approval gates for sensitive actions.
	• Measure latency, token usage, cost per task and failure rates.
	• Implement regression tests whenever prompts, models or data pipelines change.
Practice project: Create 100–200 representative test questions for your RAG application. Track answer correctness, retrieval recall, citation accuracy, latency and cost, and demonstrate improvements with measured results.
6. Communication and customer delivery
An FDE frequently works directly with customer engineering teams, product managers and business stakeholders.
Practice:
	• Writing technical discovery notes and requirements.
	• Creating architecture diagrams and integration plans.
	• Explaining trade-offs between speed, cost, accuracy and security.
	• Giving demos and gathering user feedback.
	• Documenting deployment and troubleshooting procedures.
	• Managing changing requirements and delivering iterative improvements.
	• Presenting results in terms of business impact.
A working application is valuable. A working application with clear documentation, measurable results and a convincing demo is much more valuable.
3. Which phases should you prioritize?
Your roadmap has a lot of material. Here is how I would reorganize it for FDE preparation.
1
Foundations and backend engineering
Python, Git, SQL, HTTP, APIs, testing, async programming, Linux.
Must master
2
LLM application engineering
Phases 6–11: tokens, embeddings, transformer concepts, prompting, APIs and structured outputs.
Must master
3
Production-grade RAG
Phase 12: ingestion, retrieval, hybrid search, reranking, permissions, citations and evaluation.
Must master
4
Tools, integrations and workflows
Phase 13: tool calling, state management, deterministic workflows, permissions and human approval.
Must master
5
Cloud deployment and LLMOps
Phase 17: Docker, one cloud platform, CI/CD, monitoring, tracing, reliability and cost control.
Must master
6
Fine-tuning, multimodal AI and advanced research
Phases 14, 15 and 18. Learn the concepts, but go deep only when your target roles need them.
Specialize later
Keep the transformer and LLM fundamentals. You should understand attention, embeddings, inference, context windows and model trade-offs. However, you do not need to implement distributed pretraining or master every optimization algorithm to build strong FDE applications.
4. The portfolio projects that would make you FDE-ready
I would prioritize these four projects over completing every theoretical topic.

Project 1 — Enterprise knowledge assistant
Intermediate
Build a RAG system with document ingestion, hybrid search, reranking, citations, access control and a repeatable evaluation suite.
Demonstrates: retrieval, data pipelines, evaluation and grounding.

Project 2 — Customer support workflow agent
Intermediate–advanced
Connect to mock CRM, order and ticket APIs. Let the assistant look up information, draft responses and execute permitted actions with human approval.
Demonstrates: API integration, tool calling, permissions and workflow reliability.

Project 3 — Production AI service
Advanced
Deploy one of the applications with Docker, authentication, CI/CD, tracing, automated tests, rate limits, cost monitoring and failure recovery.
Demonstrates: production ownership, cloud deployment and debugging.

Project 4 — Customer-specific FDE implementation
Portfolio differentiator
Start with a realistic business case. Produce discovery notes, architecture, a working integration, test results, a deployment guide and a demo explaining the business impact.
Demonstrates: the complete FDE delivery cycle, not just model knowledge.
For each project, publish a clean GitHub repository with:
	• A clear README and setup instructions.
	• An architecture diagram.
	• A demo video or screenshots.
	• Automated tests and a sample evaluation dataset.
	• Documented design decisions and limitations.
	• Before-and-after metrics wherever you can measure them.
5. What about the .NET Agentic AI roadmap?
The second roadmap is useful if you want to target FDE roles working in Microsoft-heavy enterprise environments.
The C#/.NET track covers useful skills such as dependency injection, asynchronous programming, API integration, RAG, agent workflows, MCP, ASP.NET Core and Azure deployment.
My recommendation:
	• If your target employers use Python-based AI stacks: prioritize Python, FastAPI and the broader GenAI roadmap.
	• If your target employers use Microsoft enterprise stacks: combine the .NET roadmap with the missing customer-facing, data engineering and production skills above.
	• If you're undecided: choose one language and stack for your first two projects. Avoid trying to master Python and .NET simultaneously before you have shipped a complete application.
You can learn the second ecosystem later without losing the transferable skills you develop in the first.
6. A practical 16-week FDE preparation plan
Assuming you already know basic programming and can spend around 2–3 focused hours daily, this is a reasonable preparation plan. It is not a guarantee of job readiness; your starting level and project complexity will affect the timeline.
Track your progress
0 of 7 phases

Weeks 1–2Software engineering and integrationPython, Git, SQL, HTTP, REST APIs, testing and debugging.

Weeks 3–4LLMs and application developmentModel APIs, prompting, structured outputs, streaming, validation and cost tracking.

Weeks 5–7Production RAGIngestion, chunking, embeddings, hybrid retrieval, reranking, citations and evaluation.

Weeks 8–9Tools and business workflowsTool calling, API integrations, state, approvals, retries and error recovery.

Weeks 10–12Deploy and operateDocker, cloud deployment, authentication, CI/CD, monitoring, tracing and security.

Weeks 13–14Customer integration projectSolve a realistic business problem, integrate multiple systems and measure outcomes.

Weeks 15–16Portfolio and interviewsPolish projects, write architecture documents, record demos and practice technical and customer discovery interviews.
Spend a substantial portion of this time coding, testing and debugging rather than just watching tutorials or reading documentation.
7. How do you know you're ready for FDE roles?
You should be able to answer "yes" to most of these questions:
	• Can I build and debug a backend application without following a tutorial step by step?
	• Can I integrate an LLM with existing APIs, databases and authentication systems?
	• Can I build a RAG system and demonstrate its retrieval and answer quality using a test dataset?
	• Can I prevent the assistant from accessing data or performing actions it is not authorized to access or perform?
	• Can I deploy the application, monitor it and investigate failures?
	• Can I explain the system's latency, reliability, quality and cost trade-offs?
	• Can I understand an unfamiliar customer's technical environment and propose a workable integration?
	• Can I present a demo and explain the measurable business value of my solution?
If you can do these things and have two or three strong projects to demonstrate them, you have a much more credible FDE profile than someone who has simply completed an extensive AI syllabus.
My final recommendation: Keep your roadmap as the technical reference, but add customer discovery, enterprise integration, data engineering and production ownership as explicit learning tracks. Prioritize shipping complete applications over mastering every advanced GenAI topic.
One important question that would help me tailor the roadmap: what is your current background — software developer, data/ML engineer, student, or working in another field? That determines which parts you can skip and where your transformation needs the most work.


