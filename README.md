# DAPR Plugin for Claude Code

A comprehensive Claude Code plugin for developing, deploying, and debugging DAPR (Distributed Application Runtime) applications with Python.

## Features

### Full DAPR Building Block Support
- **Service Invocation** - HTTP/gRPC service-to-service communication
- **State Management** - Redis, Cosmos DB, PostgreSQL, MongoDB
- **Pub/Sub Messaging** - Azure Service Bus, Kafka, Redis Streams
- **Bindings** - Azure Blob, Event Grid, Cron, HTTP webhooks
- **Secrets Management** - Azure Key Vault, local files
- **Virtual Actors** - Stateful, concurrent processing
- **Workflows** - Durable, long-running orchestration

### Azure Integration
- Azure Container Apps with managed DAPR
- Azure Kubernetes Service (AKS)
- Azure Cosmos DB for state
- Azure Service Bus for messaging
- Azure Key Vault for secrets
- Managed Identity authentication

### High Automation
- Validate configurations on save
- Generate boilerplate code
- Proactive debugging assistance
- Azure deployment automation

## Installation

```bash
# Install the plugin
claude plugin install dapr

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

## Agents

The plugin includes specialized AI agents that are automatically invoked when relevant:

| Agent | When Used |
|-------|-----------|
| `dapr-architect` | Designing distributed systems architecture |
| `microservices-expert` | Writing service code with DAPR SDK |
| `dapr-debugger` | Diagnosing runtime errors and failures |
| `azure-deployer` | Deploying to Azure Container Apps/AKS |
| `workflow-expert` | Creating durable workflows |
| `config-specialist` | Configuring DAPR components |

## Quick Start

### 1. Create a New Project

```
/dapr:init my-service
```

This creates a FastAPI microservice with:
- DAPR SDK integration
- State management helpers
- Pub/sub support
- Health endpoints
- Docker configuration
- Component YAML files

### 2. Run Locally

```
/dapr:run
```

Or manually:
```bash
dapr run --app-id my-service --app-port 8000 -- python main.py
```

### 3. Deploy to Azure

```
/dapr:deploy aca
```

## Project Structure

Projects created with `/dapr:init` follow this structure:

```
my-service/
├── src/
│   └── main.py              # FastAPI application
├── components/
│   ├── statestore.yaml      # State store config
│   ├── pubsub.yaml          # Pub/sub config
│   └── secrets.yaml         # Secrets config
├── dapr.yaml                # DAPR multi-app config
├── requirements.txt         # Python dependencies
├── Dockerfile               # Container image
└── README.md                # Documentation
```

## Component Generation

Generate properly configured DAPR components:

```
/dapr:component state redis        # Redis state store
/dapr:component state cosmos       # Azure Cosmos DB
/dapr:component pubsub servicebus  # Azure Service Bus
/dapr:component secrets keyvault   # Azure Key Vault
```

## Workflow Scaffolding

Create durable workflows with different patterns:

```
/dapr:workflow order-processing                    # Sequential
/dapr:workflow payment-saga --pattern saga         # With compensation
/dapr:workflow document-approval --pattern approval # Human approval
/dapr:workflow batch-job --pattern parallel        # Fan-out/fan-in
```

## Azure Deployment

### Container Apps (Recommended)

```
/dapr:deploy aca --rg my-resource-group
```

Features:
- Managed DAPR runtime
- Automatic sidecar injection
- Built-in scaling
- Managed identity support

### AKS

```
/dapr:deploy aks --rg my-resource-group
```

Features:
- Full Kubernetes control
- DAPR control plane
- Service mesh integration

## Best Practices

The plugin enforces DAPR best practices:

### Configuration
- Validates component YAML on save
- Checks for secrets in plain text
- Verifies required fields

### Security
- Recommends managed identity over connection strings
- Scopes sensitive components
- Uses secret stores for credentials

### Observability
- Includes OpenTelemetry setup
- Structured logging
- Health endpoints

### Resiliency
- Retry policies
- Circuit breakers
- Timeout configuration

## Troubleshooting

When you encounter issues, the plugin automatically:

1. **Detects error patterns** - Recognizes common DAPR errors
2. **Diagnoses root cause** - Checks configuration and connectivity
3. **Suggests fixes** - Provides specific commands and code changes
4. **Validates fixes** - Confirms the issue is resolved

Common issues handled:
- Sidecar not starting
- Service invocation failures
- State store connection errors
- Pub/sub message delivery problems
- Component configuration errors

## Requirements

- Python 3.9+
- DAPR CLI (`dapr init`)
- Docker (for local development)
- Azure CLI (for Azure deployment)

## License

MIT

## Support

For issues and feature requests, please open an issue on the plugin repository.
