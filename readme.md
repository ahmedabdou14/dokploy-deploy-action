# Dokploy Deployment GitHub Action

This GitHub Action triggers a deployment on Dokploy.

## Inputs

### `auth_token`

**Required** The Dokploy API key (used as x-api-key header).

### `application_id`

**Required** The Dokploy application ID.

### `dokploy_url`

**Required** Dokploy dashboard URL (this should have the Dokploy API accessible at /api) - no trailing backslash.

e.g. `https://server.example.com`

## Usage

To use this action, include it in your workflow file as follows:

```yaml
name: Dokploy Deployment Workflow

on: [push]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout code
      uses: actions/checkout@v4

    - name: Dokploy Deployment
      uses: ahmedabdou14/dokploy-deploy-action@v1.0.0
      with:
        auth_token: ${{ secrets.DOKPLOY_API_KEY }}
        application_id: ${{ secrets.DOKPLOY_APPLICATION_ID }}
        dokploy_url: ${{ secrets.DOKPLOY_URL }}
```

## Contributing

Contributions are welcome! Please feel free to submit a pull request or open an issue for any bugs or feature requests.


## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.