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

### Setting a Working Directory

You can specify the working directory for Wasp to deploy from by setting the `working-dir` input. If this is not defined, Wasp will default to using the current/default directory.

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
          # Optional: Set the working directory to deploy from
          working-dir: "app"
```

Notice that we are using the `secrets.FLY_TOKEN` so Wasp knows how to deploy.
