---
layout: post
title: "Workflow: check whether the PR is up to date"
---

Someone asked me to review his pr which is not ye up to date with the target branch. I think there should be a github action which can auto mark the pr as failed if it isn't up to date yet.

So I create a github action. Here's the steps:

1. In the repository, create a folder named `.github`
2. In the `.github` folder, create a child folder named `workflows`
3. In the `workflows` folder, create a file with whatever name you like, in my case `check-pr.yml`
4. In the `check-pr.yml`, add the content below:

```yml
name: PR-Check

on:
  pull_request:
    branches: [ "dev", "main", "prod" ]

jobs:
  Check-pr-uptodate:
    runs-on: ubuntu-latest
    steps:
      - name: Check out repository
        with:
          fetch-depth: 0
        uses: actions/checkout@v4
      - run: echo "The repository has been cloned to the runner"
      - run: |
          if git merge-base --is-ancestor origin/${{github.event.pull_request.base.ref}} HEAD
          then
            echo "Branch is up to date"
          else
            echo "Branch needs update"
            exit 1
          fi

```

Explanation:

- on: specify the event to trigger the action.
  - pull_request: the action is triggered by pull request.
    - branches: the target branch of the pr. If the pr's target branch is not in the list, the action will not be triggered.
- jobs: job's the action will do. You can set multiple jobs in one action file.
  - Check-pr-uptodate: this is a custom job name, you can set to whatever you like.
    - runs-on: the operating system you want to run the action on.
    - steps: One job may have many steps, they are executed by sequence.
      - name: You can give the step a name
      - uses: the already ready to use actions provided, you can search them on github.
      - with: the options applied to the action of the current step
      - run: command to run

As you can see, some steps does not have a name. In fact, the last two steps written by my self does not have a name. But the first one which is from github actions collection does, and it also has a `uses` option to specify what action to run.

I searched a few and don't know if it works if you place the file in other branch other than main(the default branch).But I recommended you don't waste two much time on it and just place it in the main branch, then it will work perfectly.

It looks like so easy to do but I took half of a day to make it work, honestly.
