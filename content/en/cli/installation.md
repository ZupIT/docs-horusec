---
title: Installation 
weight: 5
description: >-
  In this section, you will find guidelines to install Horusec-CLI.
---

There are 4 ways to install Horusec-CLI:

1. Local Installation 
2. Manual Installation  
3. Installation via Imagem Docker 
4. Installation via Pipeline

See each one of them below: 

## **Requirements**
Check out the requirements to use Horusec-CLI:

* [**Docker**](https://docs.docker.com/get-docker/) (recommended version ```19.03.11```). If you want to disable Docker, check out [**how to use Horusec without Docker tutorial**]({{< ref path="tutorials/how-to-use-horusec-without-docker.md" lang="en">}}), but you may lose data from analysis made by [**other tools**]({{< ref path="cli/analysis-tools/security-tools" lang="en">}}).

* [**Git**](https://git-scm.com/) (recommended version ```2.25.1```). If you want to run analysis with Git, check out [**how to enable git history analysis tutorial**]({{< ref path="tutorials/how-to-enable-git-history-analysis-and-enable-commit-authors.md" lang="en">}}), but it is not enabled by default.

## **Local Installation**
This installation is recommended if you want to use Horusec for analysis or for searching for vulnerabilities in your project. 

See below the commands to install Horusec locally according to your operating system: 


### **MAC or Linux**
Run the command below in your terminal: 

```bash
curl -fsSL https://raw.githubusercontent.com/ZupIT/horusec/main/deployments/scripts/install.sh | bash -s latest
```

### **Windows**
Run the command below in your terminal: 

{{% alert color="warning" %}}
You always need to run the command where you have downloaded the executable.
{{% /alert %}}

```bash
curl -k "https://github.com/ZupIT/horusec/releases/latest/download/horusec_win_amd64.exe" -o "./horusec.exe" && ./horusec.exe version
```

{{% alert color="info" %}}
In Horusec there are two types of binary:
- "Normal": In this type of binary you have the default execution using Docker;
- "StandAlone": In this type of binary you have only tools that use Horusec-Engine without dependence with the docker.
{{% /alert %}}

{{% alert color="info" %}}
👉[**A última versão disponível**](https://github.com/ZupIT/horusec/releases/latest)

👉[**Todas as versões disponíveis** ](https://github.com/ZupIT/horusec/releases)
{{% /alert %}}



## **Manual installation**

The manual installation is done according to your operating system and the version you want to download. 
See the latest versions below: 

**Horusec has support for:**

| Operational system | Processor Architecture | Binary Type | Download |
|---------------------|----------------------------|-----------------|----------|
| Linux               | amd64                      | Binário normal  | [📥 Download](https://github.com/ZupIT/horusec/releases/download/v2.6.5/horusec_linux_amd64) |
| Linux               | arm64                      | Binário normal  | [📥 Download](https://github.com/ZupIT/horusec/releases/download/v2.6.5/horusec_linux_arm64) |
| Linux               | amd64                      | Instalador debian normal | [📥 Download](https://github.com/ZupIT/horusec/releases/download/v2.6.5/horusec_linux_amd64.deb) |
| Linux               | arm64                      | Instalador debian normal | [📥 Download](https://github.com/ZupIT/horusec/releases/download/v2.6.5/horusec_linux_arm64.deb) |
| Linux               | amd64                      | Instalador rpm normal | [📥 Download](https://github.com/ZupIT/horusec/releases/download/v2.6.5/horusec_linux_amd64.rpm) |
| Linux               | arm64                      | Instalador rpm normal | [📥 Download](https://github.com/ZupIT/horusec/releases/download/v2.6.5/horusec_linux_arm64.rpm) |
| Linux               | amd64                      | Binário Stand Alone  | [📥 Download](https://github.com/ZupIT/horusec/releases/download/v2.6.5/horusec_linux_amd64_stand_alone) |
| Linux               | arm64                      | Binário Stand Alone  | [📥 Download](https://github.com/ZupIT/horusec/releases/download/v2.6.5/horusec_linux_arm64_stand_alone) |
| Mac                 | amd64                      | Binário normal  | [📥 Download](https://github.com/ZupIT/horusec/releases/download/v2.6.5/horusec_mac_amd64) |
| Mac                 | arm64                      | Binário normal  | [📥 Download](https://github.com/ZupIT/horusec/releases/download/v2.6.5/horusec_mac_arm64) |
| Mac                 | amd64                      | Binário Stand Alone  | [📥 Download](https://github.com/ZupIT/horusec/releases/download/v2.6.5/horusec_mac_amd64_stand_alone) |
| Mac                 | arm64                      | Binário Stand Alone  | [📥 Download](https://github.com/ZupIT/horusec/releases/download/v2.6.5/horusec_mac_arm64_stand_alone) |
| Windows             | amd64                      | Binário normal  | [📥 Download](https://github.com/ZupIT/horusec/releases/download/v2.6.5/horusec_win_amd64.exe) |
| Windows             | arm64                      | Binário normal  | [📥 Download](https://github.com/ZupIT/horusec/releases/download/v2.6.5/horusec_win_arm64.exe) |
| Windows             | amd64                      | Binário Stand Alone  | [📥 Download](https://github.com/ZupIT/horusec/releases/download/v2.6.5/horusec_win_amd64_stand_alone.exe) |
| Windows             | arm64                      | Binário Stand Alone  | [📥 Download](https://github.com/ZupIT/horusec/releases/download/v2.6.5/horusec_win_arm64_stand_alone.exe) |


{{% alert color="info" %}}
If you want a specific version, change the word `latest` in the link to the version you want. 
{{% /alert %}}


{{% alert color="warning" %}}
After downloading the files for Mac or Linux it will be necessary to make them `executable` through the command `chmod +x`.

1. Download the files;
2. You have to make these files `executable` through the `chmod +x`command:

```bash
chmod +x path/horusec_[your version here]
```

3. Now, you will be able to open the file for manual installation.

{{% /alert %}}

👉[**Lastest available version**](https://github.com/ZupIT/horusec/releases/latest)

👉[**All available versions**](https://github.com/ZupIT/horusec/releases)


## **Installation via Docker Image**

You can carry out your analysis through a docker image, you are able to run locally or using your pipeline. 

See some use cases below:

### **1. Starting image with the run command:**

When you initialize the image with the `run` command, just run Horusec with the command you want.

```bash
docker run -v /var/run/docker.sock:/var/run/docker.sock -v $(pwd):/src horuszup/horusec-cli:latest horusec start -p /src -P $(pwd)
```

{{% alert color="warning" %}}
Check out if the environment you are working in allows you to create a bidirectional volume because this is necessary to use Horusec in a docker image.
{{% /alert %}}

### **2. Installation via pipeline**

This installation assures the safety in the delivery of your project in production since Horusec is added to your pipeline.

See next the ways to install considering different types of pipeline:

### **Github Actions**

```yaml
name: SecurityPipeline

on: [push]

jobs:
  horusec-security:
    name: horusec-security
    runs-on: ubuntu-latest
    steps:
    - name: Check out code
      uses: actions/checkout@v2
      with: # Required when commit authors is enabled
        fetch-depth: 0
    - name: Running Horusec Security
      run: |
        curl -fsSL https://raw.githubusercontent.com/ZupIT/horusec/main/deployments/scripts/install.sh | bash -s latest
        horusec start -p="./" -e="true"
```

### **AWS Code Build**

* **Environment:**

  * Managed image
  * Operational sytem: `Ubuntu`
  * Execution time: `Standard`
  * Image: `aws/codebuild/standard:3.0`
  * Image Version:  `Latest`
  * Environment type:  `Linux`
  * Enable this indicator if you want to create Docker images or want your builds to get elevated privileges:  `true`

* Buildspec:

```yaml
version: 0.2

phases:
  install:
    runtime-versions:
      docker: 18
  build:
    commands:
      - docker run -v /var/run/docker.sock:/var/run/docker.sock -v $(pwd):/src/horusec horuszup/horusec-cli:latest horusec start -p /src/horusec -P $(pwd)
```

### **Circle CI**

```yaml
version: 2.1

executors:
  horusec-executor:
    machine:
      image: ubuntu-1604:202004-01

jobs:
  horusec:
    executor: horusec-executor
    steps:
      - checkout
      - run:
          name: Horusec Security Test
          command: |
            curl -fsSL https://raw.githubusercontent.com/ZupIT/horusec/main/deployments/scripts/install.sh | bash -s latest
            horusec start -p="./" -e="true"
workflows:
  pipeline:
    jobs:
      - horusec
```

### **Jenkins**

{{% alert color="warning" %}}
In machines that use Jenkins should have the **docker and git installed** so that Horusec has all power in their analyzes.Check for more information at the [requirements of CLI](#Requirements).
{{% /alert %}}

```groovy
stages {
    stage('Security') {
        steps {
            sh 'curl -fsSL https://raw.githubusercontent.com/ZupIT/horusec/main/deployments/scripts/install.sh | bash -s latest'
            sh 'horusec start -p="./" -e="true"'
        }
    }
}
```

### **Azure DevOps Pipeline**

```yaml
pool:
  vmImage: 'ubuntu-18.04'

steps:
- script: curl -fsSL https://raw.githubusercontent.com/ZupIT/horusec/main/deployments/scripts/install.sh | bash -s latest && horusec start -p ./
```

### **GitLab CI/CD**

```yaml
image: docker:latest

variables:
  GIT_DEPTH: 0 # Required when commit authors is enabled

services:
  - docker:dind

build-code-job:
  stage: build
  script:
    - docker run -v /var/run/docker.sock:/var/run/docker.sock -v $(pwd):/src/horusec horuszup/horusec-cli:latest horusec start -p /src/horusec -P $(pwd)
```
