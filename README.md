# JC Workflows

This repository contains reusable Github workflows for JC. 
This has below workflows

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
```
jobs:
  build-publish:
      uses: JMCRACKER/jsdn-devops-workflows/.github/workflows/maven-ci.yml@main
      secrets: inherit
```
