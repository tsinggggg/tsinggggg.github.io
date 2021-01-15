---
layout: post
title: "Engineering: openshift tutorial notes"
date: 2021-01-13
tags: [openshift]
---
[Source: https://learn.openshift.com/](https://learn.openshift.com/)

# Using OpenShift
Learn the basics of OpenShift through deploying and managing a container.

## Log in through web console

## Logging in Via the Command Line

+ OpenShift command line tool `oc`. 

+ For your own cluster, you would need to know the URL to login to the cluster, and pass it as an argument to `oc login`.

+ verify user: `oc whoami`

+ verify server: `oc whoami --show-server`

+ list projects: `oc get projects`


## Collaborating with Other Users

+ `Edit Project` -> `Role Bindings` -> `Create Role Binding`

+ Role type: `edit`, `view`, `admin`

+ create a project `oc new-project mysecrets`

+ add the ability for `developer` to also view project `mysecrets`:

`oc adm policy add-role-to-user view developer -n mysecrets`


## Switching Between Accounts

+ `oc login --username developer`

+ `oc login url`

+ `oc config get-clusters`

+ `oc whoami --show-context`

+ `oc whoami --show-context`

# Introduction

## Getting Started with OpenShift for Developers
Learn how to use the OpenShift Container Platform to build and deploy an application with a data backend and a web frontend.

### Exploring The Command Line
The OpenShift CLI is accessed using the command `oc`. From here, you can administrate the entire OpenShift cluster and deploy new applications.

The CLI exposes the underlying Kubernetes orchestration system with the enhancements made by OpenShift. `oc` provides all of the functionality of `kubectl`, along with additional functionality to make it easier to work with OpenShift. 

### Exploring The Web Console

OpenShift is often referred to as a container application platform in that it is a platform designed for the development and deployment of applications in containers.

To group your application, we use projects. The reason for having a project to contain your application is to allow for controlled access and quotas for developers or teams.

More technically, it's a visualization of the Kubernetes namespace based on the developer access controls.

+ `Administrator Perspective` vs `Developer Perspective`

+ `Topology`: different ways to add content to your project


### Deploying a Docker Image
+ `Topology` - > `Container Image`

+ example image from external registry:
`docker.io/openshiftroadshow/parksmap-katacoda:1.2.0`

+ By default, creating a deployment using the Container Image method will also create a Route for your application. A Route makes your application available at a publicly accessible URL.

+ This should work with any container image that follows best practices, such as defining the port any service is exposed on, not needing to run specifically as the root user or other dedicated user, and which embeds a default command for running the application.

### Scaling Your Application

+ click inside the circle for an app from `Topology` view to open side panel

+ `Details`

+ `up`

+ To verify, click `Resources` and should see 2 pods.

### application self healing

+ `Resources` open one of the pods-> `Actions` -> `Delete Pod`


### Creating a Route

+ `Admin` -> `Networking` -> `Route` -> `Create Route`

+ Also can view it in `developer` mode, at the top right corner of a pod


### Building From Source Code

+ Source-to-Image: deploy an app from git repo

+ https://github.com/openshift-roadshow/nationalparks-katacoda

+ `Add` -> `From Catelog` -> `Python` in `Language` -> `Python` -> `Create Application`