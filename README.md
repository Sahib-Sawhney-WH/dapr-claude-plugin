# DAPR Plugin for Claude Code v2.1

A comprehensive Claude Code plugin for developing, deploying, and debugging DAPR (Distributed Application Runtime) applications with Python.

## What's New in v2.1

- **DAPR Agents AI Framework** - Build intelligent, durable AI agents
- **Agentic Patterns** - Prompt chaining, parallelization, routing, evaluator-optimizer, human-in-the-loop
- **Multi-Agent Orchestration** - Workflow-based agent coordination
- **Tool Templates** - HTTP, state, pub/sub, MCP integration tools
- **CrewAI Integration** - Run CrewAI crews as durable DAPR workflows
- **OpenAI Agents Integration** - Session management with DAPR state persistence
- **Agent-Builder Skill** - Auto-validates agent configurations

## v2.0 Features (Still Available)

- **Complete Building Block Coverage** - All 12 DAPR building blocks supported
- **Testing Support** - Mocked DAPR clients, pytest fixtures, integration tests
- **CI/CD Integration** - GitHub Actions and Azure DevOps pipelines
- **Observability** - OpenTelemetry tracing, structured logging, metrics
- **Security Scanning** - Detect plain-text secrets, validate ACLs
- **Multi-Service Projects** - Shared configuration, cross-service debugging
- **Example Projects** - E-commerce saga, IoT processing, saga patterns

## Features

### DAPR Agents AI Framework

Build intelligent agents with the DAPR Agents framework:

| Agent Type | Description | Template |
|------------|-------------|----------|
| AssistantAgent | Interactive LLM-powered agents | `assistant_agent.py` |
| DurableAgent | Workflow-backed fault-tolerant agents | `durable_agent.py` |
| AgentService | Headless REST API agents | `agent_service.py` |
| Multi-Agent | Orchestrated agent systems | `multi_agent_workflow.py` |

### Agentic Patterns

| Pattern | Description | Use Case |
|---------|-------------|----------|
| Prompt Chaining | Sequential LLM calls | Document analysis pipelines |
| Parallelization | Concurrent task execution | Multi-document processing |
| Routing | Dynamic agent selection | Support ticket routing |
| Evaluator-Optimizer | Iterative refinement | Content quality improvement |
| Human-in-the-Loop | External approval gates | Sensitive action workflows |

### All 12 DAPR Building Blocks

| Building Block | Description | Component Template |
|----------------|-------------|-------------------|
| Service Invocation | Service-to-service calls | Built-in |
| State Management | Key-value storage | `statestore.yaml` |
| Pub/Sub | Event-driven messaging | `pubsub.yaml` |
| Bindings | External system triggers | `binding-*.yaml` |
| Secrets | Secure credential storage | `secretstore.yaml` |
| Actors | Virtual actor pattern | `statestore.yaml` (with actors) |
| Workflows | Durable orchestration | Built-in |
| Configuration | Dynamic app configuration | `configuration.yaml` |
| Distributed Lock | Mutex across services | `lock.yaml` |
| Cryptography | Encrypt/decrypt operations | `crypto.yaml` |
| Jobs | Scheduled task execution | `job.yaml` |
| Conversation | LLM/AI integration | `conversation.yaml` |

### Azure Integration

- Azure Container Apps with managed DAPR
- Azure Kubernetes Service (AKS)
- Azure Cosmos DB for state
- Azure Service Bus for messaging
- Azure Key Vault for secrets and cryptography
- Azure App Configuration for dynamic config
- Azure OpenAI for LLM agents
- Managed Identity authentication

## Installation

```bash
# Install from GitHub
claude plugin install github:Sahib-Sawhney-WH/dapr-claude-plugin

# Or from local path
claude --plugin-dir /path/to/dapr-plugin
```

## Commands

| Command | Description |
|---------|-------------|
| `/dapr:init` | Initialize a new DAPR project with templates |
| `/dapr:run` | Run DAPR application locally with sidecar |
| `/dapr:deploy` | Deploy to Azure Container Apps or AKS |
| `/dapr:logs` | View and filter DAPR service logs |
| `/dapr:status` | Check DAPR runtime and Azure status |
| `/dapr:component` | Generate component YAML files |
| `/dapr:workflow` | Scaffold a new DAPR workflow |
| `/dapr:test` | Run unit, integration, or E2E tests |
| `/dapr:security` | Scan for security issues |
| `/dapr:cicd` | Generate CI/CD pipelines |
| `/dapr:project` | Initialize multi-service projects |
| `/dapr:agent` | **NEW** Create DAPR AI agents |

## Agents

Specialized AI agents automatically invoked when relevant:

| Agent | When Used |
|-------|-----------|
| `dapr-architect` | Designing distributed systems architecture |
| `microservices-expert` | Writing service code with all DAPR building blocks |
| `dapr-debugger` | Diagnosing runtime errors and failures |
| `azure-deployer` | Deploying to Azure Container Apps/AKS |
| `workflow-expert` | Creating durable workflows and sagas |
| `config-specialist` | Configuring DAPR components |
| `multi-service-expert` | Cross-service debugging, service mesh |
| `ai-agent-expert` | **NEW** Building AI agents with DAPR Agents framework |

## Skills

Auto-triggered skills for specific tasks:

| Skill | Trigger |
|-------|---------|
| `dapr-validation` | Validates component YAML files on save |
| `dapr-code-generation` | Generates Python code from components |
| `dapr-troubleshooting` | Diagnoses errors in logs |
| `security-scanner` | Detects secrets and security issues |
| `observability-setup` | Configures OpenTelemetry and monitoring |
| `agent-builder` | **NEW** Validates AI agent configurations |

## Quick Start

### 1. Create a New Project

```
/dapr:init my-service
```

Creates a FastAPI microservice with:
- DAPR SDK integration
- All building block helpers
- Health endpoints
- Docker configuration
- Component YAML files

### 2. Create an AI Agent

```
/dapr:agent assistant my-agent
```

Options:
```
/dapr:agent assistant <name>     # Basic interactive agent
/dapr:agent durable <name>       # Workflow-backed durable agent
/dapr:agent service <name>       # Headless REST API agent
/dapr:agent multi <name>         # Multi-agent orchestration
```

### 3. Run Locally

```
/dapr:run
```

### 4. Deploy to Azure

```
/dapr:deploy aca
```

## DAPR Agents (v2.1)

### Basic Agent

```python
from dapr_agents import AssistantAgent, tool

@tool
async def search(query: str) -> str:
    """Search for information."""
    # Your implementation
    return f"Results for: {query}"

agent = AssistantAgent(
    name="assistant",
    role="Helpful Assistant",
    instructions="Help users find information.",
    tools=[search],
    model="gpt-4o"
)

# Run interactively
await agent.run("Search for DAPR documentation")
```

### Durable Agent (Workflow-Backed)

```python
from dapr.ext.workflow import workflow, activity
from dapr_agents import AssistantAgent

@activity
async def research_activity(ctx, topic: str) -> str:
    agent = AssistantAgent(name="researcher", ...)
    return await agent.run(f"Research: {topic}")

@workflow
def research_workflow(ctx: DaprWorkflowContext, topic: str):
    # Durable execution with automatic retries
    result = yield ctx.call_activity(research_activity, input=topic)
    return result
```

### Multi-Agent System

```python
from dapr_agents import AssistantAgent

# Specialized agents
technical = AssistantAgent(name="technical", role="Technical Support", ...)
billing = AssistantAgent(name="billing", role="Billing Support", ...)

# Router agent
router = AssistantAgent(
    name="router",
    instructions="Route requests to technical or billing based on content.",
    ...
)

# Orchestrate via DAPR workflow
@workflow
def multi_agent_workflow(ctx, request):
    category = yield ctx.call_activity(route, input=request)
    result = yield ctx.call_activity(handle, input={"category": category, ...})
    return result
```

### Agent Tools

```python
from dapr_agents import tool
from dapr.clients import DaprClient

@tool
async def save_to_state(key: str, value: str) -> str:
    """Save data to DAPR state store."""
    async with DaprClient() as client:
        await client.save_state("statestore", key, value)
    return f"Saved: {key}"

@tool
async def publish_event(topic: str, data: dict) -> str:
    """Publish event via DAPR pub/sub."""
    async with DaprClient() as client:
        await client.publish_event("pubsub", topic, data)
    return f"Published to: {topic}"
```

### MCP Integration

```python
from dapr_agents.mcp import MCPClient, MCPServerConfig

# Connect to MCP servers
mcp_config = MCPServerConfig(
    name="filesystem",
    command="npx",
    args=["-y", "@modelcontextprotocol/server-filesystem", "/data"]
)

client = MCPClient(mcp_config)
await client.connect()
tools = await client.list_tools()

# Use MCP tools with your agent
agent = AssistantAgent(
    name="mcp-agent",
    tools=tools,
    ...
)
```

## Framework Integrations

### CrewAI + DAPR

Run CrewAI crews as durable DAPR workflows:

```python
from crewai import Agent, Task, Crew
from dapr.ext.workflow import workflow, activity

@activity
async def run_crew(ctx, topic: str) -> str:
    researcher = Agent(role="Researcher", ...)
    writer = Agent(role="Writer", ...)

    crew = Crew(
        agents=[researcher, writer],
        tasks=[...],
        process=Process.sequential
    )

    return crew.kickoff()

@workflow
def crewai_workflow(ctx, topic):
    # Durable execution with checkpointing
    result = yield ctx.call_activity(run_crew, input=topic)
    return result
```

### OpenAI Agents + DAPR

Persistent sessions with DAPR state:

```python
from openai import OpenAI
from dapr.clients import DaprClient

class DaprSessionManager:
    async def save_session(self, session_id: str, thread_id: str):
        async with DaprClient() as client:
            await client.save_state(
                "statestore",
                f"session-{session_id}",
                {"thread_id": thread_id}
            )

    async def load_session(self, session_id: str):
        async with DaprClient() as client:
            state = await client.get_state("statestore", f"session-{session_id}")
            return state.data
```

## Template Structure

```
templates/
├── agents/
│   ├── assistant_agent.py      # Basic AssistantAgent
│   ├── durable_agent.py        # Workflow-backed agent
│   ├── agent_service.py        # REST API agent
│   ├── multi_agent_workflow.py # Multi-agent system
│   ├── requirements.txt
│   ├── patterns/
│   │   ├── prompt_chaining.py
│   │   ├── parallelization.py
│   │   ├── routing.py
│   │   ├── evaluator_optimizer.py
│   │   └── human_in_loop.py
│   └── tools/
│       ├── custom_tool_template.py
│       ├── http_tool.py
│       ├── state_tool.py
│       ├── pubsub_tool.py
│       └── mcp_integration.py
└── integrations/
    ├── crewai_workflow.py
    ├── openai_agents_session.py
    └── requirements.txt
```

## Hooks (Auto-Validation)

The plugin automatically validates:
- Component YAML files on save
- Agent configurations (`*_agent.py`, `*agent*.py`)
- Tool definitions (`tools/*.py`)
- Pattern implementations (`patterns/*.py`)
- Integration code (`integrations/*.py`)
- Resiliency policy configurations
- GitHub Actions workflows
- Dockerfiles for DAPR compatibility
- Secret files for plain-text credentials

## Requirements

- Python 3.9+
- DAPR CLI (`dapr init`)
- Docker (for local development)
- Azure CLI (for Azure deployment)
- OpenAI API key or Azure OpenAI (for AI agents)

## Environment Variables

```bash
# LLM Configuration (for AI Agents)
OPENAI_API_KEY=sk-...
AZURE_OPENAI_API_KEY=...
AZURE_OPENAI_ENDPOINT=...
LLM_MODEL=gpt-4o

# DAPR Configuration
DAPR_HTTP_PORT=3500
DAPR_GRPC_PORT=50001
STATE_STORE_NAME=statestore
PUBSUB_NAME=pubsub
```

## License

MIT

## Support

For issues and feature requests, please open an issue on the [plugin repository](https://github.com/Sahib-Sawhney-WH/dapr-claude-plugin).
