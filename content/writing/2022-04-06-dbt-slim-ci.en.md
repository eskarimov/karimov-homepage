+++
date = 2022-04-05
isPopular = false
tags = ["data engineering", "dbt", "github actions"]
thumbnailPath = "/self/img/thumbs/pipeline.jpg"
title = "Implementing slim CI for dbt with GitHub Actions"

+++

Recently I've started working with dbt, and have to say it's quite amazing.
With this post I'd like to share the approach for deploying only newly created/modified models, known as slim CI.

Imagine we have an Airflow instance executing our dbt DAG daily.

In case we introduce structural changes in our models, or simply by creating a new model,
we don't want to wait till Airflow starts on schedule.
Also, we don't want to fire the whole pipeline execution, because it might be costly to run it multiple times per day.

What we could do in this case is to introduce a new CI step,
which will compare differences between old and new models,
and run only those, which have changed (and their dependencies/downstream tasks).

How it works with GitHub Actions:

say we have `deploy_dbt.yml` file describing our CI actions

```yml
name: 'Deploy dbt'

on:
  push:
    branches:
      - main
env:
  DBT_VERSION: 1.0.0
jobs:
  dbt-slim-ci:
    name: Deploy dbt models
    runs-on: ubuntu-latest
    permissions:
      actions: read
      contents: read
    steps:
      - uses: actions/checkout@v2
      # Get commit hash of the last successful deployment, it will be used for comparison
      - uses: nrwl/last-successful-commit-action@v1
        id: last_successful_commit
        with:
          branch: 'main'
          workflow_id: 'deploy_dbt.yml'
          github_token: ${{ secrets.GITHUB_TOKEN }}
      - name: Checkout last successful main
        uses: actions/checkout@v2
        with:
          ref: ${{ steps.last_successful_commit.outputs.commit_hash }}
          path: last_successful_main/
      - name: Install dbt & packages
        run: |-
          pip3 install dbt==${{ env.DBT_VERSION }}
          dbt deps
      - name: Generate last successful manifest.json
        run: >
          dbt compile
          --project-dir last_successful_main/
          --profiles-dir last_successful_main/
      - name: Build and test new models
        run: >
          dbt build
          --select state:modified+
          --defer
          --state last_successful_main/target/
```

Happy coding!
