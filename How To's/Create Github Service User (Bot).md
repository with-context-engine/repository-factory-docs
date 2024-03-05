---
title: Create IAM role
draft: false
tags:
  - github
  - secrets
  - variables
  - permissions
  - ecr
date: 2024-03-04
---

## Why a Github App

The `Repository Factory` Repository needs a Github app to serve as an _overlord_ of sorts to allow files to be edited, workflows to be run, etc., without the issue of the Github token provisioned in the `workflow` context to accidentally delete its own files, or run some malicious code. The Github App, therefore, has its own permission settings and scopes and can be deactivated by the user / admin at will to safely execute workflows. 

In the case of the `Repository Factory` we are using it to call a few API's and run a few actions such as the [CML](https://cml.dev/doc/ref/comment) create comment action to let the user know that a `train` or `deploy` job has successfully completed.

### Example Github App Uses

#### Call the Github API

In the example below, the Github service app is using its generated `$APP_TOKEN` to perform a REST API call against the `GET /repos/` API endpoint. 

```bash
        run: |
          RESPONSE=$(curl -L --silent \
          -H "Accept: application/vnd.github+json" \
          -H "Authorization: Bearer $APP_TOKEN" \
          -H "X-GitHub-Api-Version: 2022-11-28" \
          https://api.github.com/repos/$GITHUB_REPOSITORY )
```

#### Use a Github app token to ensure idempotency in Github Workflow

Workflows that are edited by the `workflow runner` can cause race condition issues and security issues. As a result, any time a workflow is edited it needs to be done by a third party token. 

```yml
      - name: Checkout Repository
        uses: actions/checkout@v4
        with:
          path: template-repository
          token: ${{ steps.token.outputs.token }}
```


## Creating a Github App

> [!IMPORTANT]
> You can simply install the following [app](https://github.com/apps/repository-factory-worker) onto your own repository. 

---

> [!IMPORTANT]
> You can follow the guide on Github's [page](https://docs.github.com/en/apps/creating-github-apps/writing-code-for-a-github-app/quickstart) to create your own service user / app, or, follow the simple advice below. 

## Github App Credentials

This repository uses the [following](https://github.com/marketplace/actions/github-app-token) marketplace Github Action: 

```yaml
      - name: Generate App Token
        uses: tibdex/github-app-token@v2
        id: token
        with:
          app_id: ${{ vars.APP_ID}}
          private_key: ${{ secrets.APP_PEM_PRIVATE_KEY}}
```

To retrieve the `APP_ID` and `APP_PEM_PRIVATE_KEY` follow the instructions below. 

### Getting Github App Credentials

#### `APP_ID`

1. Click on the App Settings button

	![image](https://with-context-public.s3.us-east-1.amazonaws.com/repository-factory-docs/2024/c6ffb436794cc5dc675d1a1ba8a9e6a1.png)

2. Under **"About"**, get the `APP_ID` and store it as a variable in your organization's secrets / variables store, or in the specific repository you aim to be developing. 

#### `APP_PEM_PRIVATE_KEY`

1. Under **"Private Keys"** create a new `APP_PEM_PRIVATE_KEY` by downloading a key file: 

	![image](https://with-context-public.s3.us-east-1.amazonaws.com/repository-factory-docs/2024/5d6a09dc2acaf483cf4e8d7898c13de4.png)

2. Run: 
   
```bash
pbcopy < app_private_key.pem
```

3. Paste the key into your secrets store. 

