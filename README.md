# Action deprecated

> [!WARNING] 
> This action is deprecated and will become oudated over time. We recommend switching your workflows to directly installing Wasp and running the `wasp deploy` command.

Example workflow for deploying the Wasp application to Fly using `wasp deploy`:

```yaml
name: Wasp Deploy

on:
  push:
    branches:
      - main

jobs:
  deploy:
    name: Deploy to Fly.io
    runs-on: ubuntu-latest
    env:
      # You must add FLY_API_TOKEN to your Repository Secrets
      FLY_API_TOKEN: ${{ secrets.FLY_API_TOKEN }}

    steps:
      - uses: actions/checkout@v5

      - name: Setup Node.js
        uses: actions/setup-node@v6
        with:
          node-version: '22'

      - name: Install Wasp
        run: curl -sSL https://get.wasp.sh/installer.sh | sh -s -- -v 0.19.0

      - name: Install Flyctl
        uses: superfly/flyctl-actions/setup-flyctl@master

      - name: Deploy
        run: wasp deploy fly deploy
```

# deploy-action 🚀

Github Action to deploy with Wasp to Fly.io

## How to setup Deploy on Push

### Launch your app locally once ⚠️

- You should first launch your app locally with `wasp deploy fly launch <basename> <region>`.
- After your app is launched, make sure to commit the `fly-server.toml` and `fly-client.toml` files.

### Action Inputs

#### Get your API token from Fly.io

- Login with Fly.io and go here: https://fly.io/user/personal_access_tokens
- Click `Create token` and copy that value.
- Add your Fly.io token as a repository secret e.g. calling it `FLY_TOKEN`

  Read more about how to do it: https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository

#### Setting a Custom Server URL

If you have configured a custom domain for your server, you can specify it as a repository secret named `SERVER_URL`. If this is not defined, Wasp will default to using the `<app-name>-server.fly.dev` address.

For detailed instructions on setting up repository secrets, visit: [GitHub Docs: Creating Encrypted Secrets for a Repository](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository).

#### Setting a Wasp Version

You can specify the version of Wasp to use for deployment by setting the `wasp-version` input. If this is not defined, Wasp will default to using the latest version.

### Add the Action to your repo

Create a file called `deploy.yml` in `.github/workflows` folder in your repo with this content:

```yml
name: Deploy to Fly

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
          # Required: Fly.io API token
          fly-token: ${{ secrets.FLY_TOKEN }}
          # Optional: Override the default Fly server URL with a custom domain
          server-url: ${{ secrets.SERVER_URL }}
          # Optional: Set the Wasp version to use, defaults to latest
          wasp-version: "0.16.0"
```

Notice that we are using the `secrets.FLY_TOKEN` so Wasp knows how to deploy.
