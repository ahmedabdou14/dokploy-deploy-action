# Dokploy Deployment GitHub Action

This GitHub Action triggers a deployment on Dokploy using the latest API format.

> **Note**: This is an updated fork of the original `benbristow/dokploy-deploy-action` which is outdated and uses deprecated authentication methods. This version uses the current Dokploy API with `x-api-key` authentication.

## Inputs

| Input | Description | Required | Example |
|-------|-------------|----------|---------|
| `dokploy_url` | Dokploy dashboard URL (no trailing slash) | ✅ | `https://dokploy.example.com` |
| `auth_token` | Dokploy API key | ✅ | `your-api-key-here` |
| `application_id` | Dokploy application ID | ✅ | `app-123456` |

## Setup

1. [**Get your Dokploy API Key**](https://docs.dokploy.com/docs/core/auto-deploy#steps-to-deploy-using-api)

2. [**Find your Application ID**](https://docs.dokploy.com/docs/core/auto-deploy#steps-to-deploy-using-api)

3. **Set up GitHub Secrets**:
   - Go to your repository → Settings → Secrets and variables → Actions
   - Add the following secrets:
     - `DOKPLOY_URL`: Your Dokploy instance URL
     - `DOKPLOY_API_KEY`: Your API key from step 1
     - `DOKPLOY_APPLICATION_ID`: Your application ID from step 2

## Usage

Add this action to your workflow file (e.g., `.github/workflows/deploy.yml`):

```yaml
name: Deploy to Dokploy

on:
  push:
    branches: [ main ]  # Deploy on push to main branch

jobs:
  deploy:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout code
      uses: actions/checkout@v4

    - name: Deploy to Dokploy
      uses: ahmedabdou14/dokploy-deploy-action@v1.0.0
      with:
        dokploy_url: ${{ secrets.DOKPLOY_URL }}
        auth_token: ${{ secrets.DOKPLOY_API_KEY }}
        application_id: ${{ secrets.DOKPLOY_APPLICATION_ID }}
```