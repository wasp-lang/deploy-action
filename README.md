# deploy-action
Github Action to deploy with Wasp to Fly.io

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
