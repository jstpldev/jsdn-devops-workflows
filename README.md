# JC Workflows

This repository contains reusable Github workflows for JC. 

This has below steps

## CI Maven Workflow
This workflow executes below steps:
* Code checkout
* Config checkout
* Setup Java
* Setup Maven
* Setup settings xml
* Static code analysis
* Build
* Publish

### Calling this workflow
This workflow can be called by other repos for their ci.
In any jave codebase repo, add a workflow yaml file under .github/workflows/ with below content.
```
jobs:
  build-publish:
      uses: JMCRACKER/jsdn-devops-workflows/.github/workflows/maven-ci.yml@main
      secrets: inherit
```

Example with full yml
```
name: Build and Publish

on:
  push:
    branches:
      - main
      - develop
      - 'feature/**'
      - 'release/**'
      - 'hotfix/**'
  pull_request:
    branches:
      - main
      - develop
      - 'release/**'
  workflow_dispatch:

jobs:
  build-publish:
      uses: JMCRACKER/jsdn-devops-workflows/.github/workflows/maven-ci.yml@main
      secrets: inherit
```
