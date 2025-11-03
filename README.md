# deploy-action 🚀

Github Action to deploy Wasp apps to Fly.io or Railway.

Read more on each platform in our [docs](https://wasp.sh/docs/deployment/deployment-methods/wasp-deploy/overview).

## Action Inputs

### General

- `platform` (required): 'fly' or 'railway'
- `server-url` (optional): If you have configured a custom domain for your server, provide its URL here. If this is not defined, Wasp will default to using the deployment URL provided by the platform.
- `wasp-version` (optional): Specific Wasp version to use, defaults to latest

### Fly.io Specific

- `fly-token` (required for Fly): Fly.io API token

### Railway Specific

- `railway-token` (required for Railway): Railway API token
- `project-name` (required for Railway): Project name, max 25 characters
- `railway-workspace-id` (optional): Railway workspace ID for multi-workspace accounts

## Github Action Secrets

For detailed instructions on setting up repository secrets, visit: [GitHub Docs: Creating Encrypted Secrets for a Repository](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository).

## Deploying to Fly.io

- Prerequisites: Run `wasp deploy fly launch <basename> <region>` locally first
- Commit the generated `fly-server.toml` and `fly-client.toml` files to repository
- Get Fly.io API token from https://fly.io/user/personal_access_tokens
- Add token as repository secret called `FLY_TOKEN`

### Example

```yml
name: Deploy to Fly.io

on:
  push:
    branches:
      - "main"

jobs:
  deploy:
    name: Deploy with Wasp
    runs-on: ubuntu-latest
    steps:
      - uses: wasp-lang/deploy-action@main
        with:
          platform: fly
          fly-token: ${{ secrets.FLY_TOKEN }}
          server-url: ${{ secrets.SERVER_URL }} # Optional
          wasp-version: "0.18.0" # Optional
```

## Deploying to Railway

- Prerequisites: Run `wasp deploy railway launch <project-name>` locally first
- No configuration files to commit (Railway stores config on platform)
- Project name MUST be max 25 characters
- Get a Railway **project token**
- Add token as repository secret called `RAILWAY_TOKEN`
- Add Railway workspace ID as repository secret called `RAILWAY_WORKSPACE_ID` (optional, needed for multi-workspace accounts)

### Getting the Railway Token

### Example

```yml
name: Deploy to Railway

on:
  push:
    branches:
      - "main"

jobs:
  deploy:
    name: Deploy with Wasp
    runs-on: ubuntu-latest
    steps:
      - uses: wasp-lang/deploy-action@main
        with:
          platform: railway
          railway-token: ${{ secrets.RAILWAY_TOKEN }}
          project-name: my-app # Required, max 25 characters
          railway-workspace-id: ${{ secrets.RAILWAY_WORKSPACE_ID }} # Optional
          server-url: ${{ secrets.SERVER_URL }} # Optional
          wasp-version: "0.18.0" # Optional
```
