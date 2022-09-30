# JC Workflows

This repository contains reusable Github workflows for JC. 

This has below steps

## CI Maven Workflow
This workflow executes below steps:
* **Code checkout** : This checksout the code from current building repository
* **Config checkout**: This checksout the code from common [devops config repository](https://github.com/JMCRACKER/jsdn-devops-config). This is to get the maven *settings.xml* and pmd *rules.xml*
* **Setup Java**: This sets up Java 7
* **Setup Maven** : This sets up maven 3.6
* **Setup settings xml** : This copies *settings.xml* from config repo to *.m2* folder
* **Static code analysis** : This executes the code analysis by PMD and publishes the found issues to current action run.
* **Build**: Executes maven build
* **Publish**: Executes maven deploy

### Parameters
* __analysis__: *true* or *false*. This is to set whether PMD static analysis is to be run  (Default is *false*. it will not run static analysis)
* __verbose__: *true* or *false*. This is to verbose output for maven commands (Default is *false*. it will run in the quiet mode)

### Calling this workflow
This workflow can be called by other repos for their ci.
In any jave codebase repo, add a workflow yaml file under .github/workflows/ with below content.
```
jobs:
  build-publish:
      uses: JMCRACKER/jsdn-devops-workflows/.github/workflows/maven-ci.yml@main
      secrets: inherit
      with:
        analysis: false
        verbose: false
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
      with:
        analysis: false
        verbose: false
```
