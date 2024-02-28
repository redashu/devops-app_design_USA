
### app Design pattern components 

<img src="pat.png">

### java app -- with terraform - ansible pipeline 

### pipelinefile

```
# Maven
# Build your Java project and run tests with Apache Maven.
# Add steps that analyze code, save build artifacts, deploy, and more:
# https://docs.microsoft.com/azure/devops/pipelines/languages/java

trigger:
- master

pool: Default 
  # vmImage: ubuntu-latest

stages:
- stage: build
  jobs:
  - job: maventowar
    steps:
    - task: Maven@3
      inputs:
        mavenPomFile: 'pom.xml'
        mavenOptions: '-Xmx3072m'
        javaHomeOption: 'JDKVersion'
        jdkVersionOption: '1.8'
        jdkArchitectureOption: 'x64'
        publishJUnitResults: true
        testResultsFiles: '**/surefire-reports/TEST-*.xml'
        goals: 'package'
- stage: createInfra
  jobs:
  - job: test_terraform
    steps: 
    - script: echo "hello terraform"


```

### intro about terraform 

<img src="terraform.png">

### azure pipeline 

```
# Maven
# Build your Java project and run tests with Apache Maven.
# Add steps that analyze code, save build artifacts, deploy, and more:
# https://docs.microsoft.com/azure/devops/pipelines/languages/java

trigger:
- master

pool: Default 
  # vmImage: ubuntu-latest

stages:
- stage: build
  jobs:
  - job: maventowar
    steps:
    - task: Maven@3
      inputs:
        mavenPomFile: 'pom.xml'
        mavenOptions: '-Xmx3072m'
        javaHomeOption: 'JDKVersion'
        jdkVersionOption: '1.8'
        jdkArchitectureOption: 'x64'
        publishJUnitResults: true
        testResultsFiles: '**/surefire-reports/TEST-*.xml'
        goals: 'package'
- stage: createInfra
  jobs:
  - job: test_terraform
    steps: 
    - script: | 
        echo "hello terraform"
        terraform -v 
        cd terraform_script
        terraform init 
        terraform plan 
        terraform apply --auto-approve



```
