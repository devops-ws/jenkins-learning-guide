# Learning guide for Jenkins
Hopefully this guide could help you have a better understand of Jenkins, and even be good at it.

## What is it
Before we get started, it's important to figure out what Jenkins is.

Jenkins is an open-source automation server. It's a community driven project, and belongs to the [Continuous deliver Foundation](https://cd.foundation/) (aka, CDF). But it orinally came from [Sun Microsystems](https://en.wikipedia.org/wiki/Sun_Microsystems).

From the technical perspective, it is written by Java. There are over 1800 plugins you could find from [the community](https://plugins.jenkins.io/). Basically you will be able to the exsiting plugin to do what everything you want.

## Why do we use it
There are serval reasons that make it be worth to let you choose it.

* The community is very active, you could ask questions from multiple channels
  * [Forum](https://community.jenkins.io/), GitHub issues, [Mailling list](https://www.jenkins.io/mailing-lists/), or [Chat](https://www.jenkins.io/chat/)
* Easy installation
  * You could install Jenkins via: War package, Native package, Docker, Kubernetes, and more
* Easy configuration
  * Almost all the configuration items have its description
* Plugins
* Extensible
  * It's easy to use the plugin mechanism to extend Jenkins
* Distributed
  * Jenkins can easily distribute work across multiple machines, helping drive builds, tests and deployments across multiple platforms faster.

## How can we use it
Please make sure you have JRE 11 (Java Runtime Environment) or Docker. Your computer should has at least 1G memory, and 5G storage for the learing purpose.

### Installation
There are four common ways to install Jenkins.

* [Single Jenkins War file](https://www.jenkins.io/doc/book/installing/war-file/)
* Running in a [Tomcat](https://tomcat.apache.org/)
* [Running in a container](https://www.jenkins.io/doc/book/installing/docker/)
* [Running in a Kubernetes](https://www.jenkins.io/doc/book/installing/kubernetes/)

A simple command to run Jenkins from a single war file:
```shell
java -jar jenkins.war
```

A simiple command to run Jenkins in a container:
```shell
docker run -d -p 8080:8080 jenkins/jenkins:2.361.3-jdk11
```

See [the official installation tutorial](https://www.jenkins.io/doc/book/installing/).

### Basic usage
Task list:
* Create a free-style job, generate a file then archive it.
* Add a parameter for the job
* Set a job watch trigger
* Create a view

### Pipeline
Task list:
* Understand the Syntax
* Be familiar with some important Pipeline steps
* Build and publish a Docker image with Pipeline


```groovy
pipeline {
    agent {
        label 'java'
    }

    stages {
        stage ('clone') {
            checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/devops-ws/learn-pipeline-java']]])
        }
        stage ('build') {
            sh 'mvn clean package'
        }
    }
}
```

See [the Pipeline syntax manual](https://www.jenkins.io/doc/book/pipeline/syntax/) or the [Snippet Generator](http://localhost:8080/pipeline-syntax/).

### Mutli-branch Pipeline
Task list:
* [Understand the git](git.md)
* Create a GitHub multi-branch Pipeline
* Understand some important setting items

### Run in Kubernetes
