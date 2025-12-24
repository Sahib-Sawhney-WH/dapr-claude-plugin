---
description: Generate DAPR component YAML files for state stores, pub/sub, bindings, and secrets
---

# DAPR Component Generator

Generate properly configured DAPR component YAML files for various backends.

## Behavior

When the user runs `/dapr:component`:

1. **Select Component Type**
   - State Store (Redis, Cosmos DB, PostgreSQL, MongoDB)
   - Pub/Sub (Redis, Service Bus, Kafka, RabbitMQ)
   - Secret Store (Key Vault, Local File, Kubernetes)
   - Binding (Blob Storage, Event Grid, Cron, HTTP)

2. **Select Backend**
   Based on component type, show relevant options:
   - Local development options (Redis, local file)
   - Azure options (Cosmos DB, Service Bus, Key Vault)
   - Other cloud options

3. **Configure Settings**
   - Component name
   - Connection details
   - Authentication method (managed identity vs. connection string)
   - Component-specific settings

4. **Generate YAML**
   Create component file in `./components/` directory with:
   - Proper schema and version
   - All required metadata
   - Secret references (not plain text)
   - Comments explaining settings

5. **Validate**
   Run validation to ensure component is correct

## Arguments

- `$ARGUMENTS` - Component type and backend:
  - `state redis` - Redis state store
  - `state cosmos` - Azure Cosmos DB
  - `pubsub servicebus` - Azure Service Bus
  - `secrets keyvault` - Azure Key Vault
  - `binding blob` - Azure Blob Storage

## Examples

```
/dapr:component state redis
/dapr:component pubsub servicebus
/dapr:component secrets keyvault
/dapr:component binding cron
```

## Generated Components

### State Store - Redis (Local)
```yaml
# components/statestore.yaml
apiVersion: dapr.io/v1alpha1
kind: Component
metadata:
  name: statestore
spec:
  type: state.redis
  version: v1
  metadata:
  - name: redisHost
    value: localhost:6379
  - name: actorStateStore
    value: "true"
```

### State Store - Cosmos DB (Azure)
```yaml
# components/statestore.yaml
apiVersion: dapr.io/v1alpha1
kind: Component
metadata:
  name: statestore
spec:
  type: state.azure.cosmosdb
  version: v1
  metadata:
  - name: url
    value: https://{account}.documents.azure.com:443/
  - name: database
    value: daprdb
  - name: collection
    value: state
  - name: azureClientId
    value: "{managed-identity-client-id}"
```

### Pub/Sub - Service Bus (Azure)
```yaml
# components/pubsub.yaml
apiVersion: dapr.io/v1alpha1
kind: Component
metadata:
  name: pubsub
spec:
  type: pubsub.azure.servicebus.topics
  version: v1
  metadata:
  - name: namespaceName
    value: "{namespace}.servicebus.windows.net"
  - name: azureClientId
    value: "{managed-identity-client-id}"
  - name: consumerID
    value: "{app-id}"
```

### Secret Store - Key Vault (Azure)
```yaml
# components/secretstore.yaml
apiVersion: dapr.io/v1alpha1
kind: Component
metadata:
  name: secretstore
spec:
  type: secretstores.azure.keyvault
  version: v1
  metadata:
  - name: vaultName
    value: "{vault-name}"
  - name: azureClientId
    value: "{managed-identity-client-id}"
```

### Binding - Cron (Scheduled)
```yaml
# components/scheduled-job.yaml
apiVersion: dapr.io/v1alpha1
kind: Component
metadata:
  name: scheduled-job
spec:
  type: bindings.cron
  version: v1
  metadata:
  - name: schedule
    value: "@every 5m"
```

## Interactive Prompts

When running without arguments, prompt for:
1. Component type (state/pubsub/secrets/binding)
2. Backend service
3. Environment (local/azure/other)
4. Component name
5. Connection details based on backend

## Best Practices Applied

- Uses managed identity for Azure services
- Separates dev/prod configurations
- Includes comments for customization
- Sets appropriate defaults
- Validates before saving
