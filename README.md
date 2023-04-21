# deploy-action 🚀
Github Action to deploy with Wasp to Fly.io

## How to setup Deploy on Push

### Get your API token from Fly.io

- Login with Fly.io and go here: https://fly.io/user/personal_access_tokens
- Click `Create token` and copy that value.

### Add the token as a secret

Add your Fly.io token as a repository secret e.g. calling it `FLY_TOKEN`

Read more about how to do it: https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository

### Add a Github Action
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
          fly-token: ${{ secrets.FLY_TOKEN }}
```

Notice that we are using the `secrets.FLY_TOKEN` so the app knows to deploy.
