# Craft Kubernetes Workshop

In this workshop you will learn how to:

* Provision a basic Kubernetes cluster from the ground up using [Google Compute Engine](https://cloud.google.com/compute)
* Provision a complete Kubernetes using [Google Container Engine](https://cloud.google.com/container-engine)
* Deploy and manage Docker containers using kubectl

Kubernetes Version: 1.2.2

## Google Compute Engine (GCE)

GCE will be used to setup a Kubernetes cluster from the ground up. This workshop will require the ability to create the following resources:

* Virtual Machines
* Routes
* Firewall Rules

### Setup GCE and Enable Cloud Shell 

In this section you will create a Google Compute Engine (GCE) account. GCE will allow you to the create VMs, Networks, and Storage volumes required for this workshop. GCE also provides the [Cloud Shell](https://cloud.google.com/shell/docs) computing environment that will be used complete the labs.

  * [Enable and explore Cloud Shell](labs/enable-and-explore-cloud-shell.md)

### Clone this Repository

Login into your Cloud Shell environment and clone this repository.

```
git clone https://github.com/rahulaga/craft-kubernetes-workshop.git
```

## Containers
* Unix processes not lightweight Virtual Machines
* application + dependencies = image
* Runtime environment (cgroups, namespaces, env vars)

![Container](images/container.png)

Build a container defined in a Dockerfile.

## Kubernetes
* Container management, scheduling, and service discovery.
* API driven application management
* Agents monitor endpoints for state changes (real-time)
* Controllers enforce desired state
* Labels identify resources (nodes, applications, services)

### High level concepts
* node
* pod
* scheduler
* replication controller
* service

### Node
* Runs containers and proxies service requests.
* docker
* kubelet
* proxy

!(images/kubernetes-nodes-2.png)

### Pod
* Represents a logical application.
* One or more containers
* Shared namespaces

!(images/pod.png)

### Scheduler
* Schedules pods to run on nodes.
* Global scheduler for long running jobs
* Best fit chosen based on pod requirements
* Pluggable

!(images/kubernetes-scheduler.png)

### Replication Controller
* Manages a replicated set of pods.
* Creates pods from a template
* Ensures desired number of pods are running
* Online resizing

!(images/kubernetes-rc.png)

* Self-healing

!(images/kubernetes-rc-reschedule.png)
### Service
* Service discovery for pods.
* Proxy runs on each node
* Virtual IP per service (avoid port collisions)
* Basic round-robin algorithm
* Dynamic backends based on label queries

## Provision Kubernetes using GKE

Kubernetes can be configured with many options and add-ons, but can be time consuming to bootstrap from the ground up. In this section you will bootstrap Kubernetes using [Google Container Engine](https://cloud.google.com/container-engine) (GKE).

GKE is a hosted Kubernetes by Google. GKE clusters can be provisioned using a single command.

GKE clusters can be customized and supports different machine types, number of nodes, and network settings. 

## Create a Kubernetes cluster using gcloud

```
gcloud container clusters create craft \
  --disk-size 200 \
  --enable-cloud-logging \
  --enable-cloud-monitoring \
  --machine-type n1-standard-1 \
  --num-nodes 3 
```


## Managing Applications with Kubernetes

Kubernetes is all about applications and in this section you will utilize the Kubernetes API to deploy, manage, and upgrade applications. In this part of the workshop you will use an example application called "app" to complete the labs.

[App](https://github.com/kelseyhightower/app) is hosted on GitHub and provides an example 12 Factor application. During this workshop you will be working with the following Docker images:

* [kelseyhightower/monolith](https://hub.docker.com/r/kelseyhightower/monolith) - Monolith includes auth and hello services.
* [kelseyhightower/auth](https://hub.docker.com/r/kelseyhightower/auth) - Auth microservice. Generates JWT tokens for authenticated users.
* [kelseyhightower/hello](https://hub.docker.com/r/kelseyhightower/hello) - Hello microservice. Greets authenticated users.
* [ngnix](https://hub.docker.com/_/nginx) - Frontend to the auth and hello services.

#### Labs

  * [Creating and managing pods](labs/creating-and-managing-pods.md)
  * [Monitoring and health checks](labs/monitoring-and-health-checks.md)
  * [Managing application configurations and secrets](labs/managing-application-configurations-and-secrets.md)
  * [Creating and managing services](labs/creating-and-managing-services.md)
  * [Creating and managing deployments](labs/creating-and-managing-deployments.md)
  * [Rolling out updates](labs/rolling-out-updates.md)

## Links

  * [Kubernetes](http://googlecloudplatform.github.io/kubernetes)
  * [gcloud Tool Guide](https://cloud.google.com/sdk/gcloud)
  * [Docker](https://docs.docker.com)
  * [etcd](https://coreos.com/docs/distributed-configuration/getting-started-with-etcd)
  * [nginx](http://nginx.org)
