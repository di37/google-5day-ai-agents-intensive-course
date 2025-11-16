# Day 02: Agent Tools & Interoperability

This folder contains the materials for **Day 2** of the Kaggle 5-Day AI Agents Course, focusing on building powerful agent tools and integrating external services using the Model Context Protocol (MCP).

---

## 📑 Table of Contents

### 📝 Part I: Theoretical Foundations (Whitepaper Notes)
- [🔧 Introduction to Agent Tools](#-introduction-to-agent-tools)
- [🌐 Model Context Protocol (MCP)](#-model-context-protocol-mcp)
  - [What is MCP?](#what-is-mcp)
  - [Why MCP Matters](#why-mcp-matters)
  - [MCP Architecture](#mcp-architecture)
  - [MCP in the Agent Ecosystem](#mcp-in-the-agent-ecosystem)
- [🎯 Key Takeaways (TL;DR)](#-key-takeaways-tldr)

### 💻 Part II: Practical Implementation (Code Exercises)
- [📚 Course Contents](#-course-contents)
- [🎯 Learning Objectives](#-learning-objectives)
- [🚀 Getting Started](#-getting-started)
  - [Prerequisites](#prerequisites)
  - [Setup Instructions](#setup-instructions)
- [🔧 Core ADK Tool Types](#-core-adk-tool-types)
- [💡 Best Practices for Tool Development](#-best-practices-for-tool-development)
- [⚠️ Important Notes](#️-important-notes)
- [📚 Additional Resources](#-additional-resources)
- [🎯 Next Steps](#-next-steps)

---

## 📝 Part I: Theoretical Foundations (Whitepaper Notes)

> **Note**: This section covers key concepts from the whitepaper "Agent Tools & Interoperability with Model Context Protocol (MCP)"

---

### 🔧 Introduction to Agent Tools

**The Core Problem**

Without tools, AI agents are limited to:
- 🧠 Knowledge frozen at training cutoff date
- 💬 Can only generate text responses
- 🚫 No way to interact with external systems or databases
- ⏰ Cannot take actions in the real world

**The Solution: Tools Transform Agents**

Tools are what bridge the gap between reasoning and action:

| Without Tools | With Tools |
|---------------|------------|
| 💭 "I think the weather is..." | 🌤️ Calls weather API → "It's 72°F and sunny" |
| 📖 "Databases typically store..." | 🗃️ Queries your database → Returns actual data |
| 💬 "You should send an email saying..." | 📧 Sends the actual email via API |

**Key Insight**: Tools convert agents from **advisors** into **executors**.

---

### 🌐 Model Context Protocol (MCP)

#### What is MCP?

**Model Context Protocol (MCP)** is an **open standard** that provides a universal way for AI agents to connect to external data sources and tools.

Think of it as **USB for AI agents**:
- 🔌 **Before USB**: Different cable for every device (chaos!)
- ✨ **With USB**: One standard connector works everywhere
- 🤖 **Before MCP**: Custom integration code for every service
- ✨ **With MCP**: One standard protocol works with any MCP server

#### Why MCP Matters

**The Problem Without MCP:**

```
Your Agent needs to connect to:
├── GitHub → Write custom GitHub API client
├── Slack → Write custom Slack integration
├── Database → Write custom DB connector
├── Google Maps → Write custom Maps integration
└── ... and so on (hundreds of hours of integration work!)
```

**The Solution With MCP:**

```
Your Agent connects to MCP servers:
├── GitHub MCP Server ✅ (community-built)
├── Slack MCP Server ✅ (community-built)
├── Database MCP Server ✅ (community-built)
├── Google Maps MCP Server ✅ (community-built)
└── ... instant access to hundreds of services!
```

#### MCP Architecture

**Client-Server Model:**

```
┌──────────────────────────────────┐
│      Your Agent (MCP Client)      │
│  Uses ADK's McpToolset           │
└────────────┬─────────────────────┘
             │
             │ Standard MCP Protocol
             │ (JSON-RPC over stdio/HTTP)
             │
    ┌────────┴────┬────────┬────────┐
    │             │        │        │
    ▼             ▼        ▼        ▼
┌─────────┐  ┌──────┐ ┌──────┐ ┌─────┐
│ GitHub  │  │Slack │ │ Maps │ │ ... │
│  MCP    │  │ MCP  │ │ MCP  │ │     │
│ Server  │  │Server│ │Server│ │     │
└─────────┘  └──────┘ └──────┘ └─────┘
```

**Three Core Components:**

1. **🔌 Resources**
   - Data that servers expose to clients
   - Examples: File contents, database records, API responses
   - Like read-only files on a shared drive

2. **🛠️ Tools**
   - Actions that clients can invoke
   - Examples: Execute code, send messages, create records
   - Like functions you can call remotely

3. **💬 Prompts**
   - Reusable conversation starters
   - Examples: "Analyze this code", "Summarize these logs"
   - Like templates with placeholders

#### MCP in the Agent Ecosystem

**Key Benefits:**

✅ **Standardization**
- One protocol for all integrations
- Predictable behavior across services
- Easier debugging and monitoring

✅ **Community-Driven**
- Leverage existing MCP servers
- No need to reinvent the wheel
- Growing ecosystem of tools

✅ **Composability**
- Mix and match multiple MCP servers
- Agent can use dozens of services seamlessly
- Scales from simple to complex workflows

✅ **Maintainability**
- Server updates don't break your agent
- Separation of concerns (agent vs. integration logic)
- Update one server, all clients benefit

**Real-World Example:**

A customer support agent with MCP can:
1. 📧 Check email (Email MCP Server)
2. 🔍 Search knowledge base (Database MCP Server)
3. 📊 Pull customer data (CRM MCP Server)
4. 💬 Send Slack notifications (Slack MCP Server)
5. 📝 Update tickets (Ticketing MCP Server)

All without writing custom integration code! 🎉

**Popular MCP Servers:**

| Server | Purpose | Example Use Case |
|--------|---------|------------------|
| **@modelcontextprotocol/server-filesystem** | File operations | Read/write project files |
| **@modelcontextprotocol/server-github** | GitHub API | Analyze PRs, create issues |
| **@modelcontextprotocol/server-postgres** | Database queries | Query production database |
| **@modelcontextprotocol/server-slack** | Slack integration | Send messages, read channels |
| **@gongrzhe/image-gen-server** | Image generation | Create images via Replicate API |

Find more at [modelcontextprotocol.io/examples](https://modelcontextprotocol.io/examples)

---

### 🎯 Key Takeaways (TL;DR)

1. **🔧 Tools Are Essential**
   - Transform agents from advisors to executors
   - Enable real-world actions and data access
   - Bridge the gap between reasoning and doing

2. **🌐 MCP Solves Integration Chaos**
   - Open standard for agent-service connections
   - Like USB for AI - one protocol, many services
   - Community-built servers = instant capabilities

3. **🏗️ Production-Ready Patterns**
   - Custom Function Tools - Your business logic
   - Agent Tools - Delegate to specialists
   - MCP Tools - Connect to external services
   - Long-Running Operations - Human-in-the-loop workflows

4. **🚀 Scale Your Capabilities**
   - Start with simple function tools
   - Add MCP servers for external data
   - Implement approval workflows for critical operations
   - Build multi-agent systems for complex tasks

---

## 💻 Part II: Practical Implementation (Code Exercises)

> **Now let's get hands-on!** This section covers the practical aspects of building agent tools with ADK.

---

## 📚 Course Contents

### Jupyter Notebooks (code/)

1. **day-2a-agent-tools.ipynb**
   - Understanding why agents need tools
   - Building custom function tools with best practices
   - Creating a currency converter agent with multiple tools
   - Using agents as tools (Agent Tools pattern)
   - Improving reliability with code execution
   - Complete guide to ADK tool types

2. **day-2b-agent-tools-best-practices.ipynb**
   - Connecting to external MCP servers
   - Implementing long-running operations
   - Building human-in-the-loop approval workflows
   - Understanding pause-and-resume patterns
   - Managing agent state across conversation breaks
   - Production-ready tool patterns

3. **day-2b-final-exercise-solution.ipynb**
   - Complete solution: Image generation agent with bulk approval
   - Integrating MCP image generation server
   - Implementing bulk request approval workflow
   - Handling single vs. bulk generation requests

### Additional Resources

- **whitepaper/** - "Agent Tools & Interoperability with Model Context Protocol (MCP).pdf"
- **day_02_slides/** - Interactive HTML presentation slides

---

## 🎯 Learning Objectives

By completing Day 2, you will learn to:

### Core Concepts
- ✅ Understand why tools are essential for agents
- ✅ Build custom function tools following ADK best practices
- ✅ Use agents as tools to create specialist hierarchies
- ✅ Connect to external services via Model Context Protocol
- ✅ Implement human-in-the-loop approval workflows
- ✅ Handle long-running operations with pause-resume

### Tool Types You'll Master

#### **1. Custom Function Tools**
- Convert Python functions to agent tools
- Implement structured error handling
- Follow type hints and docstring conventions
- Return dictionary responses with status codes

#### **2. Agent Tools**
- Wrap specialist agents as tools
- Delegate complex tasks to sub-agents
- Build agent hierarchies for specialization
- Improve calculation reliability with code execution

#### **3. MCP Tools**
- Connect to MCP servers (filesystem, GitHub, Slack, etc.)
- Configure stdio and HTTP server connections
- Filter and select specific tools from servers
- Extend capabilities without custom integration code

#### **4. Long-Running Function Tools**
- Implement human-in-the-loop approvals
- Handle pause-and-resume workflows
- Use `ToolContext` for confirmation requests
- Manage state with `ResumabilityConfig`

### Real-World Patterns
- 💰 **Currency Converter** - Multi-tool coordination
- 🚢 **Shipping Coordinator** - Approval workflows
- 🎨 **Image Generator** - Bulk request approvals with MCP

---

## 🚀 Getting Started

### Prerequisites

- Completed Day 1 of the course
- Kaggle account (verified with phone number)
- Gemini API key from [Google AI Studio](https://aistudio.google.com/app/api-keys)
- Basic Python knowledge
- Understanding of async/await patterns (for long-running operations)

### Setup Instructions

#### **Running on Kaggle (Recommended)**

1. **Open a notebook** from the code/ directory in Kaggle
2. **Copy and Edit** to create your own version
3. **Add API Key** to Kaggle Secrets:
   - Go to `Add-ons` → `Secrets`
   - Create secret labeled `GOOGLE_API_KEY`
   - Paste your API key and save
   - Enable the checkbox to attach the secret
4. **Run cells in order** (avoid "Run all" to prevent rate limiting)

#### **Running Locally**

If running outside Kaggle:

```bash
# Install ADK
pip install google-adk

# Set environment variable
export GOOGLE_API_KEY="your-api-key-here"

# For MCP servers, you'll also need Node.js/npm
# Install from: https://nodejs.org/
```

#### **For Image Generation Exercise**

You'll need a Replicate API key:

1. Sign up at [replicate.com](https://replicate.com/)
2. Get your API key from [replicate.com/account/api-tokens](https://replicate.com/account/api-tokens)
3. Add to environment:
   ```bash
   export REPLICATE_API_TOKEN="your-replicate-token"
   ```

---

## 🔧 Core ADK Tool Types

ADK provides two main categories of tools:

### **1. Custom Tools** (Build Your Own)

#### **Function Tools** ⭐
```python
def get_exchange_rate(base: str, target: str) -> dict:
    """Gets currency exchange rate.
    
    Args:
        base: Currency code (e.g., "USD")
        target: Target currency code (e.g., "EUR")
    
    Returns:
        Dictionary with status and rate
    """
    # Your logic here
    return {"status": "success", "rate": 0.93}

# Add to agent
agent = LlmAgent(
    tools=[get_exchange_rate],
    # ...
)
```

#### **Agent Tools** 🤖
```python
# Create specialist agent
calc_agent = LlmAgent(name="calculator", ...)

# Use as tool in another agent
coordinator = LlmAgent(
    tools=[AgentTool(agent=calc_agent)],
    # ...
)
```

#### **Long-Running Function Tools** ⏳
```python
def place_order(amount: int, tool_context: ToolContext) -> dict:
    """Places order with approval for large amounts."""
    
    if amount > 1000:
        # Request approval
        if not tool_context.tool_confirmation:
            tool_context.request_confirmation(
                hint=f"Approve ${amount} order?",
                payload={"amount": amount}
            )
            return {"status": "pending"}
        
        # Handle approval response
        if tool_context.tool_confirmation.confirmed:
            return {"status": "approved"}
        else:
            return {"status": "rejected"}
    
    return {"status": "auto_approved"}
```

#### **MCP Tools** 🌐
```python
# Connect to MCP server
mcp_server = McpToolset(
    connection_params=StdioConnectionParams(
        server_params=StdioServerParameters(
            command="npx",
            args=["-y", "@modelcontextprotocol/server-github"],
        ),
        timeout=30,
    )
)

# Add to agent
agent = LlmAgent(
    tools=[mcp_server],
    # ...
)
```

### **2. Built-in Tools** (Ready to Use)

#### **Gemini Tools** ✨
- `google_search` - Web search powered by Google
- `BuiltInCodeExecutor` - Execute Python code in sandbox

#### **Google Cloud Tools** ☁️
- `BigQueryToolset` - Query BigQuery databases
- `SpannerToolset` - Access Cloud Spanner
- `APIHubToolset` - Enterprise API management

#### **Third-party Tools** 🔌
- Hugging Face models
- Firecrawl web scraping
- GitHub integrations
- And many more...

---

## 💡 Best Practices for Tool Development

### **1. Function Signature Best Practices**

✅ **DO: Use clear type hints**
```python
def calculate_tax(amount: float, rate: float) -> dict:
    """Calculate tax amount."""
    return {"status": "success", "tax": amount * rate}
```

❌ **DON'T: Skip type hints**
```python
def calculate_tax(amount, rate):  # Agent can't understand the types
    return amount * rate
```

### **2. Docstring Best Practices**

✅ **DO: Write detailed docstrings**
```python
def search_products(query: str, max_results: int = 10) -> dict:
    """Search product catalog by keyword.
    
    This tool searches the company's product database and returns
    matching items with their prices and availability.
    
    Args:
        query: Search keywords (e.g., "wireless headphones")
        max_results: Maximum number of results to return (default: 10)
    
    Returns:
        Dictionary with status and product list.
        Success: {"status": "success", "products": [...]}
        Error: {"status": "error", "error_message": "..."}
    """
```

❌ **DON'T: Use minimal docstrings**
```python
def search_products(query: str) -> dict:
    """Search products."""  # Too vague - agent won't know when to use this
```

### **3. Return Value Best Practices**

✅ **DO: Return structured dictionaries**
```python
# Success case
return {
    "status": "success",
    "data": {"order_id": "123", "total": 99.99}
}

# Error case
return {
    "status": "error",
    "error_message": "Payment method not found"
}
```

❌ **DON'T: Return raw values or raise exceptions**
```python
return 99.99  # Agent can't understand what this number means
raise ValueError("Invalid input")  # Will crash agent execution
```

### **4. Error Handling Best Practices**

✅ **DO: Handle errors gracefully**
```python
def get_user_data(user_id: str) -> dict:
    """Fetch user data from database."""
    try:
        user = database.get(user_id)
        if user is None:
            return {
                "status": "error",
                "error_message": f"User {user_id} not found"
            }
        return {"status": "success", "user": user}
    except DatabaseError as e:
        return {
            "status": "error",
            "error_message": f"Database error: {str(e)}"
        }
```

### **5. Tool Naming Best Practices**

✅ **DO: Use descriptive action verbs**
- `get_exchange_rate`
- `place_shipping_order`
- `search_products`
- `calculate_tax`

❌ **DON'T: Use vague names**
- `process` (process what?)
- `handle` (handle what?)
- `tool1` (meaningless)

---

## ⚠️ Important Notes

### Running the Notebooks

> ❌ **Note:** Avoid using the **Run all** cells command as this can trigger QPM (Queries Per Minute) limits resulting in 429 errors when calling the backing model. 

**Suggested workflow**: Run each cell in order - one at a time.

### No Submission Required

> ℹ️ **Note:** These notebooks are for your hands-on practice and learning only. You **do not** need to submit them anywhere to complete the course.

### Rate Limiting

If you encounter 429 errors:
1. Wait a few minutes between requests
2. Run cells one at a time instead of batch execution
3. Check the [FAQ on 429 errors](https://www.kaggle.com/code/kaggle5daysofai/day-0-troubleshooting-and-faqs)

### MCP Server Requirements

- MCP servers using npm packages require **Node.js** installed
- Some servers may require additional API keys (e.g., Replicate, GitHub)
- First run may take longer as packages are installed

### Long-Running Operations

- Requires wrapping agent in `App` with `ResumabilityConfig`
- Must use `Runner` instead of `InMemoryRunner`
- Sessions must be created before running workflows
- `invocation_id` is critical for resuming paused workflows

---

## 📚 Additional Resources

### Documentation
- [ADK Documentation](https://google.github.io/adk-docs/)
- [ADK Tools Overview](https://google.github.io/adk-docs/tools/)
- [ADK Custom Tools Guide](https://google.github.io/adk-docs/tools-custom/)
- [ADK Function Tools](https://google.github.io/adk-docs/tools/function-tools/)
- [ADK MCP Tools](https://google.github.io/adk-docs/tools/mcp-tools/)
- [ADK Third-party Tools](https://google.github.io/adk-docs/tools/third-party/)
- [The App and Runner](https://google.github.io/adk-docs/runtime/)

### MCP Resources
- [Model Context Protocol Specification](https://spec.modelcontextprotocol.io/)
- [MCP Server Examples](https://modelcontextprotocol.io/examples)
- [Kaggle MCP Documentation](https://www.kaggle.com/docs/mcp)
- [MCP GitHub Repository](https://github.com/modelcontextprotocol)

### Video Tutorials
- [ADK Runtime Deep Dive](https://www.youtube.com/watch?v=44C8u0CDtSo&list=PLOU2XLYxmsIIAPgM8FmtEcFTXLLzmh4DK&index=2&t=1s)

### Community
- [Kaggle Discord](https://discord.com/invite/kaggle) - Ask questions and get help
- [ADK GitHub Discussions](https://github.com/google/adk-docs/discussions)

---

## 🎯 Next Steps

You've built the foundation for production-ready agent systems with powerful tools and external integrations.

Continue to **Day 3** to learn about:
- 🧠 **State Management** - How agents remember across conversations
- 💾 **Memory Systems** - Short-term vs. long-term memory
- 🔄 **Session Handling** - Managing multi-user agent systems
- 📊 **Context Engineering** - Optimizing agent performance

---

**License**: Apache License 2.0  
**Copyright**: 2025 Google LLC

**Authors**: [Laxmi Harikumar](https://www.linkedin.com/in/laxmi-harikumar/)

