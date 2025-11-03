# deploy-action 🚀

<!-- TODO: Update intro to mention both Fly.io and Railway support -->

<!-- TODO: Add platform comparison table showing key differences between Fly.io and Railway -->

## Deploying to Fly.io

<!-- TODO: Explain Fly.io setup:
- Prerequisites: Run `wasp deploy fly launch <basename> <region>` locally first
- Commit the generated `fly-server.toml` and `fly-client.toml` files to repository
- Get Fly.io API token from https://fly.io/user/personal_access_tokens
- Add token as repository secret called FLY_TOKEN
- Link to GitHub docs on creating secrets
-->

<!-- TODO: Show example workflow for Fly.io deployment:
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
          server-url: ${{ secrets.SERVER_URL }}  # Optional
          wasp-version: "0.16.0"                 # Optional
```
-->

## Deploying to Railway

<!-- TODO: Explain Railway setup:
- Prerequisites: Run `wasp deploy railway launch <project-name>` locally first
- No configuration files to commit (Railway stores config on platform)
- Project name MUST be max 25 characters
- Get Railway token from Project Settings → Tokens (project token recommended)
- Add token as repository secret called RAILWAY_TOKEN
- Optional: Workspace ID for multi-workspace accounts
- Link to GitHub docs on creating secrets
-->

<!-- TODO: Show example workflow for Railway deployment:
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
          project-name: my-app                       # Required (max 25 chars)
          railway-workspace: ${{ secrets.RAILWAY_WORKSPACE }}  # Optional
          server-url: ${{ secrets.SERVER_URL }}      # Optional
          wasp-version: "0.16.0"                     # Optional
```
-->

## Action Inputs

<!-- TODO: Document all inputs:
- platform (required): 'fly' or 'railway'
- fly-token (required for fly): Fly.io API token
- railway-token (required for railway): Railway API token
- project-name (required for railway): Project name, max 25 characters
- railway-workspace (optional): Railway workspace ID for multi-workspace accounts
- server-url (optional): Custom server URL for the React app
- wasp-version (optional): Specific Wasp version to use, defaults to latest
-->

## Breaking Changes

<!-- TODO: Add breaking change notice:
- Existing users MUST add `platform: fly` to their workflow to continue working
- The `fly-token` input is no longer required by default (only when platform is 'fly')
- Show before/after example
-->
