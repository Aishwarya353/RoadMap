# Generative AI — Complete Roadmap (Part 1 of Several)

This roadmap is designed to take you from absolute beginner to Generative AI engineer, covering the foundations, mathematics, programming, machine learning, deep learning, LLMs, RAG, agents, multimodal AI, fine-tuning, deployment, evaluation, and advanced research.

The goal is not just to learn concepts, but to understand how to build, evaluate, deploy, and maintain real-world GenAI applications.

## The complete learning path

Phase 1 — Programming foundations

Python, Git, Linux, APIs, SQL, software engineering

Phase 2 — Mathematics and data foundations

Linear algebra, calculus, probability, statistics, data processing

Phase 3 — Machine learning and deep learning

Classical ML, neural networks, optimization, CNNs, sequence models

Phase 4 — Generative AI fundamentals

Tokenization, embeddings, Transformers, attention, model families

Phase 5 — Large language models

Pretraining, prompting, inference, context windows, reasoning, APIs

Phase 6 — RAG and knowledge systems

Document ingestion, chunking, vector search, hybrid retrieval, reranking

Phase 7 — AI agents and workflows

Tool calling, planning, memory, state, multi-agent systems, MCP

Phase 8 — Fine-tuning and model training

SFT, LoRA, QLoRA, preference optimization, distillation, quantization

Phase 9 — Multimodal and generative models

Image, audio, video, vision-language models, diffusion, speech

Phase 10 — Production GenAI and LLMOps

Backend, deployment, testing, monitoring, security, cost optimization

Phase 11 — Evaluation, safety and governance

Benchmarks, hallucinations, red teaming, privacy, responsible AI

Phase 12 — Advanced topics and specialization

Reasoning models, distributed training, research, domain-specific AI, capstone projects

How to use this roadmap: Follow the phases in order if you're starting from scratch. If you already know Python and machine learning, you can skip the introductory material and focus on the LLM and GenAI sections. The full roadmap will be delivered in parts so that individual topics and subtopics receive adequate coverage.

# Part 1 — Programming, mathematics, data and machine learning foundations

## Phase 1. Programming foundations

### 1.1 Python fundamentals

- Variables and data types
  - Integers, floats, strings, booleans
  - Type conversion and type checking
  - Mutable vs. immutable objects
- Operators
  - Arithmetic, comparison, logical and bitwise operators
  - Identity and membership operators
- Control flow
  - `if`, `elif`, `else`
  - `for` and `while` loops
  - `break`, `continue`, `pass`
  - List and dictionary comprehensions
- Data structures
  - Lists, tuples, sets and dictionaries
  - Stacks, queues and heaps
  - Nested data structures
- Functions
  - Parameters and return values
  - Positional and keyword arguments
  - Default arguments and variable-length arguments
  - Lambda functions
  - Scope, closures and recursion
- Object-oriented programming
  - Classes and objects
  - Constructors and instance attributes
  - Inheritance, polymorphism and encapsulation
  - Abstract classes and composition
- Error handling
  - Exceptions and custom exceptions
  - `try`, `except`, `else`, `finally`
  - Assertions and debugging
- Python modules and packages
  - Imports and package structure
  - Virtual environments
  - Dependency management
  - `pip`, `venv`, `uv` or equivalent tools
- File handling
  - Text, JSON, CSV and binary files
  - Reading and writing files
  - Context managers
  - Paths and directory operations
- Advanced Python
  - Iterators and generators
  - Decorators
  - Context managers
  - Type hints and generics
  - Dataclasses
  - `async` / `await`
  - Multiprocessing, multithreading and concurrency
  - Memory management and profiling

### 1.2 Python libraries for AI

- NumPy
  - Arrays, dimensions, shapes and dtypes
  - Indexing, slicing and broadcasting
  - Vectorization
  - Matrix operations
  - Random number generation
- Pandas
  - Series and DataFrames
  - Filtering, grouping and aggregation
  - Missing values and duplicates
  - Merging and joining
  - Data transformations
- Matplotlib and Seaborn
  - Line, bar and scatter plots
  - Histograms and distributions
  - Correlation heatmaps
  - Training curves and metric visualization
- Jupyter notebooks
  - Cells, kernels and environments
  - Experimentation and visualization
  - Reproducibility and notebook organization
- Basic SciPy
  - Statistical distributions
  - Optimization
  - Distance functions
  - Scientific computation

### 1.3 Software engineering

- Git and GitHub
  - Commits, branches, merges and pull requests
  - `.gitignore`
  - Branching strategies
  - Resolving merge conflicts
- Linux and command line
  - Files, directories and permissions
  - Processes and environment variables
  - Shell scripting basics
  - Package installation
- Software design
  - Modular code
  - Separation of concerns
  - SOLID principles
  - Design patterns
  - Logging and configuration
- Testing
  - Unit, integration and end-to-end tests
  - Mocking and fixtures
  - Test coverage
  - Regression testing
- APIs and networking
  - HTTP methods and status codes
  - REST APIs
  - JSON serialization
  - Authentication and API keys
  - Rate limits, retries and timeouts
  - Streaming responses and Server-Sent Events
- Databases
  - SQL fundamentals
  - Tables, joins, indexes and transactions
  - PostgreSQL or another relational database
  - NoSQL concepts
  - Redis and caching fundamentals

Phase 1 outcome: You should be able to write clean Python programs, manipulate datasets, call APIs, work with Git, and build a small backend service.

Suggested practice project: Create a Python application that loads a dataset, analyzes it with Pandas, stores results in a database, and exposes them through a REST API.

## Phase 2. Mathematics for AI and deep learning

You do not need to become a mathematician before building GenAI applications. However, a solid understanding of the following topics will help you understand how models learn and why they behave as they do.

### 2.1 Linear algebra

- Scalars, vectors, matrices and tensors
- Vector dimensions and matrix shapes
- Vector addition and scalar multiplication
- Dot products and matrix multiplication
- Transpose, inverse and identity matrices
- Norms and distances
  - L1 norm
  - L2 norm
  - Cosine similarity
- Linear independence and basis vectors
- Rank and matrix decompositions
- Eigenvalues and eigenvectors
- Singular value decomposition (SVD)
- Orthogonality and projections
- Tensor operations and broadcasting

GenAI applications: Embeddings, attention, neural network layers, dimensionality reduction and low-rank adaptation methods such as LoRA.

### 2.2 Calculus

- Functions, limits and continuity
- Derivatives and rates of change
- Partial derivatives
- Chain rule
- Gradients and directional derivatives
- Jacobian and Hessian matrices
- Multivariable calculus
- Computational graphs
- Automatic differentiation
- Gradient-based optimization
- Integration basics
- Vector calculus fundamentals

GenAI applications: Backpropagation, gradient descent, neural network training and optimization.

### 2.3 Probability

- Sample spaces and events
- Conditional probability
- Independence
- Bayes' theorem
- Random variables
- Discrete and continuous distributions
- Probability mass and density functions
- Joint, marginal and conditional distributions
- Expectation and variance
- Covariance and correlation
- Bernoulli and binomial distributions
- Gaussian and uniform distributions
- Categorical distributions
- Entropy and cross-entropy
- KL divergence
- Maximum likelihood estimation

GenAI applications: Next-token prediction, sampling, uncertainty, probabilistic modeling and generative distributions.

### 2.4 Statistics

- Population vs. sample
- Descriptive statistics
- Mean, median, mode and variance
- Quantiles and outliers
- Sampling methods
- Law of large numbers
- Central limit theorem
- Estimation and confidence intervals
- Hypothesis testing
- Statistical significance and effect size
- Correlation vs. causation
- Regression analysis
- Bias and variance
- Experimental design
- A/B testing
- Bootstrap and resampling

GenAI applications: Comparing models, interpreting benchmark results, analyzing experiments and measuring production quality.

### 2.5 Optimization

- Objective and loss functions
- Convex vs. non-convex optimization
- Gradient descent
- Stochastic gradient descent (SGD)
- Mini-batch gradient descent
- Momentum
- RMSProp
- Adam and AdamW
- Learning rates and schedules
- Weight decay
- Gradient clipping
- Local minima, saddle points and plateaus
- Convergence and numerical stability

### 2.6 Information theory

- Information content
- Entropy
- Conditional entropy
- Cross-entropy
- KL divergence
- Mutual information
- Perplexity
- Rate-distortion concepts

Phase 2 outcome: You should be able to understand the math behind embeddings, loss functions, gradient descent, token prediction and common model evaluation metrics.

## Phase 3. Data engineering and data preparation for AI

Models are only as useful as the data and evaluation process supporting them.

### 3.1 Data acquisition

- CSV, JSON, XML, Parquet and databases
- APIs and web data collection
- Public datasets
- Document collections and knowledge bases
- Structured vs. unstructured data
- Data licensing and provenance
- Personally identifiable information (PII)
- Data consent and usage restrictions

### 3.2 Data cleaning

- Missing values
- Duplicate records
- Invalid formats
- Outlier detection
- Inconsistent labels
- Encoding and normalization
- Data validation
- Schema enforcement
- Error handling and quality checks

### 3.3 Exploratory data analysis

- Descriptive statistics
- Distribution analysis
- Correlation analysis
- Class imbalance
- Data leakage detection
- Visual exploration
- Dataset documentation
- Data quality reports

### 3.4 Feature engineering and preprocessing

- Numerical feature scaling
- Standardization and normalization
- Categorical encoding
- Text cleaning and normalization
- Tokenization basics
- Stop-word handling where appropriate
- Stemming and lemmatization
- Image resizing and augmentation
- Audio resampling and feature extraction
- Feature selection and dimensionality reduction

### 3.5 Dataset preparation

- Training, validation and test splits
- Random vs. time-based splitting
- Stratified sampling
- Cross-validation
- Avoiding data leakage
- Labeling and annotation
- Inter-annotator agreement
- Synthetic data generation
- Data augmentation
- Dataset versioning and reproducibility

### 3.6 Data pipelines

- Batch and streaming pipelines
- ETL and ELT
- Data orchestration
- Data validation tests
- Versioned datasets
- Data lineage
- Storage and retrieval
- Data governance

Phase 3 outcome: Build a repeatable data pipeline that transforms raw data into validated datasets suitable for training and evaluation.

## Phase 4. Machine learning fundamentals

Learn traditional machine learning before moving deeply into neural networks. It teaches you how models learn patterns, generalize, and fail.

### 4.1 Introduction to machine learning

- What is machine learning?
- AI vs. machine learning vs. deep learning vs. GenAI
- Supervised learning
- Unsupervised learning
- Semi-supervised learning
- Self-supervised learning
- Reinforcement learning
- Batch learning vs. online learning
- Parametric vs. non-parametric models
- Model parameters vs. hyperparameters
- Training, inference and generalization

### 4.2 Supervised learning algorithms

- Linear regression
- Multiple linear regression
- Polynomial regression
- Ridge regression
- Lasso regression
- Elastic Net
- Logistic regression
- K-nearest neighbors (KNN)
- Naive Bayes
- Decision trees
- Random forests
- Gradient boosting
- XGBoost, LightGBM and CatBoost
- Support vector machines (SVM)
- Classification vs. regression

### 4.3 Unsupervised learning

- K-means clustering
- Hierarchical clustering
- DBSCAN
- Gaussian mixture models
- Principal component analysis (PCA)
- t-SNE and UMAP
- Anomaly detection
- Association rules
- Clustering evaluation

### 4.4 Model training and evaluation

- Loss functions
  - Mean squared error
  - Mean absolute error
  - Binary cross-entropy
  - Categorical cross-entropy
  - Hinge loss
- Classification metrics
  - Accuracy
  - Precision
  - Recall
  - F1-score
  - ROC-AUC and PR-AUC
  - Confusion matrix
- Regression metrics
  - MAE, MSE and RMSE
  - $R^2$
- Overfitting and underfitting
- Bias-variance trade-off
- Regularization
- Cross-validation
- Hyperparameter tuning
- Grid search and random search
- Early stopping
- Data leakage
- Class imbalance
- Calibration and decision thresholds

### 4.5 Practical machine learning tools

- Scikit-learn
- Pipelines and transformers
- Preprocessing with `ColumnTransformer`
- Experiment tracking
- Model serialization
- Reproducible experiments
- Feature importance
- Model interpretation with SHAP and LIME

Project: Build a customer churn prediction or text classification system. Create a reproducible training pipeline and compare at least three algorithms.

## Phase 5. Deep learning and neural networks

Deep learning is the foundation for modern language models, image generators, speech models and other generative architectures.

### 5.1 Neural network fundamentals

- Artificial neurons
- Weights, biases and layers
- Input, hidden and output layers
- Forward propagation
- Activation functions
  - Sigmoid
  - Tanh
  - ReLU
  - Leaky ReLU
  - GELU
  - Softmax
- Loss functions
- Backpropagation
- Computational graphs
- Automatic differentiation
- Gradient descent
- Batch size and epochs
- Initialization strategies
- Vanishing and exploding gradients

### 5.2 Neural network training

- Learning rate
- Optimizers: SGD, Adam and AdamW
- Learning rate scheduling
- Weight decay
- Dropout
- Batch normalization
- Layer normalization
- Gradient clipping
- Mixed-precision training
- Gradient accumulation
- Checkpointing
- Early stopping
- Distributed training basics
- GPU and accelerator fundamentals

### 5.3 Deep learning frameworks

- PyTorch
  - Tensors and tensor operations
  - Autograd
  - `nn.Module`
  - Datasets and DataLoaders
  - Custom training loops
  - GPU training
  - Model saving and loading
  - Mixed precision
- TensorFlow and Keras
  - Tensors and layers
  - Model APIs
  - Training and callbacks
  - Model export
- Understanding when to use each framework

### 5.4 Major neural network architectures

- Feedforward neural networks (MLPs)
- Convolutional neural networks (CNNs)
- Recurrent neural networks (RNNs)
- Long short-term memory networks (LSTMs)
- Gated recurrent units (GRUs)
- Autoencoders
- Variational autoencoders (VAEs)
- Generative adversarial networks (GANs)
- Attention-based networks
- Transformers

### 5.5 Sequence modeling

- Sequential data
- Word and token representations
- Sequence-to-sequence learning
- Teacher forcing
- Encoder-decoder architectures
- Padding and masking
- Positional information
- Beam search
- Greedy decoding
- Sampling-based decoding

### 5.6 Generative modeling introduction

- Discriminative vs. generative models
- Modeling a probability distribution
- Latent variables and latent spaces
- Likelihood-based models
- Autoregressive generation
- Variational inference
- Adversarial training
- Denoising and score-based generation
- Generative model evaluation

Project: Implement a small neural network from scratch with NumPy, then train an equivalent model in PyTorch. Train a basic text classifier or image classifier.

# Part 2 — Generative AI, Transformers, LLMs and RAG

This is the transition from general AI knowledge to the core skills used in modern GenAI engineering.

## Phase 6. Generative AI fundamentals

### 6.1 Understanding Generative AI

- Definition and scope of GenAI
- Generative vs. discriminative AI
- Traditional AI vs. generative AI
- Foundation models
- Pretrained models
- General-purpose vs. domain-specific models
- Open-weight vs. closed-weight models
- Hosted APIs vs. self-hosted inference
- Training vs. inference
- Capabilities and limitations of generative models

### 6.2 Types of generative models

- Autoregressive models
- Transformer-based language models
- Variational autoencoders
- Generative adversarial networks
- Diffusion models
- Normalizing flows
- Energy-based models
- Flow matching
- Multimodal generative models

### 6.3 Common GenAI tasks

- Text generation
- Question answering
- Summarization
- Translation
- Rewriting and editing
- Information extraction
- Classification using LLMs
- Code generation
- Conversational AI
- Retrieval-grounded generation
- Image generation and editing
- Speech synthesis
- Audio understanding
- Video generation
- Structured output generation

### 6.4 Core limitations

- Hallucinations
- Stale or missing knowledge
- Context-window limitations
- Non-deterministic outputs
- Sensitivity to prompts
- Bias and harmful outputs
- Inconsistent reasoning
- Computational and monetary cost
- Privacy and security risks

## Phase 7. Natural language processing (NLP)

### 7.1 Text preprocessing

- Unicode and text encoding
- Sentence segmentation
- Word tokenization
- Subword tokenization
- Character tokenization
- Normalization
- Special tokens
- Padding and truncation
- Attention masks
- Vocabulary construction

### 7.2 Traditional NLP

- Bag of words
- N-grams
- TF-IDF
- Word2Vec
- GloVe
- FastText
- Named entity recognition
- Part-of-speech tagging
- Dependency parsing
- Semantic similarity
- Text classification
- Information extraction

### 7.3 Tokenization for LLMs

- Byte Pair Encoding (BPE)
- WordPiece
- SentencePiece
- Unigram tokenization
- Byte-level tokenization
- Vocabulary size
- Token IDs
- Special tokens and delimiters
- Token count and context limits
- Tokenization effects on multilingual text
- Token-level loss and perplexity

### 7.4 Embeddings

- One-hot representations
- Static word embeddings
- Contextual embeddings
- Sentence embeddings
- Document embeddings
- Dense vectors
- Sparse vectors
- Embedding dimensions
- Cosine similarity
- Dot-product similarity
- Euclidean distance
- Embedding normalization
- Embedding model selection
- Domain-specific embeddings
- Multilingual embeddings
- Embedding evaluation and drift

Tools to learn: Hugging Face Tokenizers, Sentence Transformers and embedding APIs.

## Phase 8. Transformers and attention mechanisms

This is one of the most important phases in the entire roadmap.

### 8.1 Transformer architecture

- Why recurrent architectures have limitations
- Attention as a sequence-modeling mechanism
- Encoder-only Transformers
- Decoder-only Transformers
- Encoder-decoder Transformers
- Transformer blocks
- Residual connections
- Layer normalization
- Feedforward network layers
- Attention masks
- Positional information

### 8.2 Attention mechanisms

- Query, key and value vectors
- Scaled dot-product attention
- Self-attention
- Cross-attention
- Causal attention
- Multi-head attention
- Attention masks
- Padding masks
- Attention score matrices
- Computational complexity of attention
- Memory requirements
- Attention implementation in PyTorch

The central attention operation is commonly expressed as:

$$
\operatorname{Attention}(Q,K,V)
=
\operatorname{softmax}
\left(\frac{QK^\top}{\sqrt{d_k}}\right)V
$$

Here, $Q$ represents queries, $K$ keys, $V$ values, and $d_k$ is the key-vector dimension.

### 8.3 Advanced Transformer techniques

- Sinusoidal positional encodings
- Learned positional embeddings
- Rotary positional embeddings (RoPE)
- Relative positional encodings
- ALiBi
- Grouped-query attention (GQA)
- Multi-query attention (MQA)
- Multi-head latent attention (MLA)
- FlashAttention
- Sliding-window attention
- Sparse attention
- Linear attention approaches
- Mixture of Experts (MoE)
- Expert routing and load balancing
- Pre-norm vs. post-norm architectures

### 8.4 Transformer implementation

- Build a self-attention layer
- Implement a causal mask
- Build a Transformer block
- Create a small decoder-only model
- Implement next-token prediction
- Train on a small text corpus
- Generate text autoregressively
- Measure training loss and perplexity
- Inspect attention patterns
- Profile memory and computation

Project: Build a miniature GPT-style language model using PyTorch. You do not need to reproduce a production-scale model; the goal is to understand the architecture end to end.

## Phase 9. Large language models (LLMs)

### 9.1 LLM architecture families

- Encoder-only models
- Decoder-only models
- Encoder-decoder models
- Dense models
- Mixture-of-Experts models
- Base models
- Instruction-tuned models
- Reasoning-oriented models
- Multilingual models
- Long-context models
- Code-focused models

### 9.2 LLM pretraining

- Training corpus preparation
- Data filtering and deduplication
- Data contamination
- Tokenization and token IDs
- Next-token prediction
- Causal language modeling
- Cross-entropy loss
- Teacher-forced training
- Batch construction
- Sequence packing
- Learning rate schedules
- Warm-up and decay
- Checkpointing
- Distributed training
- Compute and memory requirements
- Training instability
- Scaling laws and compute allocation

### 9.3 LLM post-training

- Supervised fine-tuning (SFT)
- Instruction tuning
- Chat templates
- Conversational datasets
- Preference datasets
- Human feedback
- AI-generated preference feedback
- Reward modeling
- Reinforcement learning from human feedback (RLHF)
- Direct Preference Optimization (DPO)
- Proximal Policy Optimization (PPO)
- Group Relative Policy Optimization (GRPO)
- Rejection sampling
- Distillation
- Alignment and behavioral tuning

Note: These methods are related but not interchangeable. The appropriate approach depends on the training objective, model, data and available compute.

### 9.4 LLM inference

- Prompt construction
- Tokenization and decoding
- Prefill and decode stages
- Autoregressive generation
- Greedy decoding
- Beam search
- Temperature
- Top-k sampling
- Top-p (nucleus) sampling
- Repetition penalties
- Stop sequences
- Maximum output tokens
- KV cache
- Continuous batching
- Speculative decoding
- Quantized inference
- Time to first token (TTFT)
- Inter-token latency
- Throughput and concurrency

### 9.5 LLM evaluation

- Perplexity
- Exact match
- Accuracy and F1
- BLEU and ROUGE
- Semantic similarity
- Benchmark-based evaluation
- Human evaluation
- Pairwise preference evaluation
- LLM-as-a-judge
- Calibration
- Factuality
- Instruction following
- Tool-use accuracy
- Reasoning evaluation
- Robustness testing
- Contamination and benchmark leakage

### 9.6 Working with pretrained models

- Hugging Face Transformers
- Hugging Face Hub
- Model cards and configuration files
- Tokenizers and chat templates
- Loading pretrained models
- Running inference pipelines
- Text generation
- Embedding extraction
- Quantized model loading
- GPU and CPU inference
- Model licenses and usage restrictions

Project: Compare several pretrained models on the same question-answering and summarization tasks. Evaluate quality, latency, token usage and cost.

## Phase 10. Prompt engineering and structured outputs

### 10.1 Prompt engineering fundamentals

- System, developer and user instructions
- Role and task specification
- Context provision
- Instruction hierarchy
- Constraints and output requirements
- Delimiters and structured prompt sections
- Positive and negative instructions
- Prompt clarity and ambiguity reduction
- Few-shot examples
- Zero-shot prompting
- One-shot prompting
- Few-shot prompting
- Example selection and ordering

### 10.2 Advanced prompting techniques

- Chain-of-thought prompting concepts
- Self-consistency
- Least-to-most prompting
- Decomposition prompting
- ReAct-style prompting
- Plan-and-execute patterns
- Reflection and critique loops
- Retrieval-grounded prompting
- Contextual prompting
- Prompt chaining
- Prompt templates
- Dynamic prompt construction
- Prompt compression
- Prompt versioning and testing

These techniques are not universally beneficial. Evaluate them against a baseline, especially for reasoning tasks.

### 10.3 Structured generation

- JSON outputs
- JSON Schema
- Structured Outputs APIs
- Function and tool schemas
- Pydantic models
- Output validation
- Parsing and serialization
- Constrained decoding
- Enum and field constraints
- Schema evolution
- Error recovery
- Handling malformed responses

### 10.4 Prompt injection and robustness

- Direct prompt injection
- Indirect prompt injection
- Untrusted input boundaries
- Instruction conflicts
- Data exfiltration risks
- Prompt leakage
- Jailbreak testing
- Adversarial inputs
- Input and output validation
- Refusal handling
- Prompt security testing

Project: Build an information-extraction application that converts unstructured text into validated JSON and measures extraction accuracy.

## Phase 11. LLM APIs and application development

### 11.1 Model providers and interfaces

- Hosted model APIs
- Open-weight model serving
- Chat completion interfaces
- Responses-style interfaces
- Text generation endpoints
- Embedding endpoints
- Image and audio endpoints
- Streaming APIs
- Authentication and secrets management
- Model selection and fallback strategies

### 11.2 API engineering

- HTTP requests and responses
- SDK usage
- Timeouts and retries
- Exponential backoff
- Rate limits
- Token limits
- Concurrent requests
- Async inference
- Streaming token output
- Error handling
- Idempotency
- Request tracing
- Usage and cost tracking

### 11.3 Application architecture

- Python backend with FastAPI
- REST endpoints
- Request validation
- Authentication and authorization
- Frontend integration
- Session management
- Conversation persistence
- Database integration
- Background jobs
- Caching
- File uploads
- Streaming user interfaces
- Graceful failure and recovery

### 11.4 Model abstraction and routing

- Provider-independent interfaces
- Model registries
- Model routing
- Task-based model selection
- Cost-based routing
- Latency-based routing
- Fallback models
- Open-weight vs. hosted model trade-offs
- Provider migration strategies

Project: Build a chat application with streaming responses, conversation history, authentication, rate limits and usage tracking.

## Phase 12. Retrieval-Augmented Generation (RAG)

RAG is a major GenAI engineering skill. It combines a language model with external information so that responses can be grounded in retrieved documents.

### 12.1 RAG fundamentals

- Why RAG is needed
- LLM knowledge limitations
- RAG vs. fine-tuning
- RAG vs. long-context prompting
- Basic RAG architecture
- Retrieval, augmentation and generation
- Grounded answers
- Citations and source attribution
- Knowledge freshness
- RAG failure modes

### 12.2 Document ingestion

- PDF processing
- Word documents
- HTML and web pages
- Markdown and text
- CSV and spreadsheets
- Email and knowledge bases
- OCR for scanned documents
- Layout-aware parsing
- Tables and figures
- Metadata extraction
- Document identifiers
- Version tracking
- Access-control metadata

### 12.3 Text chunking

- Fixed-size chunking
- Token-based chunking
- Sentence-based chunking
- Paragraph-based chunking
- Recursive character splitting
- Semantic chunking
- Overlapping chunks
- Parent-child chunking
- Hierarchical chunking
- Document structure-aware chunking
- Chunk size and overlap tuning
- Chunk quality evaluation

### 12.4 Embedding generation

- Embedding model selection
- Document embeddings
- Query embeddings
- Embedding normalization
- Vector dimensions
- Batch embedding
- API and local embedding models
- Multilingual embeddings
- Embedding model versioning
- Re-embedding strategies

### 12.5 Vector databases

- Vector indexes
- Similarity search
- Approximate nearest neighbors
- HNSW
- IVF indexes
- Product quantization
- Metadata filtering
- Namespace and collection design
- Upserts and deletions
- Persistence
- Index tuning
- Multi-tenant isolation

Technologies to explore include FAISS, pgvector, Qdrant, Milvus, Weaviate and Pinecone. Select one or two to learn deeply before exploring the rest.

### 12.6 Retrieval strategies

- Dense vector retrieval
- Sparse retrieval
- BM25
- Keyword search
- Hybrid retrieval
- Metadata filtering
- Query rewriting
- Query expansion
- Multi-query retrieval
- Hypothetical Document Embeddings (HyDE)
- Maximum Marginal Relevance (MMR)
- Parent-document retrieval
- Multi-hop retrieval
- Temporal and metadata-aware retrieval

### 12.7 Reranking

- Cross-encoder rerankers
- Bi-encoder retrieval
- Retrieve-then-rerank
- Candidate generation
- Relevance scoring
- Top-k selection
- Diversity and redundancy reduction
- Latency-quality trade-offs

### 12.8 Generation and grounding

- Context assembly
- Context ordering
- Prompt construction
- Source citations
- Evidence-based responses
- Abstention when evidence is insufficient
- Conflicting document handling
- Context-window budgeting
- Source freshness
- Permission-aware retrieval

### 12.9 Advanced RAG

- Corrective RAG
- Self-reflective RAG
- Adaptive RAG
- Agentic RAG
- Graph RAG
- Knowledge graph retrieval
- Hierarchical retrieval
- Multi-modal RAG
- Table-aware RAG
- Long-document retrieval
- Temporal RAG
- Multi-tenant enterprise RAG

### 12.10 RAG evaluation

- Retrieval precision and recall
- Hit rate
- Mean Reciprocal Rank (MRR)
- Normalized Discounted Cumulative Gain (NDCG)
- Context relevance
- Context recall
- Faithfulness
- Answer relevance
- Citation correctness
- Answer completeness
- End-to-end latency
- Cost per query
- Retrieval ablation testing

Project: Build a document question-answering system with PDF ingestion, hybrid retrieval, reranking, citations and an evaluation dataset.

## Phase 13. AI agents and tool use

### 13.1 Agent fundamentals

- LLM applications vs. agents
- Tools and actions
- Agent state
- Goals and constraints
- Planning and execution
- Observation and feedback
- Agent loops
- Stopping conditions
- Deterministic workflows vs. autonomous agents
- Human-in-the-loop systems

### 13.2 Tool calling

- Function calling
- Tool schemas
- Tool selection
- Argument generation
- Input validation
- Tool execution
- Tool result messages
- Multi-step tool calls
- Parallel tool execution
- Tool error handling
- Tool permissions
- Sandboxed execution

### 13.3 Agent reasoning and planning

- ReAct patterns
- Plan-and-execute
- Task decomposition
- Subgoal generation
- State transitions
- Reflection
- Self-correction
- Retry policies
- Workflow graphs
- Conditional routing
- Checkpointing
- Termination and loop prevention

### 13.4 Agent memory

- Short-term conversation state
- Long-term memory
- Episodic memory
- Semantic memory
- Working memory
- User preferences
- Memory retrieval
- Memory summarization
- Memory updates and deletion
- Privacy-aware memory
- Avoiding stale or contradictory memory

### 13.5 Multi-agent systems

- Supervisor-worker architecture
- Planner-executor architecture
- Specialized agents
- Agent delegation
- Message passing
- Shared state
- Agent coordination
- Consensus and conflict resolution
- Parallel agent execution
- Agent communication protocols
- Multi-agent evaluation
- Cost and reliability management

### 13.6 Agent frameworks and protocols

- Direct tool calling without a framework
- LangGraph
- LangChain
- LlamaIndex workflows
- Semantic Kernel
- AutoGen-style multi-agent systems
- Model Context Protocol (MCP)
- MCP clients and servers
- Tools, resources and prompts in MCP
- Authentication and authorization
- Protocol security and trust boundaries

### 13.7 Production agents

- Approval gates for sensitive actions
- Human review
- Idempotent operations
- Transaction safety
- Tool access control
- Audit logs
- Rate limits
- Budget limits
- Maximum iteration counts
- Recovery and resume
- Agent traces
- Deterministic test environments

Project: Create an agent that searches an approved knowledge base, calls external tools, produces a structured report and requests human approval before performing sensitive actions.

## Phase 14. Fine-tuning and customization

### 14.1 When to fine-tune

- Prompting vs. RAG vs. fine-tuning
- Domain adaptation
- Instruction following
- Style and format consistency
- Task-specific behavior
- Data availability
- Training and inference costs
- Model licensing constraints
- Fine-tuning success criteria

### 14.2 Fine-tuning data

- Instruction-response pairs
- Chat conversation formats
- System and user messages
- Input-output examples
- Dataset filtering
- Data deduplication
- Quality scoring
- Train-validation splits
- Synthetic training data
- Data contamination
- Dataset balance
- Data privacy

### 14.3 Supervised fine-tuning

- Full-parameter fine-tuning
- Training objectives
- Loss masking
- Sequence packing
- Learning rate selection
- Batch size and gradient accumulation
- Training schedules
- Checkpoint selection
- Validation loss
- Catastrophic forgetting
- Overfitting detection

### 14.4 Parameter-efficient fine-tuning

- Adapter methods
- Low-Rank Adaptation (LoRA)
- Quantized LoRA (QLoRA)
- Rank and alpha parameters
- Target module selection
- Adapter training
- Adapter merging
- Multiple adapters
- Memory and compute trade-offs

### 14.5 Preference optimization

- Preference pairs
- Reward models
- RLHF
- DPO
- PPO
- GRPO
- Rejection sampling
- Preference-data quality
- Reward hacking
- Alignment evaluation

### 14.6 Distillation and compression

- Teacher-student learning
- Logit distillation
- Response distillation
- Synthetic data distillation
- Model pruning
- Quantization
- Weight-only quantization
- Activation quantization
- Quantization-aware training
- Quality and speed trade-offs

### 14.7 Training tools

- Hugging Face Transformers
- TRL
- PEFT
- Accelerate
- DeepSpeed
- FSDP
- Experiment tracking
- Training checkpoints
- GPU memory profiling

Project: Fine-tune a small open-weight model with LoRA on a high-quality task-specific dataset. Compare it with the original model on a held-out evaluation set.

## Phase 15. Multimodal AI and generative media

### 15.1 Vision-language models

- Image encoders
- Vision Transformers
- Image patch embeddings
- Vision-language alignment
- Contrastive learning
- Image-text embeddings
- Image question answering
- Visual reasoning
- OCR and document understanding
- Object recognition
- Image captioning
- Video understanding

### 15.2 Image generation

- Diffusion model fundamentals
- Forward noise process
- Reverse denoising process
- Denoising objectives
- Latent diffusion
- Text encoders
- Conditioning
- Classifier-free guidance
- Sampling schedulers
- Image-to-image generation
- Inpainting and outpainting
- ControlNet-style conditioning
- Personalization and fine-tuning
- Image evaluation

### 15.3 Audio and speech

- Digital audio basics
- Sampling rates
- Waveforms and spectrograms
- Audio tokenization
- Speech recognition (ASR)
- Text-to-speech (TTS)
- Speech-to-speech systems
- Speaker diarization
- Voice activity detection
- Audio captioning
- Music generation
- Audio-language models
- Streaming speech interfaces
- Speech latency and turn-taking

### 15.4 Video generation and understanding

- Video frame sampling
- Temporal representations
- Video-language models
- Text-to-video generation
- Image-to-video generation
- Temporal consistency
- Motion conditioning
- Video summarization
- Video retrieval
- Audio-video synchronization
- Evaluation of generated video

### 15.5 Multimodal RAG and agents

- Image and document retrieval
- Video retrieval
- Audio search
- Cross-modal embeddings
- Multimodal document chunking
- Visual tool use
- Real-time multimodal agents
- Combining vision, audio and text
- Modality-specific evaluation

Project: Build a multimodal assistant that accepts documents and images, answers questions with evidence, and supports speech input or output.

## Phase 16. Evaluation, safety and responsible AI

### 16.1 Evaluation methodology

- Define task-specific success metrics
- Create representative test sets
- Golden datasets
- Offline evaluation
- Online evaluation
- Human preference studies
- Pairwise comparisons
- Regression tests
- Model and prompt comparisons
- Statistical significance
- Evaluation reproducibility

### 16.2 LLM evaluation

- Instruction-following accuracy
- Factuality
- Faithfulness
- Hallucination rates
- Reasoning benchmarks
- Code generation tests
- Tool-use success
- Context adherence
- Citation verification
- Structured-output validity
- Refusal accuracy
- Robustness under paraphrasing

### 16.3 RAG and agent evaluation

- Retrieval recall
- Retrieval precision
- Evidence quality
- Answer correctness
- Tool-selection accuracy
- Tool-argument correctness
- Task completion rate
- Recovery from tool failures
- Multi-step execution accuracy
- Human intervention rate
- Cost per completed task

### 16.4 Safety and security

- Prompt injection
- Jailbreak resistance
- Sensitive-data leakage
- Personally identifiable information
- Training-data privacy
- Model access controls
- Tool permission boundaries
- Malicious document handling
- Unsafe tool execution
- Output validation
- Adversarial testing
- Abuse monitoring

### 16.5 Responsible AI and governance

- Bias and fairness
- Explainability and transparency
- Data provenance
- Copyright and licensing
- Privacy requirements
- Human oversight
- Auditability
- Model documentation
- Risk assessment
- Regulatory compliance
- Content provenance
- Incident response

## Phase 17. Production deployment and LLMOps

### 17.1 Backend and serving

- FastAPI
- Async request handling
- Streaming responses
- Background tasks
- Request validation
- Authentication
- Authorization
- Database connections
- Caching
- API gateways
- Load balancing

### 17.2 Deployment infrastructure

- Docker
- Container registries
- Kubernetes fundamentals
- Cloud deployment
- GPU instances
- Secrets management
- CI/CD pipelines
- Infrastructure as code
- Autoscaling
- Blue-green and canary deployments
- Rollbacks
- Disaster recovery

### 17.3 Model serving

- Hosted inference APIs
- vLLM
- Hugging Face TGI
- llama.cpp
- ONNX Runtime
- TensorRT-LLM
- Batching
- Continuous batching
- KV cache optimization
- Quantized inference
- GPU utilization
- Model parallelism
- Distributed inference

### 17.4 Monitoring and observability

- Request and response traces
- Latency monitoring
- Token usage
- Cost tracking
- Error rates
- Time to first token
- Throughput
- Model quality monitoring
- Retrieval quality monitoring
- Data drift
- Model drift
- Prompt and model versioning
- Alerts and incident handling

### 17.5 Performance and cost optimization

- Model selection
- Prompt shortening
- Context reduction
- Response caching
- Semantic caching
- Batch inference
- Quantization
- Smaller-model routing
- Output-token limits
- Retrieval optimization
- Concurrency control
- Cost per request
- Quality-cost trade-offs

### 17.6 LLMOps and MLOps

- Experiment tracking
- Model registries
- Dataset versioning
- Evaluation pipelines
- Automated regression tests
- Deployment gates
- Prompt registries
- Model version management
- Rollback procedures
- Production feedback loops

Project: Deploy a RAG application with authentication, Docker, automated tests, tracing, evaluation, monitoring and cost tracking.

## Phase 18. Advanced GenAI and research topics

These topics are useful for specialization, advanced engineering roles or research-oriented work.

### 18.1 Advanced LLM architecture

- Sparse and conditional computation
- Mixture of Experts
- Long-context architectures
- Advanced attention mechanisms
- Recurrent and hybrid architectures
- State-space models
- Memory-augmented models
- Retrieval-enhanced language models
- Multimodal foundation models
- Architecture scaling trade-offs

### 18.2 Advanced reasoning

- Reasoning-oriented model training
- Process supervision
- Outcome supervision
- Search-based reasoning
- Tree search
- Self-consistency
- Verifier models
- Reward models
- Test-time compute
- Tool-augmented reasoning
- Limits of benchmark-based reasoning evaluation

### 18.3 Advanced training systems

- Distributed data parallelism
- Tensor parallelism
- Pipeline parallelism
- Expert parallelism
- Sequence parallelism
- FSDP and ZeRO
- Memory optimization
- Checkpoint sharding
- Fault-tolerant training
- Large-scale data pipelines
- Training throughput profiling

### 18.4 Advanced retrieval and knowledge systems

- Knowledge graph construction
- Graph-based retrieval
- Entity linking
- Graph traversal
- Hybrid graph-vector retrieval
- Temporal knowledge
- Multi-hop question answering
- Structured database querying
- Text-to-SQL
- Enterprise permissions and data governance

### 18.5 Research skills

- Reading research papers
- Reproducing baselines
- Identifying assumptions
- Designing controlled experiments
- Ablation studies
- Benchmark selection
- Statistical uncertainty
- Research code organization
- Reproducibility
- Writing technical reports
- Tracking emerging architectures and methods

### 18.6 Specialized application domains

- AI coding assistants
- Enterprise knowledge assistants
- Customer support automation
- Finance and document intelligence
- Healthcare information systems
- Legal document analysis
- Education and tutoring
- Scientific discovery
- Robotics and embodied AI
- Synthetic data generation
- Creative tools

Domain-specific deployments require additional validation, privacy safeguards and expert oversight where appropriate.

# Phase 19. Projects to complete the roadmap

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

## Phase 20. Recommended learning resources

Use official documentation and practical exercises as your primary sources.

- Python: Python — [Official tutorial](<https://docs.python.org/3/tutorial/?utm_source=chatgpt.com>)
- Machine learning: scikit-learn — [User guide](<https://scikit-learn.org/stable/user_guide.html?utm_source=chatgpt.com>)
- Deep learning: PyTorch — [Official tutorials](<https://pytorch.org/tutorials/?utm_source=chatgpt.com>)
- Transformers and LLMs: Hugging Face — [Learning courses](<https://huggingface.co/learn?utm_source=chatgpt.com>)
- LLM application development: LangChain — [Documentation](<https://docs.langchain.com/?utm_source=chatgpt.com>)
- Retrieval and indexing: LlamaIndex — [Documentation](<https://docs.llamaindex.ai/?utm_source=chatgpt.com>)
- Agent protocols: Model Context Protocol — [Official documentation](<https://modelcontextprotocol.io/?utm_source=chatgpt.com>)
- Model training and fine-tuning: Hugging Face TRL — [Documentation](<https://huggingface.co/docs/trl/index?utm_source=chatgpt.com>)
- Production inference: vLLM — [Documentation](<https://docs.vllm.ai/?utm_source=chatgpt.com>)

## Phase 21. Suggested study timeline

A realistic timeline depends on your existing knowledge and how much time you can spend building projects.

| Learning stage | Estimated time |
| --- | --- |
| Python and software foundations | 2–4 weeks |
| Mathematics and data foundations | 3–6 weeks |
| Machine learning and deep learning | 4–8 weeks |
| Transformers and LLM fundamentals | 3–5 weeks |
| Prompting, APIs and structured outputs | 1–3 weeks |
| RAG and retrieval systems | 3–5 weeks |
| Agents and tool use | 2–4 weeks |
| Fine-tuning and multimodal AI | 4–8 weeks |
| Deployment, evaluation and LLMOps | 3–6 weeks |
| Advanced topics and portfolio projects | Ongoing |

These estimates overlap when topics are learned together. A focused learner with prior programming experience might develop practical GenAI engineering skills in several months; mastering model training, multimodal systems and advanced research takes substantially longer.

## Final checklist

## Track your progress

### 0/20

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

Reset checklist

My recommendation: For a GenAI engineer role, prioritize Python, PyTorch fundamentals, Transformers, LLM APIs, RAG, tool calling, evaluation, and deployment. Learn fine-tuning and multimodal models next. Go deep into distributed training and research-level mathematics if your goal is to become an LLM researcher or model-training engineer.

This roadmap covers the major foundations and specialization areas, but no single curriculum can include every evolving model, framework, research paper and implementation detail. Learn the underlying concepts first; tools and specific model architectures will continue to change.
