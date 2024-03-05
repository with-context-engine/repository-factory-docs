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

> [!IMPORTANT]
> You can follow the guide on Github's [page](https://docs.github.com/en/apps/creating-github-apps/writing-code-for-a-github-app/quickstart) to create your own service user / app, or, follow the simple advice below. 

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

You can simply install the following [app](https://github.com/apps/repository-factory-worker) onto your own repository. 

## Credentials from Github App needed


