# TaskMaster Shared Workflows

Centralized GitHub Actions workflows for all TaskMaster repositories.

## 🔄 Available Workflows

| Workflow | Description | Usage |
|----------|-------------|-------|
| `reusable-auto-rebase.yml` | Auto-rebase PRs when main is updated | All repos |
| `reusable-release.yml` | Create GitHub releases with changelog | All repos |
| `reusable-dotnet-build.yml` | Build and test .NET projects | .NET repos |
| `reusable-docker-build.yml` | Build Docker images to ACR | Container repos |
| `reusable-deploy-aca.yml` | Deploy to Azure Container Apps | ACA repos |

## 📦 Usage

Add a workflow file to your repo that calls the shared workflow:

```yaml
# .github/workflows/auto-rebase.yml
name: Auto-Rebase PRs

on:
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  rebase:
    uses: jasonberkes/taskmaster-shared-workflows/.github/workflows/reusable-auto-rebase.yml@main
    secrets: inherit
```

## 🔐 Required Secrets

Calling repos need these secrets configured:

| Secret | Required For | Description |
|--------|--------------|-------------|
| `TASKMASTER_API_KEY` | auto-rebase | API key for AI conflict resolution |
| `AZURE_CREDENTIALS` | deploy-aca | Azure service principal |
| `AZURE_REGISTRY_*` | docker-build | ACR credentials |

## 📋 Versioning

- Use `@main` for latest stable
- Use `@v1` for pinned versions (coming soon)
- Use `@sha` for exact commit

## 🏗️ Repository List

Repos using these workflows:
- taskmaster-platform
- TaskMaster.AgentFramework
- TaskMaster.DocumentService
- TaskMaster.Redis
- taskmaster-ui
- taskmaster-mcp-server
