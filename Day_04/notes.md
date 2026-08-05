# Model Context Protocol (MCP)

## Overview

Large Language Models (LLMs) are powerful at understanding and generating text, but they **cannot interact with the real world on their own**.

For example, an LLM **cannot**:
- Read your private GitHub repository
- Access your MongoDB database
- Send Slack messages
- Book a meeting on Google Calendar
- Deploy your application

To perform these tasks, the LLM needs a bridge.

That bridge is **Model Context Protocol (MCP).**

---

# Learning Flow

```
AI
│
├── Machine Learning
│
├── Deep Learning
│
├── Large Language Models (LLMs)
│
├── Generative AI
│
├── AI Agents
│
└── Model Context Protocol (MCP)
```

---

# 1. What is an LLM?

**LLM (Large Language Model)** is a Deep Learning model trained on massive amounts of text data.

Its primary job is to predict the next most likely word based on previous words.

Because it has learned language patterns, it can:

- Answer questions
- Write code
- Summarize text
- Translate languages
- Generate ideas

### Popular Examples

- GPT-4
- Claude
- Gemini
- Llama

---

# 2. Limitations of LLMs

Although LLMs are intelligent, they have important limitations.

They **cannot directly:**

- Access private files
- Read databases
- Control applications
- Use external software
- Interact with APIs automatically

They only understand the information given to them.

---

# 3. What is a Protocol?

A **protocol** is a standardized set of rules that allows two systems to communicate.

Think of it as a common language.

### Examples

- HTTP → Web communication
- HTTPS → Secure web communication
- FTP → File transfer
- SMTP → Sending emails

Without protocols, computers wouldn't know how to exchange information correctly.

---

# 4. What is MCP?

**MCP (Model Context Protocol)** is an open standard introduced by Anthropic that allows AI models to communicate with external tools, applications, and data sources.

Think of it as:

> **USB-C for AI**

Instead of creating a custom integration for every AI model and every application, MCP provides one standard way for them to communicate.

---

# 5. Why is MCP Needed?

Without MCP:

```
Claude
   │
   ├── Custom GitHub Integration
   ├── Custom Slack Integration
   ├── Custom Database Integration
   ├── Custom Figma Integration
   └── Custom Google Drive Integration
```

Every service requires a separate integration.

---

With MCP:

```
Claude
      │
      ▼
   MCP Client
      │
────────────────────────
│        │        │
▼        ▼        ▼
GitHub  MongoDB  Slack
MCP      MCP      MCP
Server   Server   Server
```

The AI only needs to understand MCP.

---

# 6. MCP Architecture

```
User
   │
   ▼
Claude / ChatGPT / Gemini
        │
        ▼
    MCP Client
        │
        ▼
    MCP Server
        │
────────┼──────────────
│       │       │
GitHub MongoDB Slack
```

---

# 7. Core Components of MCP

## A. Tools

Functions the AI can execute.

Examples

- Read GitHub Issues
- Query Database
- Send Email
- Create Calendar Event

---

## B. Resources

External information provided to the AI.

Examples

- CSV files
- Markdown files
- Source code
- Documentation
- Images

---

## C. Prompts

Reusable prompt templates that improve user interactions.

Instead of writing long prompts repeatedly, predefined prompts can be reused.

---

## D. Sampling

Allows different AI models to collaborate on specific tasks.

Example

```
Claude
   │
   ▼
Uses another AI model
for a specialized task
```

---

# 8. MCP Client vs MCP Server

## MCP Client

The application that wants to use tools.

Examples

- Claude Desktop
- Claude Code
- ChatGPT (when supported)

---

## MCP Server

A program that exposes tools and resources to the AI.

Example:

```
GitHub MCP Server

Tools

✓ create_issue()
✓ search_repository()
✓ create_pull_request()
✓ list_repositories()
```

---

# 9. What are Connectors?

A connector is usually a ready-made implementation of an MCP server.

Instead of building your own GitHub integration, you simply install the connector.

Example

```
Claude Code
      │
GitHub Connector
      │
GitHub API
```

The connector handles communication with GitHub.

---

# 10. Can You Build Your Own MCP Server?

Yes.

Developers can build MCP servers using languages like:

- JavaScript / Node.js
- Python

You simply register tools and expose them to AI clients.

---

# 11. SDK (Software Development Kit)

An SDK is a collection of tools that helps developers build applications faster.

An SDK typically includes:

- Libraries
- APIs
- Documentation
- Sample code
- Debugging tools

Think of it as a developer's toolbox.

---

# 12. API vs SDK vs MCP

## API

A way for one software application to communicate with another.

Example

```
Application
      │
      ▼
GitHub API
```

---

## SDK

A toolkit that helps developers use APIs more easily.

Example

```
SDK
├── Libraries
├── APIs
├── Examples
└── Documentation
```

---

## MCP

A protocol that allows AI models to discover and use tools in a standardized way.

Example

```
AI
 │
 ▼
MCP
 │
 ▼
GitHub API
```

MCP does **not replace APIs**.

It makes APIs easier for AI systems to understand and use.

---

# 13. API vs MCP

| API | MCP |
|------|-----|
| Built for software applications | Built specifically for AI |
| Fixed endpoints | AI discovers available tools |
| Developer writes integration | Standardized integration |
| App ↔ App communication | AI ↔ Tools communication |

---

# 14. Practical Example

Without MCP

```
User
 │
 ▼
Claude

"I can't access your GitHub repository."
```

---

With MCP

```
User
 │
 ▼
Claude
 │
 ▼
GitHub MCP Server
 │
 ▼
GitHub Repository
```

Now Claude can:

- Read code
- Create issues
- Review pull requests
- Search repositories

---

# Key Takeaways

- LLMs generate text but cannot access external systems on their own.
- Protocols define the rules for communication between systems.
- MCP is an open standard that connects AI models with external tools and data.
- MCP uses four main components:
  - Tools
  - Resources
  - Prompts
  - Sampling
- Connectors are typically pre-built MCP servers for specific services.
- SDKs help developers build software faster by providing reusable tools.
- APIs enable communication between software, while MCP standardizes how AI interacts with those APIs.

---

# New Concepts Learned

- Model Context Protocol (MCP)
- MCP Client
- MCP Server
- Tools
- Resources
- Prompts
- Sampling
- Protocol
- SDK
- Connectors
- API vs SDK vs MCP
- LLM Limitations

---

# Additional Learning Resources

- **Anthropic MCP Introduction**  
  https://www.anthropic.com/news/model-context-protocol

- **PulseMCP** (Discover MCP servers & tools)  
  https://www.pulsemcp.com

- **MCP App Store** (Browse available MCP servers)  
  https://mcp.so