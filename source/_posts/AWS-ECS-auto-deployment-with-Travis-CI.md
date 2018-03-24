---
title: AWS ECS continuous deployment with Travis CI
date: 2018-03-19
categories:
- AWS
tags:
- aws
- ci
- deloyment
---

In this article I am going to talk about how to build a continuous deployment pipeline for an [AWS ECS](https://aws.amazon.com/ecs/) application using [Travis CI](https://travis-ci.org).

<!-- more -->

## Problem

Deploying a docker-base application to the AWS ECS is a tedious task. It requires to push the image to an image repository, create a new task definition with that image, and update the service with the new definition. It is quick but repetitive.

In large organizations that have rapid deployment cycles, such tasks are usually taken care by CI/CD pipelines, like [Jenkins](https://jenkins.io/index.html). But for a personal side projecthttps://jenkins.io/index.html, a dedicated CI/CD system is not affordable and it is an overkill lto use

[Travis CI](https://travis-ci.org) is a continuous deployment service that provides free integration and service with public GitHub repositories. If you develop an open-source project at GitHub and add a `.travis.yml` file, Travis CI can connect with the repository and react to any code change.

This article assumes you have basic knowledge on AWS ECS and Travis CI.

## Script Deployment in Travis CI

The requirement of the continuous deployment to AWS ECS is simple. Every time a pull request to the master branch is merged, the Travis CI should be noticed and perform the continuous deployment.

The deployment to AWS ECS requires custom operations and it is not automated by the Travis CI yet. To support sophisticated deployment operations, the Travis CI provides [Script Deployment](https://docs.travis-ci.com/user/deployment/script/) and it allows the developer to execute a specified script for deployment.

It can be activated by adding a new `deploy` section in the `.travis.yml` file in the project repository.

``` yaml
# deployment section in the .travis.yml
deploy:
  provider: script
  # specify the deployment script
  script: bash deploy.sh
  # specify to deploy with code change a given branch
  on:
    branch: develop
```

## Deployment Script

The next step is to define tasks for the deployment. We would like to define more repetitive tasks for the Travis CI and leave the most important action to the developer, like clicking the `Merge` button at the GitHub PR.

Specifically, these steps are required:

1. build the docker image from the source code
2. tag the docker image as `latest`
3. push the docker image to an image repository
4. update the AWS ECS application with the new image

The first three steps could be done with the [docker CLI](https://docs.docker.com/engine/reference/commandline/cli/). The fourth step actually includes many interactions with AWS, but a very nice library called [ecs-deploy](https://github.com/silinternational/ecs-deploy) could do all things with one line of command!

``` bash
# install AWS SDK
pip install --user awscli
export PATH=$PATH:$HOME/.local/bin

# install necessary dependency for ecs-deploy
add-apt-repository ppa:eugenesan/ppa
apt-get update
apt-get install jq -y

# install ecs-deploy
curl https://raw.githubusercontent.com/silinternational/ecs-deploy/master/ecs-deploy | \
  sudo tee -a /usr/bin/ecs-deploy
sudo chmod +x /usr/bin/ecs-deploy

# build the docker image and push to an image repository
eval $(aws ecr get-login --region us-east-1)
docker build -t haoliangyu/ecs-auto-deploy .
docker tag haoliangyu/ecs-auto-deploy:latest $IMAGE_REPO_URL:latest
docker push $IMAGE_REPO_URL:latest

# update an AWS ECS service with the new image
ecs-deploy -c $CLUSTER_NAME -n $SERVICE_NAME -i $IMAGE_REPO_URL:latest
```

All `$VARIABLE_NAME` in the deployment script refer to an environment variable. Except `PATH` and `HOME`, which are provided by the operation system, you should provide the rest of them:

  * `IMAGE_REPO_URL` is the url of a docker image repository. It could be [DockerHub](https://hub.docker.com/), [AWS ECR](https://aws.amazon.com/ecr), or any other. In the example code, it works with AWS ECR.
  * `CLUSTER_NAME` is the name of the running ECS cluster.
  * `SERVICE_NAME` is the name of the running ECS service.

These values could be hard-coded, but using an environment variable makes the script more secure and portable.

Note that `ecs-deploy` deploys to an existing ECS service. If the specified service is not created, it will not try to new one and throw an error instead.

## Continuous Deployment

With the deployment script discussed above, we can write the Travis CI configuration `.travis.yml`.

``` yaml
# I am using a nodejs for my demo application
language: node_js
node_js:
  - "node"

# include the docker service so that we can use the docker command in
# the deployment script
services:
  - docker

# same as the official documentation
deploy:
  provider: script
  script: bash deploy.sh
  on:
branch: master
```

The configuration is pretty much the same as the one from the documentation. It requires the `docker` service for the docker command line tool.

Then you should add required environment variables in the `Settings` page of the Travis repository. Additionally, `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, and `AWS_DEFAULT_REGION` are needed to help accessing AWS.

{% asset_img travis-env.png This is an example image %}

## Final

Wow, you are done here :tada: With this setting, you will have a continuous deployment pipeline that reacts to any PR merged into the master branch. And it deploys :-)

{% asset_img travis-deploy.png This is an example image %}

Thank you for reading this blog post. All code in this post could be found in this [GitHub repository](https://github.com/haoliangyu/ecs-auto-deploy) (:star: it if it helps) and it is [working](https://travis-ci.org/haoliangyu/ecs-auto-deploy).
