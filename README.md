# DAPR Plugin for Claude Code v2.0

A comprehensive Claude Code plugin for developing, deploying, and debugging DAPR (Distributed Application Runtime) applications with Python.

## What's New in v2.0

- **Complete Building Block Coverage** - All 12 DAPR building blocks supported
- **Testing Support** - Mocked DAPR clients, pytest fixtures, integration tests
- **CI/CD Integration** - GitHub Actions and Azure DevOps pipelines
- **Observability** - OpenTelemetry tracing, structured logging, metrics
- **Security Scanning** - Detect plain-text secrets, validate ACLs
- **Multi-Service Projects** - Shared configuration, cross-service debugging
- **Example Projects** - E-commerce saga, IoT processing, saga patterns

## Features

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
| **Configuration** | Dynamic app configuration | `configuration.yaml` |
| **Distributed Lock** | Mutex across services | `lock.yaml` |
| **Cryptography** | Encrypt/decrypt operations | `crypto.yaml` |
| **Jobs** | Scheduled task execution | `job.yaml` |
| **Conversation** | LLM/AI integration | `conversation.yaml` |

### Azure Integration

- Azure Container Apps with managed DAPR
- Azure Kubernetes Service (AKS)
- Azure Cosmos DB for state
- Azure Service Bus for messaging
- Azure Key Vault for secrets and cryptography
- Azure App Configuration for dynamic config
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

## Skills

Auto-triggered skills for specific tasks:

| Skill | Trigger |
|-------|---------|
| `dapr-validation` | Validates component YAML files on save |
| `dapr-code-generation` | Generates Python code from components |
| `dapr-troubleshooting` | Diagnoses errors in logs |
| `security-scanner` | Detects secrets and security issues |
| `observability-setup` | Configures OpenTelemetry and monitoring |

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

### 2. Run Locally

```
/dapr:run
```

### 3. Add Testing

```
/dapr:test unit      # Unit tests with mocked DAPR
/dapr:test integration  # Integration tests with real DAPR
```

### 4. Deploy to Azure

```
/dapr:deploy aca
```

## Multi-Service Projects

Create projects with multiple services:

```
/dapr:project shop --services "order-service,inventory-service,payment-service"
```

Or use templates:

```
/dapr:project shop --template ecommerce
/dapr:project iot-hub --template iot
/dapr:project order-saga --template saga
```

### Generated Structure

```
shop/
├── dapr.yaml                      # Multi-app configuration
├── components/                    # Shared DAPR components
│   ├── statestore.yaml
│   ├── pubsub.yaml
│   └── resiliency.yaml
├── services/
│   ├── order-service/
│   ├── inventory-service/
│   └── payment-service/
├── infrastructure/
│   ├── docker-compose.yaml
│   └── bicep/
└── tests/
```

## New Building Blocks (v2.0)

### Configuration API

```python
from dapr.clients import DaprClient

async with DaprClient() as client:
    # Get configuration
    config = await client.get_configuration(
        store_name="configstore",
        keys=["feature-flags", "rate-limits"]
    )

    # Subscribe to changes
    async for update in client.subscribe_configuration(
        store_name="configstore",
        keys=["feature-flags"]
    ):
        print(f"Config updated: {update}")
```

### Distributed Lock

```python
async with DaprClient() as client:
    # Acquire lock
    lock = await client.try_lock(
        store_name="lockstore",
        resource_id="order-123",
        lock_owner="service-a",
        expiry_in_seconds=60
    )

    if lock.success:
        # Critical section
        await process_order()
        await client.unlock(
            store_name="lockstore",
            resource_id="order-123",
            lock_owner="service-a"
        )
```

### Cryptography

```python
async with DaprClient() as client:
    # Encrypt
    encrypted = await client.encrypt(
        data=b"sensitive data",
        options=EncryptOptions(
            component_name="vault",
            key_name="my-key",
            key_wrap_algorithm="RSA"
        )
    )

    # Decrypt
    decrypted = await client.decrypt(
        data=encrypted,
        options=DecryptOptions(component_name="vault")
    )
```

### Jobs (Scheduled Tasks)

```python
async with DaprClient() as client:
    # Schedule a job
    await client.schedule_job(
        name="daily-cleanup",
        schedule="0 0 * * *",  # Cron: midnight daily
        data={"type": "cleanup"}
    )
```

### Conversation (LLM)

```python
async with DaprClient() as client:
    response = await client.converse(
        component_name="openai",
        inputs=[
            ConversationInput(content="Hello!", role="user")
        ]
    )
    print(response.outputs[0].content)
```

## CI/CD Integration

Generate production-ready pipelines:

```
/dapr:cicd github --target aca
/dapr:cicd azure-devops --target aks
```

### Generated Pipeline Features

**CI (Continuous Integration)**
- Ruff linting, MyPy type checking
- Unit tests with pytest
- DAPR configuration validation
- Security scanning with Trivy
- Container build and push

**CD (Continuous Deployment)**
- Blue-green deployment
- Health check verification
- Automatic rollback on failure
- DAPR component updates

## Security Scanning

```
/dapr:security
```

Detects:
- Plain-text secrets in component files
- Missing secret store references
- Hardcoded connection strings
- Missing access control policies
- Unscoped components

## Testing Support

### Mocked DAPR Client

```python
import pytest
from tests.conftest import mock_dapr_client

async def test_state_operations(mock_dapr_client):
    await mock_dapr_client.save_state("store", "key", "value")
    state = await mock_dapr_client.get_state("store", "key")
    assert state.data == b"value"
```

### Integration Tests

```python
@pytest.mark.integration
async def test_service_invocation():
    async with DaprClient() as client:
        response = await client.invoke_method(
            app_id="my-service",
            method_name="health"
        )
        assert response.status_code == 200
```

## Example Projects

### E-Commerce (Saga Pattern)
Complete order processing with inventory reservation, payment, and compensation.

```
examples/ecommerce/
├── services/
│   ├── order-service/      # Workflow orchestration
│   ├── inventory-service/  # Actor-based stock
│   ├── payment-service/    # Payment processing
│   └── notification-service/
└── dapr.yaml
```

### IoT Processing
Real-time device telemetry with actors and alerting.

```
examples/iot-processing/
├── services/
│   ├── device-gateway/     # Telemetry ingestion
│   ├── device-actor/       # Per-device state
│   ├── analytics-service/  # Stream processing
│   └── alerting-service/
└── dapr.yaml
```

### Saga Patterns
Sequential, parallel, and choreography saga examples.

```
examples/saga-patterns/
├── services/
│   ├── orchestrator/       # Saga coordinator
│   ├── service-a/
│   ├── service-b/
│   └── service-c/
└── README.md               # Pattern documentation
```

## Hooks (Auto-Validation)

The plugin automatically validates:
- Component YAML files on save
- Resiliency policy configurations
- GitHub Actions workflows
- Dockerfiles for DAPR compatibility
- Secret files for plain-text credentials

## Requirements

- Python 3.9+
- DAPR CLI (`dapr init`)
- Docker (for local development)
- Azure CLI (for Azure deployment)

## License

MIT

## Support

For issues and feature requests, please open an issue on the [plugin repository](https://github.com/Sahib-Sawhney-WH/dapr-claude-plugin).
