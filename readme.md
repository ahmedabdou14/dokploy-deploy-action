# Dokploy Deployment GitHub Action

This GitHub Action triggers a deployment on Dokploy using the latest API format. It supports both application and compose deployments.

> **Note**: This is an updated fork of the original `benbristow/dokploy-deploy-action` which is outdated and uses deprecated authentication methods. This version uses the current Dokploy API with `x-api-key` authentication with support for both application and compose deployments.

## Inputs

| Input | Description | Required | Example |
|-------|-------------|----------|---------|
| `dokploy_url` | Dokploy dashboard URL (no trailing slash) | ✅ | `https://dokploy.example.com` |
| `auth_token` | Dokploy API key | ✅ | `your-api-key-here` |
| `application_id` | Dokploy application ID (for application deployments) | ❌* | `app-123456` |
| `compose_id` | Dokploy compose ID (for compose deployments) | ❌* | `compose-789` |

*Provide either `application_id` OR `compose_id` (not both).

## Setup

1. [**Get your Dokploy API Key**](https://docs.dokploy.com/docs/core/auto-deploy#steps-to-deploy-using-api)

2. **Find your Resource ID**:
   - For applications: [Find your Application ID](https://docs.dokploy.com/docs/core/auto-deploy#steps-to-deploy-using-api)
   - For compose: Find your Compose ID in the Dokploy dashboard

3. **Set up GitHub Secrets**:
   - Go to your repository → Settings → Secrets and variables → Actions
   - Add the required secrets:
     - `DOKPLOY_URL`: Your Dokploy instance URL
     - `DOKPLOY_API_KEY`: Your API key from step 1
     - `DOKPLOY_APPLICATION_ID`: Your application ID (for application deployments) OR
     - `DOKPLOY_COMPOSE_ID`: Your compose ID (for compose deployments)

## Usage

### Application Deployment

Provide your `application_id` to deploy an application:

```yaml
name: Deploy Application to Dokploy

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout code
      uses: actions/checkout@v4

    - name: Deploy to Dokploy
      uses: ahmedabdou14/dokploy-deploy-gha@v1.1.0
      with:
        dokploy_url: ${{ secrets.DOKPLOY_URL }}
        auth_token: ${{ secrets.DOKPLOY_API_KEY }}
        application_id: ${{ secrets.DOKPLOY_APPLICATION_ID }}
```

### Compose Deployment

Provide your `compose_id` to deploy a compose stack:

```yaml
name: Deploy Compose to Dokploy

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout code
      uses: actions/checkout@v4

    - name: Deploy to Dokploy
      uses: ahmedabdou14/dokploy-deploy-gha@v1.1.0
      with:
        dokploy_url: ${{ secrets.DOKPLOY_URL }}
        auth_token: ${{ secrets.DOKPLOY_API_KEY }}
        compose_id: ${{ secrets.DOKPLOY_COMPOSE_ID }}
```
