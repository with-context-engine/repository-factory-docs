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

```bash
        run: |
          RESPONSE=$(curl -L --silent \
          -H "Accept: application/vnd.github+json" \
          -H "Authorization: Bearer $APP_TOKEN" \
          -H "X-GitHub-Api-Version: 2022-11-28" \
          https://api.github.com/repos/$GITHUB_REPOSITORY )
```

#### Send a CML Runner a Job




https://github.com/apps/repository-factory-worker