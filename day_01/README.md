# Day 01: Introduction to AI Agents

This folder contains the materials for **Day 1** of the Kaggle 5-Day AI Agents Course, focusing on building AI agents using Google's Agent Development Kit (ADK).

---

## 📑 Table of Contents

### 📝 Part I: Theoretical Foundations (Whitepaper Notes)
- [🚀 The Big Paradigm Shift](#-the-big-paradigm-shift)
- [🎯 What is an AI Agent?](#-what-is-an-ai-agent)
- [🔄 How an Agent "Thinks": The 5-Step Process](#-how-an-agent-thinks-the-5-step-process)
- [📊 Taxonomy of Agentic Systems (5 Levels)](#-taxonomy-of-agentic-systems-5-levels)
  - [Level 0: Core Reasoning System](#level-0-core-reasoning-system-)
  - [Level 1: Connected Problem-Solver](#level-1-connected-problem-solver-)
  - [Level 2: Strategic Problem-Solver](#level-2-strategic-problem-solver-)
  - [Level 3: Collaborative Multi-Agent System](#level-3-collaborative-multi-agent-system-)
  - [Level 4: Self-Evolving System](#level-4-self-evolving-system-)
- [🏗️ Core Architecture Deep Dive](#️-core-architecture-deep-dive)
  - [🧠 The "Brain" (Model Selection)](#-the-brain-model-selection)
  - [✋ The "Hands" (Tools)](#-the-hands-tools)
  - [⚡ The "Nervous System" (Orchestration Engine)](#-the-nervous-system-orchestration-engine)
  - [🚀 The "Body" (Deployment)](#-the-body-deployment)
- [🏭 Agent Ops: Building for Production](#-agent-ops-building-for-production)
- [🔒 Security & Governance](#-security--governance)
- [🔮 The Future: How Agents Learn & Evolve](#-the-future-how-agents-learn--evolve)
- [🤖 Multi-Agent Systems](#-multi-agent-systems)
- [🎯 Key Takeaways (TL;DR)](#-key-takeaways-tldr)

### 💻 Part II: Practical Implementation (Code Exercises)
- [📚 Course Contents](#-course-contents)
- [🎯 Learning Objectives](#-learning-objectives)
- [🚀 Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Setup Instructions](#setup-instructions)
  - [Installation (Local Development)](#installation-local-development)
- [📖 Core ADK Components](#-core-adk-components)
- [💻 ADK Web Interface](#-adk-web-interface)
- [⚠️ Important Notes](#️-important-notes)
- [📚 Additional Resources](#-additional-resources)
- [👤 Author](#-author)
- [🎯 Next Steps](#-next-steps)

---

## 📝 Part I: Theoretical Foundations (Whitepaper Notes)

> **Note**: Start here to understand the theory before diving into code exercises!

---

### 🚀 The Big Paradigm Shift

**From Predictive AI → Autonomous Agents**

| Predictive AI (Traditional) | Autonomous Agents (New) |
|----------------------------|------------------------|
| 🤔 Passive, discrete tasks | ⚡ Active, multi-step problem solving |
| 👨‍💻 Requires constant human direction | 🤖 Makes plans and takes actions autonomously |
| 💬 "Translate this text" | 🎯 "Plan my trip to the conference" |

**Key Insight**: An agent is a complete application that combines reasoning with the ability to act—not just a model!

---

### 🎯 What is an AI Agent?

An AI Agent is a system that uses a **Language Model (LM) in a loop with tools** to accomplish a goal.

**Simple Flow:**
- **LLM Response**: `Prompt → LLM → Text`
- **AI Agent**: `Prompt → Agent → Thought → Action → Observation → Final Answer`

**Four Essential Components** (Body Analogy):

1. **🧠 The Model (Brain)**
   - The LM that processes information and makes decisions
   - Handles reasoning and strategic thinking

2. **✋ Tools (Hands)**
   - APIs, functions, databases that let the agent **act**
   - Examples: Search, Calendar, Database queries
   - Connect reasoning to reality

3. **⚡ Orchestration (Nervous System)**
   - The code that runs the agent's loop
   - Manages planning, memory, and decision-making
   - Decides when to "think" vs. "use a tool"

4. **🚀 Deployment (Body)**
   - Secure, scalable server infrastructure
   - Logging, monitoring, reliability services
   - Makes the agent production-ready

---

### 🔄 How an Agent "Thinks": The 5-Step Process

Agents operate on a **"Think, Act, Observe"** cycle:

1. **1️⃣ Get the Mission**
   - Receives a high-level goal (e.g., "Where is my order?")

2. **2️⃣ Scan the Scene**
   - Gathers context: "What do I know? What tools can I use?"

3. **3️⃣ Think It Through**
   - The "brain" makes a plan (e.g., "1. Find order. 2. Track it.")

4. **4️⃣ Take Action**
   - The "hands" execute the plan (e.g., call `find_order("12345")`)

5. **5️⃣ Observe and Iterate**
   - Sees the result, then **loops back to Step 3** for the next action

This loop continues until the goal is achieved! 🔁

---

### 📊 Taxonomy of Agentic Systems (5 Levels)

Agents are classified into levels, each building on the capabilities of the last:

#### **Level 0: Core Reasoning System** 💭
- An LM in isolation—no tools, no memory, no live data
- Can **explain** but can't **do**
- **Example**: Can explain baseball rules ⚾ but can't tell you yesterday's score

#### **Level 1: Connected Problem-Solver** 🔌
- LM with "Hands" (Tools)
- Can interact with the world
- Uses the 5-step loop for **simple, single-step tasks**
- **Example**: Can use Search tool to find and tell you yesterday's score

#### **Level 2: Strategic Problem-Solver** 🎯
- Plans and executes **multi-step goals**
- Uses "context engineering" to chain tools together
- **Example**: "Find a coffee shop ☕ halfway between my office and my client's office" (Maps → Places tools)

#### **Level 3: Collaborative Multi-Agent System** 👥
- A "team of specialists"
- "Project Manager" agent delegates tasks to specialized sub-agents
- Handles complex business workflows
- **Example**: ResearchAgent + MarketingAgent + SalesAgent working together

#### **Level 4: Self-Evolving System** 🧬
- The most advanced and autonomous level
- Can **identify gaps in its own capabilities**
- Dynamically **creates new tools or agents** to fill those gaps
- **Example**: Project Manager agent realizes it needs social media tracking → creates a SentimentAnalysisAgent on the fly!
- 🤖 **True Autonomy** + 🔄 **Self-Improvement**

---

### 🏗️ Core Architecture Deep Dive

#### 🧠 The "Brain" (Model Selection)

Choosing the right model is critical:

✨ **Superior Reasoning**
- Must navigate multi-step problems effectively

🎯 **Reliable Tool Use**
- Must correctly call functions and APIs

💡 **Pro-Tip: Team of Specialists**
- 🦾 **Powerful Model** (Gemini Pro) for complex planning
- ⚡ **Fast Model** (Gemini Flash) for simple, high-volume tasks

#### ✋ The "Hands" (Tools)

**Two Main Categories:**

**1. Retrieving Information** 📥
- 📚 **RAG** (Retrieval-Augmented Generation): Document/vector database lookup
- 🔍 **Google Search**: Live web knowledge
- 🗃️ **NL2SQL**: Query structured databases

**2. Executing Actions** 📤
- 🔌 **APIs**: Send emails, schedule meetings, update CRM
- 💻 **Code Execution**: Write and run code (e.g., Python)
- 👤 **Human-in-the-Loop (HITL)**: Pause to ask human for confirmation

#### ⚡ The "Nervous System" (Orchestration Engine)

The state machine that governs behavior:

- 📋 **Manages Plans**: Keeps track of strategy
- 🧠 **Short-Term Memory**: Current conversation history
- 💾 **Long-Term Memory**: Past conversations, user preferences (accessed via tools)
- 🛡️ **Error Handling**: Recovers gracefully when tools fail

#### 🚀 The "Body" (Deployment)

The infrastructure that makes the agent production-ready and reliable:

**Core Infrastructure Components:**

**1. 🏢 Hosting & Runtime Environment**
- Secure, scalable server infrastructure
- Container orchestration (Docker, Kubernetes)
- Cloud platforms (Google Cloud, AWS, Azure)
- Auto-scaling for handling variable loads

**2. 📊 Observability & Monitoring**
- **Logging**: Capture all agent actions and decisions
- **Metrics**: Track performance, latency, token usage
- **Tracing**: Follow requests through the entire system (OpenTelemetry)
- **Alerting**: Get notified when things go wrong

**3. 🔒 Security & Compliance**
- API authentication and authorization
- Secrets management (API keys, credentials)
- Data encryption (at rest and in transit)
- Compliance with regulations (GDPR, HIPAA, etc.)

**4. ⚡ Performance & Reliability**
- Load balancing across multiple instances
- Caching strategies for faster responses
- Retry mechanisms and circuit breakers
- Graceful degradation when services fail

**5. 🔄 CI/CD Pipeline**
- Automated testing and validation
- Version control and rollback capabilities
- Staged deployments (dev → staging → production)
- A/B testing for model improvements

**💡 Pro-Tip: Start Simple, Scale Smart**
- Begin with a simple deployment (e.g., Cloud Run, Lambda)
- Add monitoring and logging from day one
- Scale infrastructure as usage grows
- Use managed services to reduce operational overhead

---

### 🏭 Agent Ops: Building for Production

⚠️ **The Problem**: Agents are **stochastic** (non-deterministic), so traditional pass/fail tests don't work!

**Solution: Agent Ops** 🚀

**1. 📊 Measure What Matters**
Track business KPIs:
- ✅ Goal Completion Rate
- 💰 Cost Per Interaction
- 😊 User Satisfaction Score

**2. ⚖️ Use an "LM as Judge"**
- Use a powerful model (like Gemini Pro) to automatically evaluate output quality against a rubric
- Automated quality assessment at scale

**3. 🔍 Debug with Traces**
- Use **OpenTelemetry** to get step-by-step recording of the agent's "thought process"
- See exactly what the agent did and why

---

### 🔒 Security & Governance

⚠️ **Warning**: Giving an agent power creates risk (rogue actions, data leaks)

**Cannot trust the model alone!** 🚫

**🛡️ Defense-in-Depth: Hybrid Approach**

**1. 🔧 Hardcoded Rules**
- Deterministic guardrails
- Example: "NEVER allow purchase over $100 without confirmation"

**2. 🤖 AI Guardrails**
- Use a second, faster "guard model" to screen:
  - 📥 **Inputs**: Detect prompt injections
  - 📤 **Outputs**: Filter harmful content

**🆔 Agent Identity: A New Security Concept**
- An agent must have its **own identity** (like a service account)
- Separate permissions from the user
- Principle of least privilege

---

### 🔮 The Future: How Agents Learn & Evolve

⏰ **The Challenge**: Agents deployed today will "age"—performance degrades as policies and data change

**They must be designed to learn!** 📚

**📖 Learning from Experience**
- 📋 Runtime artifacts (logs, traces)
- 👥 Human-in-the-Loop (HITL) feedback

**🔄 Adapting Capabilities**
The system can generalize feedback to:
- ✍️ Refine its prompts and instructions
- 🔧 Identify gaps and suggest new tools

**🏋️ Agent Gym: The Future**
- A frontier concept: An "offline" simulation environment
- "Train" agents and pressure-test them before deployment
- Optimize behavior safely without production risks

---

### 🤖 Multi-Agent Systems

Instead of one "do-it-all" agent, build a team of specialized agents that collaborate:

**Benefits:**
- ✅ Easier to build and maintain
- ✅ Simpler to debug (which agent failed?)
- ✅ More reliable and powerful when working together
- ✅ Clear separation of concerns

**Workflow Patterns Decision Guide:**

| Pattern | When to Use | Example |
|---------|-------------|---------|
| **LLM-based** | Dynamic orchestration needed | Research + Summarize |
| **Sequential** | Order matters, linear pipeline | Outline → Write → Edit |
| **Parallel** | Independent tasks, speed matters | Multi-topic research |
| **Loop** | Iterative improvement needed | Writer + Critic refinement |

---

### 🎯 Key Takeaways (TL;DR)

1. **🚀 Paradigm Shift**
   - Agents are active, autonomous problem-solving partners (not passive tools)

2. **🏗️ It's a System**
   - A successful agent is not just a prompt—it's an engineered system:
     - 🧠 Model (Brain)
     - ✋ Tools (Hands)
     - ⚡ Orchestration (Nervous System)

3. **🎓 New Challenges**
   - Building agents requires new disciplines:
     - 🏭 **Agent Ops** (Testing & Monitoring)
     - 🔒 **Agent Identity** (Security)
     - 👥 **Multi-Agent Systems** (Architecture)

---

## 💻 Part II: Practical Implementation (Code Exercises)

> **Now let's get hands-on!** This section covers the practical aspects of building agents with ADK.

---

## 📚 Course Contents

### Jupyter Notebooks (code/)

1. **day-1a-from-prompt-to-action.ipynb**
   - Your first AI agent implementation
   - Setting up the Agent Development Kit (ADK)
   - Configuring Gemini API authentication
   - Building a simple agent with Google Search tool
   - Introduction to ADK web interface

2. **day-1b-agent-architectures.ipynb**
   - Multi-agent systems and workflow patterns
   - LLM-based orchestration (dynamic agent coordination)
   - Sequential workflows (assembly line pattern)
   - Parallel workflows (concurrent execution)
   - Loop workflows (iterative refinement)
   - Choosing the right pattern for your use case

### Additional Resources

- **Day_01_Introduction_to_Agents.pdf** - Course presentation slides
- **agent_slides.html** - Interactive HTML version of slides
- **day_01_slides/** - Slide source files
- **artifacts/kaggle_agents_poster.png** - Visual reference poster

## 🎯 Learning Objectives

By completing Day 1, you will learn to:

- ✅ Install and configure the Agent Development Kit (ADK)
- ✅ Set up Gemini API authentication using Kaggle Secrets
- ✅ Build your first AI agent with tool-calling capabilities
- ✅ Understand the difference between LLMs and AI Agents
- ✅ Design multi-agent systems with specialized agents
- ✅ Implement four core workflow patterns:
  - **LLM-based orchestration** - Dynamic decision-making
  - **Sequential agents** - Fixed execution pipeline
  - **Parallel agents** - Concurrent task execution
  - **Loop agents** - Iterative refinement cycles
- ✅ Use ADK's web interface for debugging and testing

## 🚀 Getting Started

### Prerequisites

- Kaggle account (verified with phone number)
- Gemini API key from [Google AI Studio](https://aistudio.google.com/app/api-keys)
- Basic Python knowledge

### Setup Instructions

1. **Open a notebook** in Kaggle
2. **Copy and Edit** to create your own version
3. **Add API Key** to Kaggle Secrets:
   - Go to `Add-ons` → `Secrets`
   - Create secret labeled `GOOGLE_API_KEY`
   - Paste your API key and save
   - Enable the checkbox to attach the secret
4. **Run cells in order** (avoid "Run all" to prevent rate limiting)

### Installation (Local Development)

If running outside Kaggle:

```bash
pip install google-adk
```

## 📖 Core ADK Components

- **Agent** - The core agent class with model, instructions, and tools
- **Gemini** - Google's LLM model wrapper
- **InMemoryRunner** - Orchestrates agent execution and manages state
- **AgentTool** - Wraps agents as tools for other agents
- **FunctionTool** - Wraps Python functions as agent tools
- **google_search** - Built-in tool for web search

## 💻 ADK Web Interface

The course introduces ADK's built-in web UI for:
- Interactive chat with agents
- Testing and debugging
- Visualizing agent workflows
- Monitoring tool calls and responses

To create a sample agent structure:
```bash
adk create sample-agent --model gemini-2.5-flash-lite --api_key $GOOGLE_API_KEY
```


## 📚 Additional Resources

- [ADK Documentation](https://google.github.io/adk-docs/)
- [ADK Quickstart for Python](https://google.github.io/adk-docs/get-started/python/)
- [ADK Agents Overview](https://google.github.io/adk-docs/agents/)
- [ADK Tools Overview](https://google.github.io/adk-docs/tools/)
- [Gemini API Documentation](https://ai.google.dev/gemini-api/docs)

## 🎯 Next Steps

Continue to **Day 2** to learn about:
- Creating custom functions
- Using MCP (Model Context Protocol) tools
- Managing long-running operations
- Advanced agent capabilities

---

**License**: Apache License 2.0  
**Copyright**: 2025 Google LLC
